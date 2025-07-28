---
title: Resume
nav_order: 2
parent: Posts
---

# Resume Guide

Resume... no introduction needed. So let's get started.

> Keep one thing in mind, we make resumes for machines not for humans :)

## Keypoints to remember
- Never make resume on Canva. It's not ATS friendly. Always use word or overleaf(or any LaTex editor).
- Try to include numbers in every line. It increases ATS score.
- Bullet points should be small and plenty enough to not make your resume short or lengthy.
- Always start bullet points with strong action verbs.
- Highlight important points. 
- No spelling mistakes please.
- Always provide links, it acts as a proof.
- It should be of 1 page for freshers, and of 2 pages for experienced. 

## Where to make one ?
[Overleaf](https://www.overleaf.com/) is your friend in this case. There are plenty of templates available over there. But my favourite ones are: 
1. [Template 1](https://www.overleaf.com/latex/templates/jakes-resume/syzfjbzwjncs)
2. [Template 2](https://drive.google.com/file/d/1oabOopXNdkq-pqXLiByFckQHNvtk7Wxy/view)


## Some action verbs for reference :
![ActionVerbs](https://cdn-images.livecareer.co.uk/pages/action_words_for_cv_livecareer_uk_image.jpg)


### Resume Worded - Here you can check your ATS Score.
[Site](https://resumeworded.com/)

![ResumeWorded](https://resumeworded.com/assets/images/updated-homepage-sketch.png)


## Simple LaTex Format for resume

### Packages: 

```
\documentclass[letterpaper,11pt]{article}

\usepackage{ragged2e} % Required for \justify command
\usepackage{latexsym}
\usepackage[empty]{fullpage}
\usepackage{titlesec}
\usepackage{marvosym}
\usepackage[usenames,dvipsnames]{color}
\usepackage{verbatim}
\usepackage{enumitem}
% \usepackage[hidelinks]{hyperref}
\usepackage{hyperref}
\usepackage{fancyhdr}
\usepackage[english]{babel}
\usepackage{tabularx}
\usepackage{fontawesome5}
\usepackage{multicol}
\setlength{\multicolsep}{-3.0pt}
\setlength{\columnsep}{-1pt}
\input{glyphtounicode}


%----------FONT OPTIONS----------
% sans-serif
% \usepackage[sfdefault]{FiraSans}
% \usepackage[sfdefault]{roboto}
% \usepackage[sfdefault]{noto-sans}
% \usepackage[default]{sourcesanspro}

% serif
% \usepackage{CormorantGaramond}
% \usepackage{charter}


\pagestyle{fancy}
\fancyhf{} % clear all header and footer fields
\fancyfoot{}
\renewcommand{\headrulewidth}{0pt}
\renewcommand{\footrulewidth}{0pt}

% Adjust margins
\addtolength{\oddsidemargin}{-0.6in}
\addtolength{\evensidemargin}{-0.5in}
\addtolength{\textwidth}{1.19in}
\addtolength{\topmargin}{-.7in}
\addtolength{\textheight}{1.4in}

\urlstyle{same}

\raggedbottom
\raggedright
\setlength{\tabcolsep}{0in}

% Sections formatting
\titleformat{\section}{
  \vspace{-4pt}\scshape\raggedright\large\bfseries
}{}{0em}{}[\color{black}\titlerule \vspace{-5pt}]

% Ensure that generate pdf is machine readable/ATS parsable
\pdfgentounicode=1

%-------------------------
% Custom commands
\newcommand{\resumeItem}[1]{
  \item\small{
	{#1 \vspace{-2pt}}
  }
}

\newcommand{\classesList}[4]{
	\item\small{
    	{#1 #2 #3 #4 \vspace{-2pt}}
  }
}

\newcommand{\resumeSubheading}[4]{
  \vspace{-2pt}\item
	\begin{tabular*}{1.0\textwidth}[t]{l@{\extracolsep{\fill}}r}
  	\textbf{#1} & #2 \\
  	\textit{\small#3} & \textit{\small #4} \\
	\end{tabular*}\vspace{-7pt}
}

\newcommand{\resumeSubSubheading}[2]{
	\item
	\begin{tabular*}{0.97\textwidth}{l@{\extracolsep{\fill}}r}
  	\textit{\small#1} & \textit{\small #2} \\
	\end{tabular*}\vspace{-7pt}
}

\newcommand{\resumeProjectHeading}[2]{
	\item
	\begin{tabular*}{1.001\textwidth}{l@{\extracolsep{\fill}}r}
  	\small#1 & \textbf{}\\
	\end{tabular*}\vspace{-7pt}
}

\newcommand{\resumeSubItem}[1]{\resumeItem{#1}\vspace{-4pt}}

\renewcommand\labelitemi{$\vcenter{\hbox{\tiny$\bullet$}}$}
\renewcommand\labelitemii{$\vcenter{\hbox{\tiny$\bullet$}}$}

\newcommand{\resumeSubHeadingListStart}{\begin{itemize}[leftmargin=0.0in, label={}]}
\newcommand{\resumeSubHeadingListEnd}{\end{itemize}}
\newcommand{\resumeItemListStart}{\begin{itemize}}
\newcommand{\resumeItemListEnd}{\end{itemize}\vspace{-5pt}}

\hypersetup{
    colorlinks=true,
    linkcolor=blue,
    filecolor=blue,      
    urlcolor=blue,
}
```

### Main Content: 

```
\begin{document}

%----------HEADING----------

\begin{center}
    {\Huge \scshape Name} \\
    Location \\
    Contact Number  $|$ Email Id \\
    \href{github text}{github link} $|$
    \href{portfolio text/}{portfolio link} $|$
    \href{linkedin text}{linkedin link}
\end{center}

%-----------EDUCATION-----------
\section{Education}
  \resumeSubHeadingListStart
	\resumeSubheading
  	{College}{Start Year - End Year}
  	{Degree}{CGPA}
  \resumeSubHeadingListEnd

%-----------PROGRAMMING SKILLS-----------
\justify
\section{Skills Summary}
 \begin{itemize}[leftmargin=0.15in, label={}]
	\small{\item{
 	\textbf{Skill Title 1}{: Comma Separated skills} \\
 	\textbf{Skill Title 2}{: Comma Separated skills}
 \end{itemize}

% %-----------EXPERIENCE-----------
\justify
\section{Experience}
    \resumeSubHeadingListStart
	\resumeSubheading
  	{Company Name $|$ {\href{LoR link}{LoR}}}{Start Date - End Date}
  	{Position}{Location}
  	\resumeItemListStart
    	\resumeItem{First Bullet Point}
    	\resumeItem{Second Bullet Point}
	\resumeItemListEnd
  \resumeSubHeadingListEnd

%-----------PROJECTS-----------
\justify
\section{Projects}
\resumeSubHeadingListStart
    \resumeProjectHeading
        {\textbf{Project Name} $|$ \emph{Comma Separated Skills used}  $|$ {{\href{github link}{Github}}} $|$ {{\href{live link}{Live}}}}{}
        \resumeItemListStart
            \resumeItem{Bullet Point}
        \resumeItemListEnd
\resumeSubHeadingListEnd

%-----------Achievements-----------
\justify
\section{Achievements and Awards}
\resumeSubHeadingListStart
    \resumeItemListStart
        \resumeItem{Bullet Point}
    \resumeItemListEnd
\resumeSubHeadingListEnd
 
 %-----------Position Of Responsibility-----------
\justify
\section{Leadership \& Extracurricular}
    \resumeSubHeadingListStart
            \resumeItemListStart
                  \resumeItem{Bullet Point}
            \resumeItemListEnd
    \resumeSubHeadingListEnd
\end{document}

```