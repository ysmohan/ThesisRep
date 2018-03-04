---
layout: page
title: LaTeX
subtitle: LaTeX document and project structure
minutes: 
---

> ## Learning Objectives {.objectives}
>
> * Understand the parts of a LaTeX document.
> * Be able to make a title.
> * Be able to use sectioning commands.
> * Be able to generate a table of contents.
> * Understand the difference between "starred" and "unstarred" sectioning commands.
> * Be able to insert other text files into a LaTeX document.
> * Understand the difference between inputting and including files.
> * Understand the different parts of LaTeX output.

We will now have a look at the basic structure required to set up any LaTeX project.

We've seen that every LaTeX document can be thought of as having two parts:

* Preamble
* Body

Recall that the preamble is where we tell LaTeX what sort of document we're writing, 
and which non-default resources we'd like to use.
It is also a good place to customise the way we use LaTeX.
For example, we can define our own command words,
or modify the behaviour of existing command words.

Titles
----

Let's look at how to add a title.
It is possible to write a title page from scratch, and this is the only way to
do it if there is a particular style you want to achieve.
However, for most cases it is possible to use much simpler built-in commands.

This needs to be done in two steps.
First in the preamble we specify some fields using the
`\title`, `\author` and `\date` command words.
All these fields are optional.
Then in the document body we use the `\maketitle` command word.

~~~ {.tex}
\documentclass{article}
\title{Hello World}
\author{J. Smith}
\begin{document}
\maketitle
% etc ...
~~~

A lot of the time when we generate an article,
we don't want the date in the title.
Let's suppress it by adding an empty date to the preamble:

~~~ {.tex}
\documentclass{article}
\title{Hello World}
\author{J. Smith}
\date{}
\begin{document}
\maketitle
% etc ...
~~~


Sectioning
----

Now we'll add a simple structure to our content from the previous lesson.

~~~ {.tex}
\documentclass{article}
\title{Hello World}
\author{J. Smith}
\date{}
\begin{document}
\maketitle

\section{Cat pictures}

Use a command provided by graphicx to add a picture:
\includegraphics{cat.jpg}

Use an option in square brackets to change the image width:
\includegraphics[width=0.9\textwidth]{cat.jpg}


\section{Lists}

An ordered list:
\begin{enumerate}
  \item The First
  \item The Second
\end{enumerate}

An unordered list:
\begin{itemize}
  \item Some point
  \item Another point
\end{itemize}
\end{document}
~~~

In all there are seven levels of sectioning, numbered from -1 through 5:

~~~ {.tex}
\part{}
\chapter{}
\section{}
\subsection{}
\subsubsection{}
\paragraph{}
\subparagraph{}
~~~

Only some of these section types are used regularly.
In practice, you really only need to know about `\section` and `\subsection`
for both articles and reports, and `\chapter` just for reports.

In the latest document, you might start to notice some aspects of formatting
that aren't to your taste.
For example, most people will find the text a bit small.
Also, the default LaTeX paper size is Letter,
whereas A4 is preferred by most people outside the United States.
So, change the top of the document to state:

~~~ {.tex}
\documentclass[12pt, a4paper]{article}
~~~


Table of contents
----

Now that we have a document structure in place,
we notice it's missing a table of contents.

Just underneath `\maketitle` command, before any sectioning commands,
add the following line:

~~~ {.tex}
\tableofcontents
~~~

This is a point where LaTeX has some behaviour that needs getting used to.
In particular, when first generating a table of contents,
you will need to compile your document *twice*.

This is because the LaTeX compiler first needs to look through the document to
collect the information required for a table of contents.
Once this information has been prepared,
the table of contents itself can be generated for inclusion at the correct place.

When generating a simple document, we don't always want to number our sections.
To suppress numbering, we can modify the standard sectioning
commands by using their "starred" version:

~~~ {.tex}
\section*{Cat pictures}
~~~

(The standard commands are sometimes called "unstarred".)


Splitting up a large document
----

There is a final aspect to structuring a document that is not strictly required,
but which will make it much easier to work with non-trivial documents.
This is to split a document over multiple files,
then tell the compiler to bundle them all together at the last minute.


