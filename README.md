# Page-Rank-Algorithm
Google Page-Rank Algorithm for sorting web pages
## Built on Jupyter notebook.

# Page Rank Algorithm
## Orders the popularity of web page search results
#### First we create a Model for a mini internet which is composed of 4 web pages; A, B, C and D.
#### The folowing graph illustrates our model:
[![pages.jpg](https://i.postimg.cc/6TJT6Yh5/pages.jpg)](https://postimg.cc/XBLnQKhT)
#### Each node denotes a webpage, each edge denotes a web link from one page to another.
### So page B conatins two links, one link to A and the other link to D.
#### We ignore any self referencing links.
#### We consider only direct links, such as A to D, but not A to B to D.

#### To determine the most popular page we set a random selection system.
#### So if a user starts at page A, randomly selects page B, then page A once more, we can represent this as a random page hop.
#### The porbability that a page is accessed at random is guaged and will give a measure of the pages popularity.
#### The links are described as a vector, each with a value of 1 for the presence of a link and 0 for absence of a link.
#### In order that the probability for a page hit we normalise the vectors.


[![linkvect.jpg](https://i.postimg.cc/pdhTjw1X/linkvect.jpg)](https://postimg.cc/GBRdw5CZ)

### Normalisation of the vectors involves division by the sum of the link vector elements.

[![znorm.jpg](https://i.postimg.cc/Y9RJC9f4/znorm.jpg)](https://postimg.cc/MMcsszLx)


## Python code:
```
#importing libraries
import numpy as np
import numpy.linalg as la
```
```
# Link Matrix
#Build Link Matrix

L = np.array([[0,   1/2, 0,  0   ],
              [1/3, 0,   0,  1/2 ],
              [1/3, 0,   0,  1/2 ],
              [1/3, 1/2, 1,  0 ]])
```

#### As an iteration loop will be administered then an initial vector will be required, where each element denotes it's probability of selection first. A network of four pages will give the probabilities for each page:
[![zprob.jpg](https://i.postimg.cc/tCnyZ2V9/zprob.jpg)](https://postimg.cc/RNm221RY)

```
# Initial vector r,
# Multiplied by 100 in order to gain percentage probabilty
r = 100*np.ones(4)/4   # Set the vector with 4 entries of 1/4 x100 each
r    
```
[![zrank.jpg](https://i.postimg.cc/RVhN9JQH/zrank.jpg)](https://postimg.cc/svFV4XLj)

```
# Performing the first iteration, multiply matrix L with vector r
r = L @ r  # applies link matrix to r
r #this is the rank vector after first iteration
```


[![zeig.jpg](https://i.postimg.cc/2Svj8QqV/zeig.jpg)](https://postimg.cc/QF8ZfWJ3)

```
# To update the value of r, keep repeating 
r = L @ r 
r
```

## While loop.
### Introduce a while loop to iterate 100 times
```
# We repeat using a loop
r=100*np.ones(4)/4
for i in np.arange(100):
    r=L@r
r
```
#### The final iteration of r denotes the probabilty of hitting each page during the 100 cloop experiment.
#### The user spends 12% in page A, 24% in page B and 24% in C, then 40% in D
```
# Best Probabilty:
round(np.max(r),2)
```
### Running the while loop until a a specific condition is met, such as a tolerance level
```
# We may run the code until a specific condition is met, such as tolerance
r =  100*np.ones(4)/4
lastR = r  #set to equal initial r
r = L@r
i = 0      # counting variable
while la.norm(lastR - r)> 0.01:
    lastR = r
    r = L@r
    i += 1
    print(r)
print(str(i)+" is number of iterations for convergence")
r
```
[![zresult.jpg](https://i.postimg.cc/N0CQdpSC/zresult.jpg)](https://postimg.cc/5Hvc0qx8)


# Full Python Code:
```
#importing libraries
import numpy as np
import numpy.linalg as la

# Link Matrix
#Build Link Matrix

L = np.array([[0,   1/2, 0,  0   ],
              [1/3, 0,   0,  1/2 ],
              [1/3, 0,   0,  1/2 ],
              [1/3, 1/2, 1,  0 ]])
              
# Initial vector r,
# Multiplied by 100 in order to gain percentage probabilty
r = 100*np.ones(4)/4   # Set the vector with 4 entries of 1/4 x100 each
r      

# Performing the first iteration, multiply matrix L with vector r
r = L @ r  # applies link matrix to r
r #this is the rank vector after first iteration

# To update the value of r, keep repeating 
r = L @ r 
r

# We repeat using a loop
r=100*np.ones(4)/4
for i in np.arange(100):
    r=L@r
r

# Best Probabilty:
round(np.max(r),2)

# We may run the code until a specific condition is met, such as tolerance
r =  100*np.ones(4)/4
lastR = r  #set to equal initial r
r = L@r
i = 0      # counting variable
while la.norm(lastR - r)> 0.01:
    lastR = r
    r = L@r
    i += 1
    print(r)
print(str(i)+" is number of iterations for convergence")
r



#######################################
#Lets take a new case with 6 pages

M = np.array([[0,   1/2, 1/3, 0, 0,    0 ],
              [1/3, 0,   0,   0, 1/2, 1/3],
              [1/3, 1/2, 0,   1, 0,   0 ],
              [1/3, 0,   1/3, 0, 1/2, 1/3 ],
              [0,   0,   0,   0, 0,   1/3 ],
              [0,   0,   1/3, 0, 0,   0 ]])
              
              
r=100*np.ones(6)/6
lastR = r
r =M@r
i =0
while la.norm(lastR - r)>0.01:
    lastR = r
    r= M@r
    i +=1
    print(r)
print(str(i) + "iterations for convergence to give vector r")
r

# A=17%, B=11%,C=34%,D=22%,E=4%,F=11%
m=round(max(r),1)
print("maximum % is "+str(m)+" %")

r[0:6] 

toppage=np.where(r==max(r))
top =str(toppage)
print("Page number {} with {}% hit pobability".format(top,m))


```

## Improvements
#### Develop the code to adapt to any number of pages.
