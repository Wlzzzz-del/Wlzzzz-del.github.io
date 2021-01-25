---
title: latex算法编辑
date: 2020-10-19 12:55:15
tags: 学习
---
因为要写论文，不得不开始学习latex。我感觉写这个比写代码还要难受哈哈哈
```
\def\SetClass{article}
\documentclass{\SetClass}
\usepackage[lined,boxed,commentsnumbered]{algorithm2e}\begin{document}
\begin{algorithm}[H]
\SetAlgoLined
\KwData{$G(V,E)$,$k$}
\KwResult{K-degree anonymity sequences $d^*$ }
get degree sequence of G\;
sort the degree sequence\;
put the first $k$ nodes into a group $g$\;
count $d_{average}(g)$\;
set $d(n_{g})=d_{average}(g)$\;
\While{until every node get the group}
{    
    count $C_{merge} = (d(a)-d_{k+1})+I(d[k+2,2k+1])$\;
    count $C_{new} = I(d[k+1,2k])$\;
    \eIf {$C_{merge}>C_{new}$}
    {put nodes from $n_{k+1}$ to $n_{2k}$ into new group $g`$\;}
    {pass\;}
    \eIf {$C_{merge}<C_{new}$}
    {put $n_{k+1}$ into group $g$}
    {pass\;}
    
}  \caption{greedy partition\label{IR}}\end{algorithm}




\begin{algorithm}[H]  
\SetAlgoLined  
\KwData{original graph $G=(V,E)$, K-degree anonymity sequences $d^*$ , original degree anonymity $d$}  
\KwResult{K-degree anonymity graph $G^*=(V^*,E^*)$ }
\While{True}
{
sort ($d^*$)\;
pick node $v_{i}= d^*_{max}$\;
pick randomly node $v_{j}$, $v_{j}$ in $d^*$ \;
\eIf{
$d_{v_{i}}<d^*_{v_{i}}$ and $d_{v_{j}}<d^*_{v_{j}}$
}
{
\eIf{
${\exists}$$e_{v_{i},v_{j}}$}{pick randomly two nodes $v_{p},v_{q}$\
(${\exists}e_{v_{p},v_{q}}$ and ($v_{p},v_{q}{\notin}neighbor(v_{i})$),($v_{p},v_{q}{\notin}neighbor(v_{j})))$}
{add $e_{v_{i},v_{j}}$\;continue;}}{pass}\
\eIf{$d_{v_{i}}>d^*_{v_{i}}$ and $d_{v_{j}}>d^*_{v_{j}}$}{
\eIf{${\exists}$$e_{v_{i},v_{j}}$
}
{
delete $e_{v_{i},v_{j}}$;
}
{
pick randomly two nodes $v_{p},v_{q}$\
(${\exists}e_{v_{p},v_{q}}$ and ($v_{p},v_{q}{\in}neighbor(v_{i})$),($v_{p},v_{q}{\in}neighbor(v_{j})))$\;delete $e_{v_{i},v_{p}}$\;delete $e_{v_{j},v_{q}}$\;add $e_{v_{p},v_{q}}$\;continue;
}
}
{pass}
\eIf{
$d_{v_{i}}>d^*_{v_{i}}$ and $d_{v_{j}}<d^*_{v_{j}}$
}
{
pick randomly one node $v_{p}$(${\exists}$$e_{v_{i},v_{p}}$ and $v_{p} \notin neighbor(v_{j})$)\;delete $e_{v_{i},v_{p}}$\;add $e_{v_{j},v_{p}}$\;continue;}{pass}}

\caption{Graph modification algorithm}
\end{algorithm}


\end{document}
```
![贪婪算法](https://i.loli.net/2020/10/19/ljgm12ziyMhcfqO.png)
![图修改算法](https://i.loli.net/2020/10/19/Ww6a4OKCnTDdoBQ.png)
