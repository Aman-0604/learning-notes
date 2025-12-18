DECLARE @TableName sysname = N'Loan';  -- change to your table

DECLARE @ObjectId int = OBJECT_ID(@TableName);

SELECT JSON_QUERY((
    SELECT
        OBJECT_SCHEMA_NAME(@ObjectId) AS schema_name,
        OBJECT_NAME(@ObjectId)        AS table_name,

        -- columns
        (
            SELECT  c.name                               AS column_name,
                    TYPE_NAME(c.user_type_id)            AS data_type,
                    c.max_length,
                    c.precision,
                    c.scale,
                    c.is_nullable,
                    c.is_identity
            FROM sys.columns c
            WHERE c.object_id = @ObjectId
            ORDER BY c.column_id
            FOR JSON PATH
        ) AS columns,

        -- indexes
        (
            SELECT  i.name           AS index_name,
                    i.type_desc,
                    i.is_primary_key,
                    i.is_unique,
                    STUFF((
                        SELECT ',' + COL_NAME(ic.object_id, ic.column_id)
                        FROM sys.index_columns ic
                        WHERE ic.object_id = i.object_id
                          AND ic.index_id  = i.index_id
                        ORDER BY ic.key_ordinal
                        FOR XML PATH(''), TYPE
                    ).value('.', 'nvarchar(max)'),1,1,'') AS index_columns
            FROM sys.indexes i
            WHERE i.object_id = @ObjectId
              AND i.is_hypothetical = 0
              AND i.type > 0
            FOR JSON PATH
        ) AS indexes,

        -- foreign keys
        (
            SELECT  fk.name AS fk_name,
                    OBJECT_NAME(fk.referenced_object_id) AS referenced_table,
                    STUFF((
                        SELECT ',' + pc.name
                        FROM sys.foreign_key_columns fkc2
                        JOIN sys.columns pc
                          ON pc.object_id = fkc2.parent_object_id
                         AND pc.column_id = fkc2.parent_column_id
                        WHERE fkc2.constraint_object_id = fk.object_id
                        FOR XML PATH(''), TYPE
                    ).value('.', 'nvarchar(max)'),1,1,'') AS parent_columns,
                    STUFF((
                        SELECT ',' + rc.name
                        FROM sys.foreign_key_columns fkc3
                        JOIN sys.columns rc
                          ON rc.object_id = fkc3.referenced_object_id
                         AND rc.column_id = fkc3.referenced_column_id
                        WHERE fkc3.constraint_object_id = fk.object_id
                        FOR XML PATH(''), TYPE
                    ).value('.', 'nvarchar(max)'),1,1,'') AS referenced_columns
            FROM sys.foreign_keys fk
            WHERE fk.parent_object_id = @ObjectId
            FOR JSON PATH
        ) AS foreign_keys

    FOR JSON PATH, WITHOUT_ARRAY_WRAPPER
)) AS TableMetadataJson;
