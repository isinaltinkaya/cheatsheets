# LaTeX



## Get an item list with (1) (2) etc in parentheses

```
\newlist{CustomItemList}{enumerate}{10}
\setlist[CustomItemList]{label*=(\arabic*)}

\begin{CustomItemList}
    \item something
    \item something
\end{CustomItemList}
```

