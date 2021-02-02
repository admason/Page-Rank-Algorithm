# Page-Rank-Algorithm
Google Page-Rank Algorithm for sorting web pages
Page Rank Algorithm
Orders the popularity of web page search results
First we create a Model for a mini internet which is composed of 4 web pages; A, B, C and D.
The folowing graph illustrates our model:
image.png

Each node denotes a webpage, each edge denotes a web link from one page to another.
So page B conatins two links, one link to A and the other link to D.
We ignore any self referencing links.
We consider only direct links, such as A to D, but not A to B to D.
To determine the most popular page we set a random selection system.
So if a user starts at page A, randomly selects page B, then page A once more, we can represent this as a random page hop.
The porbability that a page is accessed at random is guaged and will give a measure of the pages popularity.
The links are described as a vector, each with a value of 1 for the presence of a link and 0 for absence of a link.
In order that the probability for a page hit we normalise the vectors.
Link vectors:
Link vector A
𝐿𝐴=[0111] 
Whereby page A has a link to B, C and D.
Link vector B
𝐿𝐵=[1001] 
Whereby page B has a link to A and D.
Link vectors C and D
𝐿𝐶=[0001]𝐿𝐷=[0110] 
Normalisation of the vectors involves divion by the sum of the element.
𝐿𝐴=[0111]=[0131313]𝐿𝐵=[1001]=[120012]𝐿𝐶=[0001]=[0001]𝐿𝐷=[0110]=[012120]  \

The normalised vectors are then placed as column in Link matrix:
The link matrix L=  01313131200120001012120 
