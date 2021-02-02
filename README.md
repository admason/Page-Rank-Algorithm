# Page-Rank-Algorithm
Google Page-Rank Algorithm for sorting web pages

# Page Rank Algorithm
## Orders the popularity of web page search results
### First we create a Model for a mini internet which is composed of 4 web pages; A, B, C and D.
### The folowing graph illustrates our model:
![image.png](attachment:image.png)
### Each node denotes a webpage, each edge denotes a web link from one page to another.
### So page B conatins two links, one link to A and the other link to D.
### We ignore any self referencing links.
### We consider only direct links, such as A to D, but not A to B to D.

#### To determine the most popular page we set a random selection system.
#### So if a user starts at page A, randomly selects page B, then page A once more, we can represent this as a random page hop.
#### The porbability that a page is accessed at random is guaged and will give a measure of the pages popularity.
#### The links are described as a vector, each with a value of 1 for the presence of a link and 0 for absence of a link.
#### In order that the probability for a page hit we normalise the vectors.

## Link vectors:
### Link vector A
$L_{A}= \begin{bmatrix}
0 & 1 & 1 & 1\\
\end{bmatrix}$
#### Whereby page A has a link to B, C and D.

### Link vector B
$L_{B}= \begin{bmatrix}
1 & 0 & 0 & 1\\
\end{bmatrix}$
#### Whereby page B has a link to A and D.

### Link vectors C and D
$L_{C}= \begin{bmatrix}
0 & 0 & 0 & 1\\
\end{bmatrix}
\\
L_{D}= \begin{bmatrix}
0 & 1 & 1 & 0\\
\end{bmatrix}$

### Normalisation of the vectors involves divion by the sum of the element.
$L_{A}= \begin{bmatrix}
0 & 1 & 1 & 1\\
\end{bmatrix}  =  \begin{bmatrix}
0 & \frac{1}{3} & \frac{1}{3} & \frac{1}{3}\\
\end{bmatrix}
\\
L_{B}= \begin{bmatrix}
1 & 0 & 0 & 1\\
\end{bmatrix}  =\begin{bmatrix} \frac{1}{2} & 0 & 0 & \frac{1}{2}\\
\end{bmatrix}
\\
L_{C}= \begin{bmatrix}
0 & 0 & 0 & 1\\
\end{bmatrix}  =\begin{bmatrix}0 & 0 & 0 & 1\\
\end{bmatrix}
\\
L_{D}= \begin{bmatrix}
0 & 1 & 1 & 0\\
\end{bmatrix}=\begin{bmatrix}0 & \frac{1}{2} & \frac{1}{2} & 0\\
\end{bmatrix}$
\\
#### The normalised vectors are then placed as column in Link matrix:
#### The link matrix L=  $\begin{bmatrix}
0 & \frac{1}{2} & 0 & 0\\
\frac{1}{3} & 0 & 0 & \frac{1}{2}\\
\frac{1}{3} & 0 & 0 & \frac{1}{2}\\
\frac{1}{3} & \frac{1}{2} & 1 & 0\\
\end{bmatrix}$
