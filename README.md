# Sangblad

Cba using md correctly

### texmaker config någågågåg

One or more of the .tex documents uses fonts that require xetex or lualatex

## Roadmap i guess

1. Create custom build script (text file with song lyrics, title and corresponding melody(if exists) -> space optimised default formatted .tex chapter/section
2. If this is too difficult (big dumb dumb !) just streamline the process and write a .tex library to minimise boilerplate (grr)


# Using the dotnet sb (Sangblad) tool (under development)

## Song structure 

### Parsing

1. Using LaTeX minipages (good for space-conserving, slightly larger leaflets)

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

If you're using a two-column minipage setup, consider configuring a set minipage width:

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
  \textit{Mel: Melody 1}
\end{minipage}%
\hspace{.05\textwidth} //no empty lines between side-by-side minipages
\noindent
\begin{minipage}{.475\textwidth}
  \paragraph*{Title 2\\}
  \vspace{3px}
  \textit{Mel: Melody 2}
\end{minipage}

\noindent
\begin{minipage}{.475\textwidth} //obviously, the child pages need the same spacial configuration
  \noindent //This is up to you, I find it more pleasing having no indentation in song lyrics 
            //so before every paragraph I usually add this
  Line 1, Song 1\\ //newline
  Line 2, Song 1\\
                    //extra newline here so that TeX adds horizontal space between paragraph
  \noindent
  Line 3, Song 1\\
  Line 4, Song 1\\
  
  ...
\end{minipage}% <- next minipage is to be placed side-by-side with this one
\hspace{.05\textwidth}
\noindent
\begin{minipage}{.475\textwidth}
  \noindent
  ...
\end{minipage}

\newpage
\noindent
\begin{minipage}...
```

2. Using a standalone section (good for small-form books)

### Using a text file as input
