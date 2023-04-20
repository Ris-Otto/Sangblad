# Sangblad

Cba using md correctly

### texmaker config någågågåg

One or more of the .tex documents uses fonts that require xetex or lualatex

## Roadmap i guess

1. Create custom build script (text file with song lyrics, title and corresponding melody(if exists) -> space optimised default formatted .tex chapter/section
2. If this is too difficult (big dumb dumb !) just streamline the process and write a .tex library to minimise boilerplate (grr)


# Using the dotnet `sb` (Sangblad) tool (under development)

## Song structure 

### Parsing

1. Using **LaTeX minipages** (good for space-conserving, slightly larger leaflets)

Basic structure of song using minipages is:

A minipage containing the song header:

```
\begin{minipage}
  \paragraph*{Title\\}
  \vspace{3px} //Tiny vertical space between title and melody
  \textit{Mel: Melody}
\end{minipage}
```


Followed by either a minipage containing the song lyrics **OR** another minipage header positioned side-by-side.

To mark that a second minipage should be placed side-by-side with the first one, append a '%' after `\end{minipage}`:

```
...
\end{minipage}% <- TeX understands this as 'side-by-side', don't ask me how or why
```

If you're using a **two-column minipage setup**, consider configuring a set minipage width:

```
\begin{minipage}{.475\textwidth} //.475 of page is my preferred width, so that we can add \hspace{.05\textwidth} 
                                 //between the two minipages
  ...
\end{minipage}%
\hspace{.05\textwidth}
\noindent %\noindent seems to be common practice for minipages, given that a minipage is followed by another
```

Given these structural specifications, a full two column minipage page might look like this:

```
\newpage
\noindent
\begin{minipage}{.475\textwidth}
  \paragraph*{Title 1\\}
  \vspace{3px}
  \textit{Mel: Melody 1}\\
\end{minipage}%
\hspace{.05\textwidth}
\noindent
\begin{minipage}{.475\textwidth}
  \paragraph*{Title 2\\}
  \vspace{3px}
  \textit{Mel: Melody 2}\\
\end{minipage}

\noindent
\begin{minipage}{.475\textwidth} 
  \noindent 
  Line 1, Song 1\\ 
  Line 2, Song 1\\
                   
  \noindent
  Line 3, Song 1\\
  Line 4, Song 1\\
\end{minipage}%
\hspace{.05\textwidth}
\noindent
\begin{minipage}{.475\textwidth}
  \noindent
  \noindent 
  Line 1, Song 2\\ 
  Line 2, Song 2\\
                   
  \noindent
  Line 3, Song 2\\
  Line 4, Song 2\\
\end{minipage}
```

Finally, if a two-column setup is present and the two songs have lyrics of different length you might need

to add some \vspace to one side or the other so that they're properly aligned. This will eventually be done programmatically

if you're using the `sb` cli tool.

2. Using a **standalone section** (good for small-form books)

This is far more straightforward and as it stands (20.04.2023) now they're essentially parsed as

  - \section*{This contains the song title}
  - \paragraph*{This contains the author/composer}
  - Anything after the paragraph is treated as simple lyrics, and this part follows the same rules that the minipage lyrics did

At some point I will add support for song melody but I have mostly used this format for songs that are written as they were composed,

inserting the song score on the following page.



### Using a text file as input

(Under development)
