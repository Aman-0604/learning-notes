;WITH Tables AS (
    SELECT t.object_id,
           s.name AS schema_name,
           t.name AS table_name
    FROM sys.tables t
    JOIN sys.schemas s ON s.schema_id = t.schema_id
),
Columns AS (
    SELECT c.object_id,
           c.column_id,
           c.name AS column_name,
           TYPE_NAME(c.user_type_id) AS data_type,
           c.max_length,
           c.precision,
           c.scale,
           c.is_nullable,
           c.is_identity
    FROM sys.columns c
),
Indexes AS (
    SELECT i.object_id,
           i.index_id,
           i.name AS index_name,
           i.type_desc,
           i.is_primary_key,
           i.is_unique,
           STRING_AGG(COL_NAME(ic.object_id, ic.column_id), ',') WITHIN GROUP (ORDER BY ic.key_ordinal) AS index_columns
    FROM sys.indexes i
    JOIN sys.index_columns ic
      ON ic.object_id = i.object_id AND ic.index_id = i.index_id
    WHERE i.is_hypothetical = 0
      AND i.type > 0
    GROUP BY i.object_id, i.index_id, i.name, i.type_desc, i.is_primary_key, i.is_unique
),
ForeignKeys AS (
    SELECT fk.parent_object_id AS object_id,
           fk.name AS fk_name,
           OBJECT_NAME(fk.referenced_object_id) AS referenced_table,
           STRING_AGG(pc.name, ',') WITHIN GROUP (ORDER BY pc.column_id) AS parent_columns,
           STRING_AGG(rc.name, ',') WITHIN GROUP (ORDER BY rc.column_id) AS referenced_columns
    FROM sys.foreign_keys fk
    JOIN sys.foreign_key_columns fkc
      ON fkc.constraint_object_id = fk.object_id
    JOIN sys.columns pc
      ON pc.object_id = fkc.parent_object_id
     AND pc.column_id = fkc.parent_column_id
    JOIN sys.columns rc
      ON rc.object_id = fkc.referenced_object_id
     AND rc.column_id = fkc.referenced_column_id
    GROUP BY fk.parent_object_id, fk.name, fk.referenced_object_id
)
SELECT
    t.schema_name + '.' + t.table_name AS TableName,
    JSON_QUERY((
        SELECT
            t.schema_name      AS schema_name,
            t.table_name       AS table_name,
            (
                SELECT  c.column_name,
                        c.data_type,
                        c.max_length,
                        c.precision,
                        c.scale,
                        c.is_nullable,
                        c.is_identity
                FROM Columns c
                WHERE c.object_id = t.object_id
                ORDER BY c.column_id
                FOR JSON PATH
            ) AS columns,
            (
                SELECT  i.index_name,
                        i.type_desc,
                        i.is_primary_key,
                        i.is_unique,
                        i.index_columns
                FROM Indexes i
                WHERE i.object_id = t.object_id
                FOR JSON PATH
            ) AS indexes,
            (
                SELECT  fk.fk_name,
                        fk.referenced_table,
                        fk.parent_columns,
                        fk.referenced_columns
                FROM ForeignKeys fk
                WHERE fk.object_id = t.object_id
                FOR JSON PATH
            ) AS foreign_keys
        FOR JSON PATH, WITHOUT_ARRAY_WRAPPER
    )) AS TableMetadataJson
FROM Tables t
ORDER BY t.schema_name, t.table_name;
