# *Numeric Methods - Homework I*



## **Page Rank Algorithm - Google**

### ***General explanations about PageRank***

PageRank is an algorithm used by Google search engine to assign a score, known as the ***PageRank index***, to web pages based on their relative importance within a set of interconnected web pages. These algorithms work by analyzing hyperlinks between web pages and measuring the probability that a user would visit a particular page based on the ***number & quality of incoming links***. 

To calculate the PageRank index of a particular page, the algorithm considers the set of all pages that link to it directly/indirectly, and the number of links that each of these pages has. The probability of a user visiting a particular page is higher if the pages linking to it are more important and have a fewer outgoing links. Also, the probability is also affected by **damping factor**, which represents the probability that a user will continue surfing the web.

The formula that calculates the PageRank index of a a page takes into account the <ins>*PageRank indices of all pages linking to it, as well as the damping factor.*</ins> The higher the PageRank indices of the linking pages are, the higher the PageRank index of the page being analyzed. By assigning a score to each page based on its relative importance within the set of pages. PageRank algorithm helps search engines to prioritize the most relevant and authoritative pages for a specific query, making it easier for users to find the information they are looking for.

### ***PageRank algorithm***

To determine the importance of a specific web page, which will refer to as page *A*. We will identify the set of web pages that send us to page *A*, denoted as ***M(A)*** , that link to a page *A* with a single click. 

<ins>*Example*</ins>: if page *B, C, D* have a directly link to page *A*, then *M(A)* will include pages *B, C & D.*

Second step, look at the importance of the pages in set *M(A)*, which determines the number of incoming links they have, denoted as ***L(B), L\(C\) & L(D)*** for pages *B, C & D*. The higher the number of incoming links to a page is, the more important is considered to be. Therefore, let's say page *B* has more incoming links than *C* and *D*, which means it is considered more important.

The importance of *M(A)* is to calculate the probability that a user will visit page *A*. The probability ***PR(A)*** for users that will visit page *A* is affected by <ins>damping factor</ins>, represented by coefficient ***d***, which represents the probability that a user will continue browsing the web after visiting a page. This coefficient is normally set to **0.85**.

The formula to calculate the PageRank index for $\forall A$ pages: 

$$ PR(A) = \frac{1 - d}{N} + d \cdot \sum_{P \in M(A)} \frac{PR(P)}{L(P)} =
\frac{1 - d}{N} + d \cdot (\frac{PR(B)}{L(B)} + \frac{PR(C)}{L(C)} + \frac{PR(D)}{L(D)} + \cdots) $$

This formula takes into account the importance of each page in set *M(A)*, as represented by their PageRank indices ****(PR(B), PR(C*\) , PR(D), etc...)*** and the number of incoming links each of these pages has ***(L(B), L(C*\), L(D), etc...)**. The higher the PageRank indices of the linking pages and the fewer the number of incoming links, the higher the PageRank index of page *A* is.

### ***Task 1: Iterative algorithm***

Program takes N web resources and creates a graph with an adjacency list, displaying it in a file with N on the first line and lists of neighbors on the following lines. To complete the requirements, we construct the adjacency matrix of the graph and implement the iterative method of the PageRank program. 

The algorithm takes: <ins>**the file name, d parameter - damping factor and eps - tolerance as input and output is PR vector - list of all pages ranked**</ins>. The adjacency matrix of this graph is denoted by *A*, which respects specific proprieties: 

 - $A(i,j) = 0$ if node i is not adjacent with the node j, otherwise 1.
 - A web page contains at least one link to another web page. This means that matrix resulted from iterative algorithm is invertible.
 - Some pages will have a link to themselves, for easier navigation, so not all elements from main diagonal of matrix *A* are 0. In analysis, these links are meaningless, so they will not be counted. $A(i,i) = 0 \forall i \in [1,N]$ 

After reading the file, the code builds the matrix of initial links for each page, calculates the R factor, and initializes the PageRank vector with a value of *1/number of pages for each page*.

The function then enters a while loop, which calculates the PageRank vector for each page using the formula: 

$$ PageRank = d \cdot L_0 \cdot PR_0 + ((1 - d) ./ N)  \cdot L $$ 

 - $L$ is the matrix of initial links for each page
 - $PR_0$ is the previous value of the PageRank vector,
 - $d$ is the damping factor
 - $N$ is the number of pages
 - $L$ is a column vector with 1s.

The loop continues until the difference between the current and previous PageRank vectors is less than the tolerance specified by the $eps$ parameter. Finally, the function returns the PageRank vector for each page. Overall, the code implements the Iterative PageRank algorithm to calculate the PageRank vector for a given hyperlinks matrix.

### ***Task 2: Algebraic algorithm***

To implement the Algebraic algorithm, the function needs to build the hyperlink matrix, calculate the stochastic matrix, and use the power iteration method to compute the PageRank vector.

In addition, the Gram-Schmidt algorithm will be used to compute the inverse of the matrix. To do so, the function needs to solve the system of equations, for each line separately, using the optimized Gram-Schmidt algorithm.

To calculate the inverse of a matrix, the Gram-Schmidt algorithm will be used: let $T$ be an invertible matrix <u>(with n rows and n columns)</u> for which **$T ^{-1}$** is required to be determined.

**The optimized Gram-Schmidt** algorithm will be used to find Q and R matrices such that:

$$ T = Q · R \newline T =  [t_1, t_2,  \cdots  t_n],  \space T^{-1}  =  [x_1, x_2, \cdots  x_n]  \newline T · [x_1, x_2  \cdots  x_n] = [e_1, e_2  \cdots e_n], \space \space \space T ·  x_i =  e_i $$

Based on the Q and R matrices, the function will then solve the n systems of equations.
Overall, the Algebraic function will calculate the PageRank vector using the hyperlinks matrix and the damping factor, and use the Gram-Schmidt algorithm to compute the inverse of the matrix.
