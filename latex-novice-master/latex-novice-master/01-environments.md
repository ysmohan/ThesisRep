---
layout: page
title: LaTeX
subtitle: Environments and packages
minutes: 
---

> ## Learning Objectives {.objectives}
>
> * Understand how to begin and end an environment.
> * Be able to invoke a package.
> * Be able to include figures.
> * Be able to generate bullet points and enumerated lists.
> * Be able to enter verbatim text.
> * Understand the concept of floats.
> * Be able to create simple tables.

Images
----

We'll start with a simple LaTeX document that only shows the following image:

![cat](fig/cat.jpg)

Put the following in a LaTeX file called `main.tex`:

~~~ {.tex}
\documentclass{article}

% Tell LaTeX about image types like JPEG.
\usepackage{graphicx}

% End of preamble. Now add content.
\begin{document}

Use a command provided by graphicx to add a picture:
\includegraphics{cat.jpg}

\end{document}
~~~

We can see there are words beginning with back-slashes,
and words inside curly brackets.

The words with back-slashes in front are called *control words*.
Control words are used to issue commands to LaTeX.
Control words don't usually appear in the final document.
Instead they modify the appearance of the final document in some way.

Many control words have fairly general uses and need to be told the specific
way you want to use them.
This is what the curly brackets are for.
After the control word, put curly brackets,
and inside the curly brackets provide an argument.
(There are other uses for curly brackets in LaTeX but you don't need to worry
about them at first.)

For example, LaTeX doesn't know about graphics by default.
Without `\usepackage{graphicx}` we wouldn't be able to
include and manipulate graphics in our document.

Also note how the document content (at this stage just an image)
appears between a `\begin{document}` and an `\end{document}`.
Every LaTeX project needs `\begin{document}` and `\end{document}`.
(See what happens if you try making a LaTeX document without them.)

Everything before `\begin{document}` is called the preamble.
The preamble consists of control words that set up the overall appearance
for your document.
The only thing required in the preamble is `\documentclass{}`.
There are five built-in document classes,
and many more available through packages.

The only document classes we'll look at are `article` and `report`.
The reason for this is that they are both built-in,
and they are both the most likely classes you'll want to use LaTeX for.
The `article` class is good for journals, and `report` is good for theses.

Some of the other popular document classes are these
days often better off not done in LaTeX.
For example, you might hear about
[Beamer](https://bitbucket.org/rivanvx/beamer/wiki/Home)
as a way to make slides for presentations.
However, unless you're doing a very mathematical talk,
all the cool people are now using
[`reveal.js`](https://github.com/hakimel/reveal.js).
Even with mathematics, you should be able to use
[MathJax](https://www.mathjax.org) with `reveal.js`.

Anyway, we have a document with an image.
For many command words, we can provide additional options in square brackets.
Let's change the image size:

~~~ {.tex}
\includegraphics[width=0.9\textwidth]{cat.jpg}
~~~

Note use of `\textwidth`. Lots of other units exist.
It's best to use units that are defined relative to your document's settings,
such as `em`, `ex`, `\textheight`, and `\baselineskip`.
(There is an image in
[The Not So Short Introduction to LaTeX](https://tobi.oetiker.ch/lshort/lshort.pdf) 
that summarises many relative units of length.)
If you really need absolute measurements, you can also use units like `pt` and `mm`.


Lists
----

~~~ {.tex}
\documentclass{article}
\begin{document}
Ordered:
\begin{enumerate}
  \item The First
  \item The Second
\end{enumerate}

Unordered:
\begin{itemize}
  \item Some point
  \item Another point
\end{itemize}
\end{document}
~~~

