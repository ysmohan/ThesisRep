---
layout: page
title: LaTeX
subtitle: References and bibliographies
---

> ## Learning Objectives {.objectives}
>
> * Be able to use the \label, \ref and \pageref control words.
> * Be able to create simple footnotes.
> * Be able to generate a simple bibliography.
> * Be able to use BibTeX to maintain a more sophisticated bibliography.

Cross-References
----

It is fairly easy to internally cross-reference many parts of a LaTeX document.
For example,

~~~{.tex}
\documentclass[a4paper,12pt]{article}
\usepackage{graphicx}

\begin{document}

\section{A section of interest}
\label{sec:interesting}

\includegraphics{figures/cat.jpg}


\section{Odds and ends}

Recall in Section~\ref{sec:interesting} that there was a cat picture.

\end{document}
~~~

It is possible to cross-reference all sorts of things such as Figures and
Tables.


Bibliographies
----

There are various ways to include citations and bibliographies in a LaTeX document.


### Simple bibliographies

It is possible to generate simple bibliographies within LaTeX by combining three
elements:

* The `\cite` command within the document text where you want the citation to appear.
* The `thebibliography` environment to contain the list of references.
* The `\bibitem` command used within `thebibliography` to describe how each
  reference should appear.

An example document looks like so:

~~~{.tex}
\documentclass[12pt, a4paper]{article}

\begin{document}

Noether \cite{noether1918} developed a unified concept of conservation laws
which later became known as \emph{Noether's Theorem}.

Foucault \cite{foucault1977} argued that prisons developed not out of humanitarian interests
but in order to make the effects of torture more distributed, predictable and controllable.

\begin{thebibliography}{1}
    \bibitem{noether1918} Emmy Noether, \textit{Invariante Variationsprobleme}.
        Nachrichten von der Gesellschaft der Wissenschaften zu G{\"o}ttingen,
        mathematisch-physikalische Klasse, 1918.

    \bibitem{foucault1977} Michel Foucault,
        \textit{Discipline and punish: The birth of the prison},
        Vintage, 1977.
}
\end{document}
~~~

To know which citations go with which references, LaTeX will need to be run twice
on this document (although if you're using a program like TeXstudio then
it will probably do this for you).

This method has two advantages:

* The appearance of entries in the bibliography is fairly easy to control so
  long as you know how to do general text formating in LaTeX.
* It is built into LaTeX by default so it is very portable and can be used
  without needing to learn anything other than standard LateX.

It also has two disadvantages:

* The appearance is not suited to people in the humanities who often place
  references in footnotes rather than bibliographies.
* It becomes unwieldy for long lists of references.

To overcome these disadvantages, people usually keep a list of references in an
external file, then use citation commands in the LaTeX document to refer to them.

This adds some additional complexity:
LaTeX does not know about the external list of references by default.
Instead, it is now necessary to use another program in addition to LaTeX,
which assembles and links all the citations and references together.
There are two main alternatives for these LaTeX bibliography programs:

* [BibTeX](http://www.bibtex.org/).
* [Biber](http://www.bibtex.org/).

Fortunately, they both usually come packaged with LaTeX,
so you don't have to install anything extra.
Unfortunately, they are not compatbile with each other.

The choice will usually depend on which field you are in.
BibTeX is a solid traditional option, especially for people in the Sciences.
Biber is a newer program.
It has a number of advantages such as more flexible referencing styles,
and better internationalisation.
This often makes it better suited to writing for the Arts and Humanities,
although it can also be used in the Sciences.
However, for various reasons not all journals will accept Biber style bibliographies,
especially scientific journals.

For more information about the differences, there is a good
[summary on StackExchange](http://tex.stackexchange.com/a/25702).


### BibTeX

Let's first have a look at BibTeX.
First put the following in a file called `myreferences.bib`.

~~~ {.bib}
@article{noether1918,
    title={Invariante variationsprobleme},
    author={Noether, Emmy},
    journal={Nachrichten von der Gesellschaft der Wissenschaften zu G{\"o}ttingen, mathematisch-physikalische Klasse},
    volume={1918},
    pages={235--257},
    year={1918}
}

@book{foucault1977,
    title={Discipline and punish: The birth of the prison},
    author={Foucault, Michel},
    year={1977},
    publisher={Vintage}
}
~~~

Then change the main document to:

~~~ {.tex}
\documentclass[12pt, a4paper]{article}

\begin{document}

Noether \cite{noether1918} developed a unified concept of conservation laws
which later became known as \emph{Noether's Theorem}.

Foucault \cite{foucault1977} argued that prisons developed not out of humanitarian interests
but in order to make the effects of torture more distributed, predictable and controllable.

\bibliographystyle{plain}
\bibliography{myreferences}{}
\end{document}
~~~

To give BibTeX all the information it needs, and then to include information
from BibTeX back into LaTeX, we need to make a LaTeX-BibTeX sandwich:

1. Run LaTeX on `main.tex`.
2. Run BibTeX on `main.aux`.
3. Run LaTeX on `main.tex` again.

If things don't look right, try running steps one and three twice.

Again, front-end programs like TeXstudio will again
often know how to do all this automatically,
but it is useful to know about what is happening "under the hood".

In the above `myreferences.bib` file, we saw two citation types,
article and book, and both had a number of fields specified,
such as title and author.
There are more citation types than this, and each type has a number
of required and optional fields.
For more information about what is possible or required,
there is a good summary on [Wikipedia's BibTeX page](https://en.wikipedia.org/wiki/BibTeX).

To give more control over bibliographies when using BibTeX,
people will usually also use the [natbib package](https://www.ctan.org/pkg/natbib).
For example, try changing `main.tex` like so:

~~~{.tex}
\documentclass[12pt, a4paper]{article}
\usepackage[round]{natbib}

\begin{document}

Noether \citep{noether1918} developed a unified concept of conservation laws
which later became known as \emph{Noether's Theorem}.

\citet{foucault1977} argued that prisons developed not out of humanitarian interests
but in order to make the effects of torture more distributed, predictable and controllable.

\bibliographystyle{plainnat}
\bibliography{myreferences}
\end{document}
~~~

Notice that we have passed the optional argument of `round` when invoking
`natbib` to ensure the use of round brackets, and the use of `\citep` and
`\citet` instead of `\cite` to choose between parenthetical and textual citations.
For more information the
[natbib reference sheet](http://mirrors.ctan.org/macros/latex/contrib/natbib/natnotes.pdf)
is a good resource.


### Biber/BibLaTeX

Just as BibTeX is often used with natbib,
Biber is used with a package called BibLaTeX.

Compared to BibTeX and natbib, Biber and BibLaTeX are much more closely intertwined.
It is quite difficult to construct a small example to demonstrate
Biber without also using BibLaTeX.
So, in this section we will just proceed to use them together.

To use a Chicago-footnotes referencing style,
keep the above `myreferences.bib`,
but now change `main.tex` to:

~~~{.tex}
\documentclass[12pt, a4paper]{article}

\usepackage[notes, backend=biber]{biblatex-chicago}
\addbibresource{myreferences.bib}

\begin{document}
Noether developed a unified concept of conservation laws
which later became known as \emph{Noether's Theorem}\autocite{noether1918}.

Foucault argued that prisons developed not out of humanitarian interests
but in order to make the effects of torture more distributed, predictable and controllable
\autocite{foucault1977}.
\end{document}
~~~

The build process now goes like:

1. Run LaTeX on `main.tex`.
2. Run Biber on `main`.
3. Run LaTeX on `main.tex`.

If using a front-end like TeXstudio, you might need to
change some options which describe the build process.
