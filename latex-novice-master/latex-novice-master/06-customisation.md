---
layout: page
title: LaTeX
subtitle: Customisation and layout
minutes: 
---

> ## Learning Objectives {.objectives}
>
> * Understand the different document classes.
> * Be able to define or redefine commands.
> * Understand the different page styles and how to switch between them.
> * Understand page layout and be able to set lengths.
> * Understand counters and how to change and display them.
> * Be able to customise the appearance of chapters, sections, etc.


Change numbering style of an ordered list:

~~~ {.tex}
\renewcommand{\theenumi}{\roman{enumi}}
\renewcommand{\labelitemi}{***}
~~~

Note use of `\renewcommand`.
Not necessary for basic LaTeX usage but often necessary for customisation.

There are also packages that can assist with changing enumeration styles but
they're not really necessary unless you want to easily change styles throughout
a document instead of maintaining consistency.

