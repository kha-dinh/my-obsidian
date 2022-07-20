# xspace
For some reason, Latex's default behavior for defining commands is to "eat" up the space right after. For example, the command defined by `\newcommand{\thename}{MyName}` would be joined with the next word when used (e.g., `\thename is X` -> `MyNameis X`). 

# Table related
## tabularx
tabularx is a drop-in replacement for the default tabular package. It allows (1) defining fixed table width and (2) defining new flexible column types (e.g., "X" type) that  takes up the remaining space available.

## booktabs
booktabs overwrite the default latex tables. It just looks better.

# makecell
makecell allows customized formating of individual table cells. It also provides useful commands for formating table headings (`\thead{}`)   

# multicolumn & multirow