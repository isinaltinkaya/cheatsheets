# LaTeX

## Get the changes between versions highlighted
```
latexdiff-git SupplementaryMaterial_old.tex SupplementaryMaterial_new.tex > changes_SupplementaryMaterial.tex
```

## Get an item list with (1) (2) etc in parentheses

```
\newlist{CustomItemList}{enumerate}{10}
\setlist[CustomItemList]{label*=(\arabic*)}

\begin{CustomItemList}
    \item something
    \item something
\end{CustomItemList}
```

