---

layout: post
title: "An Introduction to R for Network Analysis."
author: "Mario H. Gonzalez-Sauri"
date: "2023-09-14"

---


# Introduction

This guide is divided into two parts. The first part provides a basic
introduction to the R programming language, while the second part
focuses on practical code snippets for creating network visualizations,
generating statistics and performing analysis using the igraph package.

# Section 1: An introduction to R.

## Getting Started with R

To become proficient in R, it’s helpful to think of coding in a way
similar to learning a language. Start with the fundamentals, which are
the basic operators. Operators are symbols that instruct the computer to
perform specific actions. For example, in `1 + 2`, the `+` operator
performs addition. In `a <- 1:5`, the `<-` operator assigns values.
Begin by familiarizing yourself with these operators; you don’t need to
memorize them all at once. Focus on the ones you encounter frequently,
and gradually expand your knowledge.

### Key Concepts

As you gain confidence with operators, move on to writing your own code
snippets. To do this effectively, understand the fundamental rules of R:

- **R is Case Sensitive**: Pay attention to letter case; uppercase and
  lowercase letters are treated differently.
- **R Executes Code Sequentially**: R processes code from top to bottom,
  so the order of your commands matters.
- **R Reads Left to Right**: Code is evaluated from left to right, so
  the sequence of operations is crucial.

Learn about essential data structures like vectors, matrices, data
frames, lists, and arrays, and how to manipulate them. For example,
`2 + 1L` may not be a valid operation, but you can learn how to make it
valid. Understanding object classes and subsetting data within objects
is crucial.

### Learning by Doing

The best way to learn is by doing. When you have a clear, step-by-step
plan in mind, there’s likely a way to code it in R.

## Mastering R-base

Familiarize yourself with the R-base, which comprises core functions
that don’t require additional packages. This forms the foundation of
your knowledge. New users often make the mistake of installing numerous
unnecessary packages. Keep it simple and use additional packages like
`igraph` for specialized tasks, such as network analysis, only when
necessary.

### Operators Reference

Operators are symbols that provide instructions to the computer for
specific tasks, such as variable manipulation, statement evaluation,
function creation, and general operations. You can find a comprehensive
list of operators in the [R
documentation](https://cran.r-project.org/doc/manuals/r-devel/R-lang.html#Operators).

|      | Logical Operators                                             |
|:-----|:--------------------------------------------------------------|
| \-   | Minus, can be unary or binary                                 |
| \+   | Plus, can be unary or binary                                  |
| !    | Logical not (Negation)                                        |
| ~    | Tilde (used in model formulae)                                |
| ?    | Help                                                          |
| :    | Sequence, binary (in model formulae: interaction)             |
| \*   | Multiplication, binary                                        |
| /    | Division, binary                                              |
| ^    | Exponentiation, binary                                        |
| %x%  | Special binary operators, x can be replaced by any valid name |
| %%   | Modulus, binary                                               |
| %/%  | Integer divide, binary                                        |
| %\*% | Matrix product, binary                                        |
| %o%  | Outer product, binary                                         |
| %x%  | Kronecker product, binary                                     |
| %in% | Matching operator, binary (in model formulae: nesting)        |
| \<   | Less than, binary                                             |
| \>   | Greater than, binary                                          |
| ==   | Equal to, binary                                              |
| \>=  | Greater than or equal to, binary                              |
| \<=  | Less than or equal to, binary                                 |
| &    | And, binary, vectorized                                       |
| &&   | And, binary, not vectorized                                   |
| \|   | Or, binary, vectorized                                        |
| \|\| | Or, binary, not vectorized                                    |
| \<-  | Left assignment, binary                                       |
| -\>  | Right assignment, binary                                      |
| \$   | List subset, binary                                           |

R Operators

Understanding the basic syntax and notation in R is crucial to
effectively navigate and utilize the language. In this example, we’ll
explore the importance of this understanding while demonstrating the use
of operators for algebraic and logical operations.

We can use various operators in R to perform fundamental algebraic and
logical operations. It’s essential to be familiar with the basic syntax
of the language, including elements like semicolons and parentheses.

``` r
1 + 5       # Addition
```

    ## [1] 6

``` r
5 * 6       # Multiplication
```

    ## [1] 30

``` r
4 ^ -1      # Exponentiation
```

    ## [1] 0.25

``` r
3 / 2       # Division
```

    ## [1] 1.5

``` r
4 / (6 * 6) * (2 - 4)  # Complex arithmetic expression
```

    ## [1] -0.2222222

``` r
# Integer division
6 %/% 4
```

    ## [1] 1

``` r
# Returns the remainder
6 %% 4
```

    ## [1] 2

``` r
4:7         # Create a sequence of numbers
```

    ## [1] 4 5 6 7

``` r
# Logical Statements

(TRUE == FALSE) == FALSE
```

    ## [1] TRUE

``` r
(F == F) == T
```

    ## [1] TRUE

``` r
4 > 5
```

    ## [1] FALSE

``` r
7 < 2
```

    ## [1] FALSE

``` r
(6 * 7) == (7 * 6)
```

    ## [1] TRUE

``` r
c(2, 3) == c(3, 2)
```

    ## [1] FALSE FALSE

``` r
c(3, 2) == c(3, 2)
```

    ## [1] TRUE TRUE

``` r
(3 + 2) & (2 + 3) == 5
```

    ## [1] TRUE

``` r
# Using |
vector1 <- c(TRUE, FALSE, TRUE)
vector2 <- c(FALSE, TRUE, TRUE)

# Element-wise logical OR using |
result1 <- vector1 | vector2

# Using in
c(2, 3) %in% c(2, 4, 3)
```

    ## [1] TRUE TRUE

## Understanding Objects in R Programming

R is a powerful programming language known for its object-based
approach. In practical terms, this means that every piece of data in R,
apart from operators and syntax, is treated as an object with specific
attributes. These attributes include class, structure, typeof, length,
dimension, and structure. To effectively work with R, it’s crucial to
grasp the fundamental concept of objects and how they function within
the language. Let’s dive into some of the foundational aspects of
objects in R.

### Vectors: The Building Blocks

In R, vectors are the fundamental building blocks of data. They are
often referred to as atomic vectors because they can hold elements of a
single data type. Here are some key points about vectors:

Empty Vectors: You can create empty vectors using the NULL keyword.

``` r
z <- NULL
```

Numeric Vectors: Numeric vectors store numerical values, and you can
assign names to elements within a vector. R

``` r
a <- c('a' = 2.3, 'b' = 4)
```

Integers: R also supports integer vectors, which can be created using
the L suffix.

``` r
b <- c(2L, 9L)
```

Logical Vectors: Logical vectors store TRUE and FALSE values.

``` r
d <- c(TRUE, FALSE)
```

Character Vectors: Character vectors hold text or character data.

``` r
e <- c("A", 'B')
```

Factor: Factors are used to represent categorical variables. They have
levels and can be ordered or unordered.

``` r
f <- factor(1:2, levels = c('male', "female"))
```

Operations on Vectors: You can perform various operations on vectors,
such as addition, multiplication, and more. Vectors are the foundation
for more complex data structures in R, and understanding their
properties and manipulation is essential.

``` r
4 * a
```

    ##    a    b 
    ##  9.2 16.0

``` r
(a) ^ -1
```

    ##         a         b 
    ## 0.4347826 0.2500000

``` r
a1 <- c(4, 7)
names(a1) <- c('a', 'b')

a + a1
```

    ##    a    b 
    ##  6.3 11.0

Stay tuned as we explore more about matrices, data frames, functions,
and lists in the world of R programming. These concepts will further
enhance your ability to work with data effectively in R.

### Matrices

Matrices are 2-dimensional arrays of data consisting of a single atomic
object. They are essential for conducting statistical analyses and
algorithms that involve mathematical manipulations. One crucial aspect
of matrices is that their type is determined by a single atomic object.

Let’s create a matrix with numeric vector elements and examine its type
using the `typeof` function:

``` r
# Matrices
# Basic
A <- matrix(1:9, ncol = 3, byrow = TRUE)
class(A)
```

    ## [1] "matrix" "array"

``` r
typeof(A)
```

    ## [1] "integer"

``` r
# Add a column with character elements
Z <- matrix(c(1:9, LETTERS[1:3]), ncol = 4, byrow = TRUE)
class(Z)
```

    ## [1] "matrix" "array"

``` r
typeof(Z)
```

    ## [1] "character"

``` r
# Math operators don't work.
Z + Z
```

    ## Error in Z + Z: argumento no-numérico para operador binario

``` r
# Change the elements of the matrix
A[upper.tri(A)] <- 1
A[lower.tri(A)] <- 2
diag(A) <- 3
A
```

    ##      [,1] [,2] [,3]
    ## [1,]    3    1    1
    ## [2,]    2    3    1
    ## [3,]    2    2    3

``` r
# Combining vectors by column
B <- cbind(2:0, 1:3, 0:2)
B
```

    ##      [,1] [,2] [,3]
    ## [1,]    2    1    0
    ## [2,]    1    2    1
    ## [3,]    0    3    2

``` r
# Combining vectors by row
C <- rbind(1:3, 4:6, 7:9)
C
```

    ##      [,1] [,2] [,3]
    ## [1,]    1    2    3
    ## [2,]    4    5    6
    ## [3,]    7    8    9

### Basic Linear Algebra

We can perform basic linear algebra operations on matrices:

``` r
# Basic Linear Algebra
# Vector Operations
4 * a
```

    ##    a    b 
    ##  9.2 16.0

``` r
(a) ^ -1
```

    ##         a         b 
    ## 0.4347826 0.2500000

``` r
a + a1
```

    ##    a    b 
    ##  6.3 11.0

``` r
# Matrix Transpose
t(A)
```

    ##      [,1] [,2] [,3]
    ## [1,]    3    2    2
    ## [2,]    1    3    2
    ## [3,]    1    1    3

``` r
# Matrix Addition
A + B - C
```

    ##      [,1] [,2] [,3]
    ## [1,]    4    0   -2
    ## [2,]   -1    0   -4
    ## [3,]   -5   -3   -4

``` r
# Dot Product
A %*% B
```

    ##      [,1] [,2] [,3]
    ## [1,]    7    8    3
    ## [2,]    7   11    5
    ## [3,]    6   15    8

``` r
# Cross Product
t(A) %*% B == crossprod(A, B)
```

    ##      [,1] [,2] [,3]
    ## [1,] TRUE TRUE TRUE
    ## [2,] TRUE TRUE TRUE
    ## [3,] TRUE TRUE TRUE

``` r
# Inverse
C <- matrix(c(39L, 8L, 71L, 72L, 54L, 42L, 76L, 77L, 15L), ncol = 3)
D <- solve(C)
C %*% D
```

    ##      [,1]          [,2] [,3]
    ## [1,]    1  0.000000e+00    0
    ## [2,]    0  1.000000e+00    0
    ## [3,]    0 -4.440892e-16    1

``` r
round(C %*% D)
```

    ##      [,1] [,2] [,3]
    ## [1,]    1    0    0
    ## [2,]    0    1    0
    ## [3,]    0    0    1

``` r
# Eigenvalues and Eigenvectors
eigen(C)
```

    ## eigen() decomposition
    ## $values
    ## [1] 147.741703 -34.981904  -4.759798
    ## 
    ## $vectors
    ##            [,1]       [,2]       [,3]
    ## [1,] -0.6935491 -0.1529705  0.3017373
    ## [2,] -0.4916846 -0.6387581 -0.7727752
    ## [3,] -0.5265319  0.7540478  0.5583664

``` r
e <- eigen(C)$vector
v <- eigen(C)$value
C %*% e[, 1] == v[1] * e[, 1]
```

    ##       [,1]
    ## [1,] FALSE
    ## [2,] FALSE
    ## [3,] FALSE

``` r
all.equal(as.vector(C %*% e[, 1]), v[1] * e[, 1])
```

    ## [1] TRUE

### Data Frames

Data frames have a more heterogeneous structure compared to matrices.
While vectors and matrices belong to a specific `typeof` object, data
frames can have multiple data types in each column.

``` r
## Basic Data Frame
df <- data.frame(
  A = LETTERS[1:5],
  B = factor(letters[1:5]),
  C = 1L:5L,
  D = c(2.4, 2, 3, 9, 7)
)

# Structure
str(df)
```

    ## 'data.frame':    5 obs. of  4 variables:
    ##  $ A: chr  "A" "B" "C" "D" ...
    ##  $ B: Factor w/ 5 levels "a","b","c","d",..: 1 2 3 4 5
    ##  $ C: int  1 2 3 4 5
    ##  $ D: num  2.4 2 3 9 7

``` r
# Basic statistics
summary(df)
```

    ##       A             B           C           D       
    ##  Length:5           a:1   Min.   :1   Min.   :2.00  
    ##  Class :character   b:1   1st Qu.:2   1st Qu.:2.40  
    ##  Mode  :character   c:1   Median :3   Median :3.00  
    ##                     d:1   Mean   :3   Mean   :4.68  
    ##                     e:1   3rd Qu.:4   3rd Qu.:7.00  
    ##                           Max.   :5   Max.   :9.00

``` r
# Print head
head(df, 3)
```

    ##   A B C   D
    ## 1 A a 1 2.4
    ## 2 B b 2 2.0
    ## 3 C c 3 3.0

``` r
# Print tail
tail(df)
```

    ##   A B C   D
    ## 1 A a 1 2.4
    ## 2 B b 2 2.0
    ## 3 C c 3 3.0
    ## 4 D d 4 9.0
    ## 5 E e 5 7.0

``` r
## Bipartite Projection
bp <- data.frame(papers = c(rep('A', 3), rep('B', 2), 'C'), authors = c(1:3, 2:3, 4))
bp
```

    ##   papers authors
    ## 1      A       1
    ## 2      A       2
    ## 3      A       3
    ## 4      B       2
    ## 5      B       3
    ## 6      C       4

``` r
# Incidence Matrix
py <- table(bp)
py
```

    ##       authors
    ## papers 1 2 3 4
    ##      A 1 1 1 0
    ##      B 0 1 1 0
    ##      C 0 0 0 1

``` r
# Adjacency Matrix
py <- crossprod(py)
py
```

    ##        authors
    ## authors 1 2 3 4
    ##       1 1 1 1 0
    ##       2 1 2 2 0
    ##       3 1 2 2 0
    ##       4 0 0 0 1

### Functions

Functions are invaluable when we need to perform the same operation(s)
multiple times. Let’s create a simple function to calculate the degree
from an adjacency matrix:

``` r
n <- 5
A <- matrix(sample(0:1, n * n, replace = TRUE), ncol = n)
rownames(A) <- LETTERS[1:n]
colnames(A) <- LETTERS[1:n]

# Remove loops
diag(A) <- 0

s.degree <- function(x) {
  n <- ncol(x)
  d <- x %*% rep(1, n)
  colnames(d) <- 'Degree'
  d
}

s.degree(A)
```

    ##   Degree
    ## A      3
    ## B      2
    ## C      0
    ## D      1
    ## E      1

### Lists

Lists are the most flexible data structure in R, allowing us to store
multiple objects of different classes. A data frame is a list with a
specific structure. We can use the `dput` function to print and store
the structure of any object, which helps in creating reproducible
examples.

``` r
# Print the structure of the data frame
dput(df)
```

    ## structure(list(A = c("A", "B", "C", "D", "E"), B = structure(1:5, levels = c("a", 
    ## "b", "c", "d", "e"), class = "factor"), C = 1:5, D = c(2.4, 2, 
    ## 3, 9, 7)), class = "data.frame", row.names = c(NA, -5L))

``` r
# Store a vector, matrix, data frame, function, and a list together
s <- list(c(1:3))
l <- list(
  factor = f,
  matrix = A,
  data.frame = df,
  list = s
)
str(l)
```

    ## List of 4
    ##  $ factor    : Factor w/ 2 levels "male","female": NA NA
    ##  $ matrix    : num [1:5, 1:5] 0 1 0 0 1 1 0 0 0 0 ...
    ##   ..- attr(*, "dimnames")=List of 2
    ##   .. ..$ : chr [1:5] "A" "B" "C" "D" ...
    ##   .. ..$ : chr [1:5] "A" "B" "C" "D" ...
    ##  $ data.frame:'data.frame':  5 obs. of  4 variables:
    ##   ..$ A: chr [1:5] "A" "B" "C" "D" ...
    ##   ..$ B: Factor w/ 5 levels "a","b","c","d",..: 1 2 3 4 5
    ##   ..$ C: int [1:5] 1 2 3 4 5
    ##   ..$ D: num [1:5] 2.4 2 3 9 7
    ##  $ list      :List of 1
    ##   ..$ : int [1:3] 1 2 3

### Indexing Objects

Subsetting in R can be done using nominal, numeric, or logical indexing.
Data frames and lists use the special operator `$` for subsetting.

``` r
### Nominal ####
## Vectors ##
names(a)
```

    ## [1] "a" "b"

``` r
a['a']
```

    ##   a 
    ## 2.3

``` r
a['b']
```

    ## b 
    ## 4

``` r
## Matrices ##
A[c('A', 'C'), c('D', 'E')]
```

    ##   D E
    ## A 1 1
    ## C 0 0

``` r
## Data Frames ##
df[c('A', 'D')]
```

    ##   A   D
    ## 1 A 2.4
    ## 2 B 2.0
    ## 3 C 3.0
    ## 4 D 9.0
    ## 5 E 7.0

``` r
## Lists ##
l[c('factor', 'matrix')]
```

    ## $factor
    ## [1] <NA> <NA>
    ## Levels: male female
    ## 
    ## $matrix
    ##   A B C D E
    ## A 0 1 0 1 1
    ## B 1 0 0 1 0
    ## C 0 0 0 0 0
    ## D 0 0 1 0 0
    ## E 1 0 0 0 0

``` r
### Numeric ####

## Vectors ##
a[1]
```

    ##   a 
    ## 2.3

``` r
## Matrices ##
A[2:3, 4]
```

    ## B C 
    ## 1 0

``` r
## Data Frames ##
df[1:5, 2:3]
```

    ##   B C
    ## 1 a 1
    ## 2 b 2
    ## 3 c 3
    ## 4 d 4
    ## 5 e 5

``` r
## Lists ##
# Extract the data frame
l[unlist(lapply(l, class)) == 'data.frame']
```

    ## $list
    ## $list[[1]]
    ## [1] 1 2 3

``` r
### Logical ####

## Vectors ##
a[c(TRUE, FALSE)]
```

    ##   a 
    ## 2.3

``` r
## Matrices ##
A[upper.tri(A)]
```

    ##  [1] 1 0 0 1 1 0 1 0 0 0

``` r
## Data Frames ##
df[, c(rep(FALSE, 3), TRUE)]
```

    ## [1] 2.4 2.0 3.0 9.0 7.0

``` r
## Lists ##
# Extract the data frame
l$data.frame$C
```

    ## [1] 1 2 3 4 5

``` r
l$matrix[, 4]
```

    ## A B C D E 
    ## 1 1 0 0 0

``` r
### Combinations ###
A[2:3, c('C', 'D')]
```

    ##   C D
    ## B 0 1
    ## C 0 0

``` r
### Special Operator ####
# Subset a Column
df$A
```

    ## [1] "A" "B" "C" "D" "E"

``` r
# Subset the data frame in a list and print column D
l$data.frame$C
```

    ## [1] 1 2 3 4 5

``` r
l$matrix[, 4]
```

    ## A B C D E 
    ## 1 1 0 0 0

### Control Flow

Control flow structures like `if`, `else`, and `ifelse` are essential
for making decisions and executing code conditionally in R.

``` r
### Basic Structure if|else ####
condition <- 7
if (condition == 7) {
  print('Yes, it is...')
}
```

    ## [1] "Yes, it is..."

``` r
# Check if a graph is connected
is.connected <- function(am) {
  d <- s.degree(am)
  if (all(d > 0)) {
    print('Graph is connected')
  } else {
    print('Graph is disconnected')
  }
}

py <- table(bp)
py
```

    ##       authors
    ## papers 1 2 3 4
    ##      A 1 1 1 0
    ##      B 0 1 1 0
    ##      C 0 0 0 1

``` r
is.connected(py)
```

    ## [1] "Graph is connected"

``` r
# Evaluate multiple conditions (and, or)
is.sim_multi <- function(am) {
  mult.ed <- any(am > 1)
  loops <- sum(diag(am)) != 0
  type <- c('The graph has:', 'multi edges', 'and loops.')
  if (mult.ed | loops) {
    am[am > 1] <- 1
    diag(am) <- 0
    print(paste(type[c(TRUE, mult.ed, loops)], collapse = " "))
  } else {
    print("The graph is simple")
  }
}

is.sim_multi(B)
```

    ## [1] "The graph has: multi edges and loops."

``` r
is.sim_multi(A)
```

    ## [1] "The graph is simple"

``` r
# Count the number of edges or vertices
no.ver.edges <- function(am) {
  v <- ncol(am)
  e <- sum(am > 0)
  if (e > v) {
    print(paste('Edges:', e))
  } else if (e < v) {
    print(paste('Vertices:', v))
  } else {
    paste('Vertices and Edges:', v)
  }
}

no.ver.edges(A)
```

    ## [1] "Edges: 7"

``` r
no.ver.edges(B)
```

    ## [1] "Edges: 7"

``` r
#### ifelse function ####
# ifelse function is efficient and partially vectorized
# It produces an output of the same length as the input.

ifelse(4 > 7, "YES", "NO")
```

    ## [1] "NO"

``` r
ifelse(7 > 4, "YES", "NO")
```

    ## [1] "YES"

``` r
# Nested ifelse
is.sym <- function(am) {
  ifelse(ncol(am) != nrow(am),
    'Not symmetric',
    ifelse(all(am[upper.tri(am)] == am[lower.tri(am)]), 'Symmetric', 'Squared'))
}

A
```

    ##   A B C D E
    ## A 0 1 0 1 1
    ## B 1 0 0 1 0
    ## C 0 0 0 0 0
    ## D 0 0 1 0 0
    ## E 1 0 0 0 0

``` r
is.sym(A)
```

    ## [1] "Squared"

``` r
B[3, 2] <- 1
B
```

    ##      [,1] [,2] [,3]
    ## [1,]    2    1    0
    ## [2,]    1    2    1
    ## [3,]    0    1    2

``` r
is.sym(B)
```

    ## [1] "Symmetric"

### Loops

Loops are used for repetitive tasks, but it’s essential to use them
judiciously as they can be inefficient. Here, we cover while and for
loops:

``` r
### while loop ####
fibo <- c(1, 2)
digi <- length(fibo)

# Create a Fibonacci Sequence and stop when it reaches 10 digits
while (digi < 4) {
  digi <- length(fibo)
  fibo[digi + 1] <- sum(fibo[digi - 1], fibo[digi])
  print(paste("Fibonacci Seq:", fibo[digi]))
}
```

    ## [1] "Fibonacci Seq: 2"
    ## [1] "Fibonacci Seq: 3"
    ## [1] "Fibonacci Seq: 5"

``` r
### for loop ####
# Get adjacent vertices (neighborhood)
i <- 1
nams <- row.names(A)

for (i in 1:nrow(A)) {
  print(nams[A[i, ] > 0])
}
```

    ## [1] "B" "D" "E"
    ## [1] "A" "D"
    ## character(0)
    ## [1] "C"
    ## [1] "A"

### Apply Family of Functions

The `apply` function in R takes an array as its first argument and
applies a function to all the elements of the array. Let’s explore some
examples:

``` r
# Example of summing all the columns of a matrix
ma <- matrix(sample(1:100, 25), ncol = 5, nrow = 5)

# Using a loop
col.cum <- vector('numeric', length = 0)
for (c in 1:ncol(ma)) {
  col.cum <- c(col.cum, sum(ma[, c]))
}

# Using the apply function
apply(ma, 2, sum) == col.cum
```

    ## [1] TRUE TRUE TRUE TRUE TRUE

In this example, we create a matrix `ma` and calculate the sum of each
column using both a loop and the `apply` function. The apply function
provides a more concise and efficient way to perform this operation.

``` r
# Example of summing each row of a matrix

# Using a loop
row.cum <- vector('numeric', length = 0)
for (r in 1:nrow(ma)) {
  row.cum <- c(row.cum, sum(ma[r, ]))
}

# Using the apply function
apply(ma, 1, sum) == row.cum
```

    ## [1] TRUE TRUE TRUE TRUE TRUE

``` r
# Using linear algebra (For simpler functions, it is better to use linear algebra)
apply(ma, 1, sum) == row.cum & rowSums(ma) == row.cum
```

    ## [1] TRUE TRUE TRUE TRUE TRUE

In this section, we demonstrate how to sum each row of a matrix, first
using a loop and then using the `apply` function. Additionally, we show
how you can achieve the same result using linear algebra operations for
efficiency.

``` r
# Example: Count how many times a string [A-] appears in each column

ma <- matrix(replicate(5, sample(LETTERS[1:10], 5)), ncol = 5, nrow = 5, byrow = TRUE)
lvls <- unique(c(ma))
apply(ma, 2, function(x) {
  table(factor(x, levels = lvls))
})
```

    ##   [,1] [,2] [,3] [,4] [,5]
    ## J    1    1    0    0    0
    ## F    2    1    0    0    0
    ## G    1    1    0    0    0
    ## I    1    0    1    0    2
    ## D    0    1    0    1    0
    ## A    0    1    1    0    0
    ## E    0    0    1    1    0
    ## C    0    0    2    0    2
    ## B    0    0    0    1    1
    ## H    0    0    0    2    0

In this example, we create a matrix of random characters and count how
many times each character appears in each column using the apply
function.

### lapply Function

The `lapply` function in R takes a list as its first argument and
applies a function to all the elements of the list. It offers advantages
such as improved code readability and flexibility compared to the
`apply` function.

``` r
### lapply Examples ###

# Heterogeneous list example
lapply(list(data.frame(1:10), 20:30), sum)
```

    ## [[1]]
    ## [1] 55
    ## 
    ## [[2]]
    ## [1] 275

``` r
# Homogeneous list example
lapply(list(A, B, C, D), s.degree)
```

    ## [[1]]
    ##   Degree
    ## A      3
    ## B      2
    ## C      0
    ## D      1
    ## E      1
    ## 
    ## [[2]]
    ##      Degree
    ## [1,]      3
    ## [2,]      4
    ## [3,]      3
    ## 
    ## [[3]]
    ##      Degree
    ## [1,]    187
    ## [2,]    139
    ## [3,]    128
    ## 
    ## [[4]]
    ##           Degree
    ## [1,]  0.04585366
    ## [2,] -0.07556911
    ## [3,]  0.06121951

``` r
# Since a data.frame is a list, we can apply functions directly
# Check the list of sample data.frames ?data
# Load data
data(attitude)

lapply(attitude, function(x) {
  c(
    mean = mean(x),
    var = var(x),
    min = min(x),
    max = max(x),
    median = median(x)
  )
})
```

    ## $rating
    ##      mean       var       min       max    median 
    ##  64.63333 148.17126  40.00000  85.00000  65.50000 
    ## 
    ## $complaints
    ##     mean      var      min      max   median 
    ##  66.6000 177.2828  37.0000  90.0000  65.0000 
    ## 
    ## $privileges
    ##      mean       var       min       max    median 
    ##  53.13333 149.70575  30.00000  83.00000  51.50000 
    ## 
    ## $learning
    ##      mean       var       min       max    median 
    ##  56.36667 137.75747  34.00000  75.00000  56.50000 
    ## 
    ## $raises
    ##      mean       var       min       max    median 
    ##  64.63333 108.10230  43.00000  88.00000  63.50000 
    ## 
    ## $critical
    ##     mean      var      min      max   median 
    ## 74.76667 97.90920 49.00000 92.00000 77.50000 
    ## 
    ## $advance
    ##      mean       var       min       max    median 
    ##  42.93333 105.85747  25.00000  72.00000  41.00000

Here, we showcase various uses of `lapply`. It can be applied to both
heterogeneous and homogeneous lists. When working with data frames, you
can directly apply functions to columns, which can lead to more readable
code.

``` r
# Similar to summary(attitude)

# Try to arrange the structure for better readability (not always successful)
t <- sapply(attitude, function(x) {
  c(
    mean = mean(x),
    var = var(x),
    min = min(x),
    max = max(x),
    median = median(x)
  )
})
class(t)
```

    ## [1] "matrix" "array"

In this section, we demonstrate a similar approach to the
`summary(attitude)` function using `sapply` to provide a structured
summary of the data.

## Graphics in R

R offers a robust environment for creating graphics, making it a
powerful tool for both statistical analysis and data visualization. To
explore its capabilities, you can start by running `demo(graphics)` in
the R console. Additionally, you can refer to this cheatsheet for an
overview of the main plotting functions.

``` r
# demo(graphics)
```

Let’s delve into various aspects of graphics in R.

### Color Management

Managing color spaces in R is essential for creating visually appealing
graphics. Colors can be defined in three different ways: by name, by
hexadecimal values, or by RGB values. You can explore a wide range of
colors and conversions between these systems on this
[website](http://cloford.com/resources/colours/500col.htm).

For this tutorial a palette of high contrasting colors that I am defining in the following vector:

``` r
colors37 = c("#466791","#60bf37","#953ada","#4fbe6c","#ce49d3","#a7b43d","#5a51dc","#d49f36","#552095","#507f2d","#db37aa","#84b67c","#a06fda","#df462a","#5b83db","#c76c2d","#4f49a3","#82702d","#dd6bbb","#334c22","#d83979","#55baad","#dc4555","#62aad3","#8c3025","#417d61","#862977","#bba672","#403367","#da8a6d","#a79cd4","#71482c","#c689d0","#6b2940","#d593a7","#895c8b","#bd5975")
```

And in this snipped of code where you can see clearly the contrast in the palette:

``` r
# Example of hexadecimal format
# print(head(colors37))
# Example of RGB 
# rgb(red=1, green=0.05, blue=0.02, alpha=.2)
# Examples colors by name
# head(colors())

# Plot using a color space by name
plot(
  # Values on the x-axis
  x = 2:10,
  # Values on the y-axis
  y = 9:1,
  # Size of the point
  pch = 19,
  # Shape of the point
  cex = 2,
  # Color by name
  col = "dark red",
  # Axis labels
  xlab = "",
  ylab = "",
  axes = FALSE,
  # Limits for x and y
  xlim = c(2, 10.05),
  ylim = c(0, 11)
)

# Try running these loops again but change the cex value to get different shapes
for (i in 2:9) {
  # Plot using the RGB color space (arguments are values between [0,1]) 
  points(x = i:10, y = 10:i, pch = 19, cex = 2, col = rgb(runif(1), runif(1), runif(1)))
  # Plot using a vector of hexadecimal values
  points(x = 2:(11 - i), y = (10 - i):1, pch = 19, cex = 2, col = sample(colors37, 1))
}

# Draw a box
box()
```

![](https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-24-1.png?raw=true)<!-- -->

In this section, we explore different ways to define and use colors in
your plots, including by name, RGB values, and hexadecimal values.

### Histograms

Histograms are a fundamental tool for visualizing the distribution
(spread) of data around central values. To plot a single variable we can
use the `hist(...)`, and we need to include the specific vector that
contains the data, for instance, `hist(attitude[, 1L])`.

``` r
### Plotting a simple histogram ####
hist(attitude[, 1L])
```

![](https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-25-1.png?raw=true)<!-- -->

However, typically we are interested on visualize a whole set of
variables on a data frame. Hence, I believe it is more useful a snipped
of code that can plot a group of variables in grid (a group of plots).
The subsequent R code sets up a 3x3 plotting layout using the `par()`
function, allowing for a 3x3 grid of plots. Then the following code then
creates histograms for each variable in the `attitude` dataframe and
arranges them within the previously defined layout.

Here’s a step-by-step breakdown:

- `par(mfrow = c(3, 3))`: This sets up a plotting layout with 3 rows and
  3 columns, creating a 3x3 grid for plotting.

- `var.names <- colnames(attitude)`: Retrieves the column names
  (variable names) of the `attitude` dataframe.

- `invisible(lapply(seq_along(var.names), function(x) {...})`: Iterates
  over each variable in `attitude` using `lapply()` and generates
  histograms.

- `hist(...)`: Generates a histogram for each variable. The hist()
  function takes parameters such as the data to be plotted
  (`attitude[, x]` for each variable), the main title (`var.names[x]`,
  which is the variable name), and the color of the bars
  (`col = sample(colors37, 1)`).

- The `invisible()` function is used to suppress the output of
  `lapply()` which would otherwise display the individual histograms.

``` r
### Using lapply and histograms ###

# Set up a 3 x 3 layout

par(mfrow = c(3, 3))

# render the histograms 
var.names <- colnames(attitude)
invisible(lapply(seq_along(var.names), function(x) {
  hist(
    attitude[, x],
    main = var.names[x],
    col = sample(colors37, 1),
    xlab = ""
  )
}))
```

![](https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-26-1.png?raw=true)<!-- -->
\### Box-Plots:

Box plots, also known as box-and-whisker plots, are a valuable tool for
visualizing the distribution and spread of data. They provide a concise
summary of a dataset’s central tendency, variability, and potential
outliers. Unlike some other types of plots, box plots focus on
displaying the overall distribution of data rather than showing
individual data points.

They are particularly useful because they show the following key
statistics:

- The median (the middle value of the dataset).
- The interquartile range (the range between the first quartile or Q1
  and the third quartile or Q3), which contains the central 50% of the
  data.
- The minimum and maximum values within a defined range.
- Outliers, represented as individual points outside the “whiskers” of
  the plot.

Similar to the previous chunk, I am using the `lapply` combined with the
function of box-plots (`boxplot(...)`) to efficiently display a plot for
each variable in the `attitude` dataset.

``` r
  par(mfrow = c(3, 3))
  var.names <- colnames(attitude)
  invisible(lapply(seq_along(var.names), function(x) {
  boxplot(attitude[, x],
  main = var.names[x],
  xlab = "")
  }))
```

![](https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-27-1.png?raw=true)<!-- -->

### Scatter Plots:

Scatter plots are a basic form of data visualization that help us see
the relationship between two continuous variables. They differ from
other plots because they allow us to examine how two variables interact,
specifically whether there is a linear or nonlinear relationship between
them.

The importance of scatter plots lies in their ability to reveal
patterns, trends, clusters and outliers in the data. By arranging data
points as individual points on a two-dimensional plane, we can visually
identify relationships, associations, or the lack thereof. Scatter plots
are particularly useful for the following reasons.

- Finding linear and non-linear relationships: Scatter plots help us to
  find out if two variables are linearly positively or negatively
  related or the relationship is not linear.

- Identifying outliers: Outliers, data points that deviate significantly
  from the overall pattern, are easily detected in scatter plots and can
  be identified

- Cluster analysis: Clusters of data points can indicate distinct
  subpopulations or clusters in the data.

- Visualizing multivariate data: Scatter matrices like the one created
  in your code snippet allow us to visualize relationships between
  multiple variables simultaneously, which is important in exploratory
  data analysis

Using Scatter Plots in R:

`pairs(attitude, main = "attitude data", panel = panel.smooth)`: This
line generates a scatter plot matrix (a grid of scatter plots) for all
the variables in the “attitude” dataset. The panel.smooth argument adds
smoothed regression lines to each scatter plot to help visualize trends.

``` r
  # Plot variables: Useful to detect linear or non-linear patterns.
  pairs(attitude, main = "attitude data", panel = panel.smooth)
```

![](https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-28-1.png?raw=true)<!-- -->

`plot(attitude$rating, attitude$complaints)`: This line creates a single
scatter plot between the “rating” and “complaints” variables, providing
a detailed view of the relationship between these two specific
variables.

``` r
  # Single plot
  plot(attitude$rating, attitude$complaints)
```

![](https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-29-1.png?raw=true)<!-- -->

`abline(lm(rating ~ complaints, data = attitude), col = 'red')`: Here, a
regression line is added to the scatter plot created in the previous
step. This line represents the best-fit linear relationship between
“rating” and “complaints” using a linear regression model. The line is
colored red for visibility.

``` r
  plot(attitude$rating, attitude$complaints)
  # Draw a regression line
  abline(lm(rating ~ complaints, data = attitude), col = 'red')
```

![](https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-30-1.png?raw=true)<!-- -->

### Multiple Regression model

Imagine you have a yummy meal, and you want to know what makes it taste
so good. Is it the color, the smell, or maybe the shape? Multiple
regression helps us figure out which of these things, or variables, are
most important in making the meal delicious. It’s like sniffing out the
best part of a treat recipe! So the idea of regression is that we have a
series of variables that affect or predict the behavior of another
outcome variable. These explanatory variables are called determinants of
the dependent variable precisely for their power to predict outcome.

- Univariate models have only one determinant, but they are mostly
  unused. It is difficult to expect that one thing has only one
  predictor.

``` r
  # Single Regression
m0 <- lm(rating ~ advance, data = attitude)
summary(m0)
```

    ## 
    ## Call:
    ## lm(formula = rating ~ advance, data = attitude)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -25.7465  -4.8749   0.5975   7.4232  18.1526 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept)  56.7558     9.7428   5.825 2.93e-06 ***
    ## advance       0.1835     0.2209   0.831    0.413    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 12.24 on 28 degrees of freedom
    ## Multiple R-squared:  0.02405,    Adjusted R-squared:  -0.0108 
    ## F-statistic:  0.69 on 1 and 28 DF,  p-value: 0.4132

- Multiple Regression model has two or more explanatory variables and it
  is the most frequent use model.

``` r
m1 <- lm(rating ~ ., data = attitude)
summary(m1)
```

    ## 
    ## Call:
    ## lm(formula = rating ~ ., data = attitude)
    ## 
    ## Residuals:
    ##      Min       1Q   Median       3Q      Max 
    ## -10.9418  -4.3555   0.3158   5.5425  11.5990 
    ## 
    ## Coefficients:
    ##             Estimate Std. Error t value Pr(>|t|)    
    ## (Intercept) 10.78708   11.58926   0.931 0.361634    
    ## complaints   0.61319    0.16098   3.809 0.000903 ***
    ## privileges  -0.07305    0.13572  -0.538 0.595594    
    ## learning     0.32033    0.16852   1.901 0.069925 .  
    ## raises       0.08173    0.22148   0.369 0.715480    
    ## critical     0.03838    0.14700   0.261 0.796334    
    ## advance     -0.21706    0.17821  -1.218 0.235577    
    ## ---
    ## Signif. codes:  0 '***' 0.001 '**' 0.01 '*' 0.05 '.' 0.1 ' ' 1
    ## 
    ## Residual standard error: 7.068 on 23 degrees of freedom
    ## Multiple R-squared:  0.7326, Adjusted R-squared:  0.6628 
    ## F-statistic:  10.5 on 6 and 23 DF,  p-value: 1.24e-05

# Section 2: An introduction to Network Analysis using Igraph

## Install packages

Before you start this section I recommend that you install the following packages:

-   `igraph`: A package for network analysis and visualization (most important).
-   `tnet`: A package for analyzing weighted, two-mode, and longitudinal networks.
-   `data.table`: A package for data manipulation and analysis.
-   `qgraph`: A package for creating and analyzing graphical models (e.g., network models) that we use only to improve the visualization of networks.
-   `knitr`: A package for dynamic report generation in R.


``` r

# packages
pks <- c('knitr', 'igraph', 'tnet', 'data.table', 'qgraph')
 
#Load and install packages
to.install <- pks[!unlist(lapply(pks, require, character.only = T ))]
if(length(to.install)!=0){install.packages(to.install, dependencies = T)}

```

## Generate Graphs

To create networks, we have the option of utilizing both R base
functions and functions within the igraph package.

### Using Adjanceny Matrices

One approach involves generating a network using an adjacency matrix,
where the rows and columns of the matrix correspond to vertices, and the
values in the matrix indicate connections between these vertices.

``` r
#### Graph from a Matrix ####
n <- 5
g <- matrix(0, ncol = n, nrow = n)
val <- round(runif(sum(upper.tri(g)), min = 0, max = 1))
g[upper.tri(g)] <- val
g <- t(g) + g

# Create a graph object
g1 <- graph_from_adjacency_matrix(g, mode = "undirected")
as_bipartite()
```

    ## igraph layout specification, see ?layout_:
    ## layout_as_bipartite(<graph>, input = "C:/Users/mglez/Documents/PHD/Semester 16/15092023_network_blog/igraph_tu_mgs_v01.Rmd", 
    ##  igraph layout specification, see ?layout_:
    ##     encoding = "UTF-8")

``` r
?as_bipartite
```

    ## starting httpd help server ... done

### Using Edge lists

- The second most common way to generate a network is from an edge list
  or a set of pairs that define the connection between two vertices.

``` r
#### Graph from Edgelist ####
g1 <- graph_from_edgelist(t(combn(1:n,2)))
```

### Using formulas

- The third way to create a graph is by using specific formulas with the
  `graph_from_literal` function. This function enables us to create
  networks based on formulaic representations. Essentially, we specify
  the desired network structure using a compact formula notation within
  this function.

This is the general notation of the function:

- `-+`: Represents a directed edge between two vertices. For example,
  `A -+ B` indicates a directed edge from vertex A to vertex B.

- `--`: Represents an undirected edge between two vertices. For example,
  `A -- B` indicates an undirected edge between vertex A and vertex B.

- `++`: Represents a directed edge with an arrowhead at both ends,
  implying a bidirectional connection between two vertices. For example,
  `A ++ B` signifies bidirectional directed edges between vertex A and
  vertex B.

- `:`: Represents a grouping of vertices. For example, `A:B` signifies
  that vertices A and B are in the same group or cluster within the
  network.

These notations allow you to define various types of connections and
structures within your network using concise and expressive formulas.

``` r
#### Graph from Formula ####

#Undirected
par(mfrow = c(1, 4))
g1 <- graph_from_literal( A-B-C )

#Directed
g2 <- graph_from_literal( A -+ B ++ C )

#Undirected grouping
g3 <- graph_from_literal( A-B:C )

#Directed grouping
g4 <- graph_from_literal( A-+B:C )

#Plot the graphs
invisible(lapply(list(g1, g2, g3, g4), plot, vertex.size = 25, edge.arrow.size = .5))
```

![](https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-35-1.png?raw=true)<!-- -->

### Using igraph-functions

In the `igraph` package, there are several functions are available to
generate networks using various algorithms and models. Here are some of
the commonly used functions for network generation:

Erdős-Rényi Model (`erdos.renyi.game`): This function generates random
networks following the Erdős-Rényi model. In this model, you specify the
number of vertices (n) and the probability (p) of forming an edge
between any pair of vertices. The default type is set to `gnp` for the
probability model. This model is useful for creating networks where
edges exist between pairs of vertices independently with a fixed
probability.

Watts-Strogatz Model (`watts.strogatz.game`): The Watts-Strogatz model
creates small-world networks with a combination of regularity and
randomness. By default, it starts with a regular lattice where each
vertex is connected to its (nei) nearest neighbors in a ring. Then,
edges are rewired with probability p to introduce randomness. You can
specify the number of vertices (n), the dimension of the lattice (dim),
the number of neighbors (nei), and the rewiring probability (p) as
parameters. This model helps generate networks that exhibit small-world
properties.

Barabási-Albert Model (`barabasi.game`): This function generates
networks using the Barabási-Albert model. By default, it creates an
undirected network with n vertices and attaches each new vertex to m
existing vertices with preferential attachment. The default is set to
`m = 1`, meaning each new vertex connects to a single existing vertex.
This model results in scale-free networks with a few highly connected
nodes, which is a common property in many real-world networks.

Forest Fire Model (`forest.fire.game`): The forest fire model simulates
the growth of networks using the forest fire algorithm. By default, it
creates a network with n vertices. The m parameter specifies the number
of edges added from the new vertex to the existing graph in each step.
The p parameter controls the probability of spreading the fire to
existing vertices. This model is suitable for generating networks with a
specified number of vertices and a desired average degree while
considering network growth dynamics.

``` r
# Set the number of vertices for all networks
n <- 25

# Generate networks using different models
g1 <- erdos.renyi.game(n, p = 0.2)
g2 <- watts.strogatz.game(n, dim = 1, size = 4, p = 0.2)
g3 <- barabasi.game(n, m = 1)
g4 <- forest.fire.game(n, fw.prob = 0.2, bw.factor = 2)
```

This is the full list of functions available in igraph to generate
networks:

``` r
games <- grep("^.*game", ls("package:igraph"), value = TRUE)[-1]
games
```

    ##  [1] "aging.barabasi.game"         "aging.prefatt.game"         
    ##  [3] "asymmetric.preference.game"  "ba.game"                    
    ##  [5] "barabasi.game"               "bipartite.random.game"      
    ##  [7] "callaway.traits.game"        "cited.type.game"            
    ##  [9] "citing.cited.type.game"      "degree.sequence.game"       
    ## [11] "erdos.renyi.game"            "establishment.game"         
    ## [13] "forest.fire.game"            "grg.game"                   
    ## [15] "growing.random.game"         "hrg.game"                   
    ## [17] "interconnected.islands.game" "k.regular.game"             
    ## [19] "lastcit.game"                "preference.game"            
    ## [21] "random.graph.game"           "sbm.game"                   
    ## [23] "static.fitness.game"         "static.power.law.game"      
    ## [25] "watts.strogatz.game"

## Visualizing Networks with igraph

To create insightful network visualizations using the `igraph` package
in R, we’ll begin with plotting a simple network. Later on, we’ll
explore customization options and demonstrate how to visualize multiple
networks side by side.

### Plotting a Simple Network

In this initial plot, we have our network displayed.

``` r
plot(g1)
```

![](https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-38-1.png?raw=true)<!-- -->

However, to improve the visualization we can further customize the
attributes of the `plot` function in the following way:

- `vertex.size`: This attribute allows you to adjust the size of the
  nodes (vertices) in your network.
- `edge.arrow.size`: If your network contains directed edges, you can
  modify the arrow size using this attribute.
- `vertex.color`: Sets the color of nodes (here, light blue).
- `edge.color`: Defines the color of edges (here, gray).
- `vertex.label`: Removes node labels for a cleaner visualization.
- `layout`: Specifies the layout algorithm; we used the
  Fruchterman-Reingold layout here.

### Customizing network attributes:

``` r
# Visualizing multiple networks in a grid
par(mfrow = c(2, 2))
networks <- list(g1, g2, g3, g4)
invisible(lapply(networks, plot, 
                vertex.size = 25, 
                edge.arrow.size = 0.5,
                vertex.color = "lightblue", 
                edge.color = "gray",
                vertex.label = NA,
                layout = layout.fruchterman.reingold))
```

![](https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-39-1.png?raw=true)<!-- -->

### Layouts of igraph

The igraph has different algorithms called layouts, which help us
visualize and highlight network patterns, degree distributions, and the
spatial arrangement of vertices within a network.

``` r
# Generate a graph
n <- 15
g1 <- barabasi.game(n, directed = F)

# Explore the complete list of layouts.
# layouts <- grep("^layout_", ls("package:igraph"), value = TRUE)[-1]
# layouts <- layouts[!grepl("bipartite|sugiyama", layouts)]
# dput(layouts)

layouts <- c("layout_as_star", "layout_as_tree", "layout_components", "layout_in_circle", 
"layout_nicely", "layout_on_grid", "layout_on_sphere", "layout_randomly", 
"layout_with_dh", "layout_with_drl", "layout_with_fr", "layout_with_gem", 
"layout_with_graphopt", "layout_with_kk", "layout_with_lgl", 
"layout_with_mds")

par(mfrow = c(2, 2))
invisible(lapply(layouts, function(x){plot(
g1,
vertex.size = 30,
layout = eval(get(x)),
xlab = x
) }))
```

![](https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-40-1.png?raw=true)<!-- -->![](https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-40-2.png?raw=true)<!-- -->![](https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-40-3.png?raw=true)<!-- -->![](https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-40-4.png?raw=true)<!-- -->

### Setting shape of vertices

Vertex shapes in a network graph represent the graphical symbols used to
depict individual vertices or nodes. They are a visual attribute that
allows you to distinguish between nodes based on specific
characteristics or groupings. Vertex shapes are useful in network
visualization as they help convey additional information beyond just the
connections between nodes.

To illustrate the usefulness of vertex shapes, we are creating an
example where we visualize different vertex attributes. In this
particular case, we’re generating a random variable called `Age` from
random draws of a normal distribution, with a mean of `30` and a
standard deviation of `5`, and dividing the vertices into three distinct
groups based on quantiles of this variable. Each group will be assigned
a different vertex shape, making it clear which nodes belong to which
category. This approach enhances the interpretability of the network by
allowing you to visually identify nodes with similar attributes or
characteristics.

``` r
## All shape forms
shapes <- c(
  'circle',
  'square',
  'csquare',
  'rectangle',
  'crectangle',
  'vrectangle',
  'pie',
  'raster',
  'sphere'
)
V(g1)$Age <- rnorm(n, 30, 5)
q <- quantile(V(g1)$Age, c(0, .33, .66, 1))
ind <- cut(V(g1)$Age, q, include.lowest = T, labels = F)
shape <- ifelse(ind==1, 'csquare', ifelse(ind==2, 'circle', 'sphere'))

plot(
  g1,
  vertex.size = 15,
  edge.arrow.size = .3,
  vertex.shape = shape,
  layout = layout_nicely
)
```

<img src="https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-41-1.png?raw=true" style="display: block; margin: auto;" />

### Setting colours of vertices and adding legends to plots

Generate a vector of attributes by sampling with replacement from a set
`Gender = {female, male}`, and set a new attribute to the graph called
gender. Also, add legends using the legend function and pass the desired
arguments.

``` r
V(g1)$gender <- sample(c("male", "female"), n, replace = T)

plot(
  g1,
  vertex.size = 15,
  vertex.color = ifelse(V(g1)$gender == "male", "light blue", "pink"),
  edge.arrow.size = .3,
  vertex.shape = shape,
  layout = layout_nicely
)

legend(
  # Position
  x = -1.5,
  y = -1.1,
  # Legends
  c("male", "female"),
  # Mark type (circle)
  pch = 21,
  col = 1,
  pt.bg = c("light blue", "pink"),
  pt.cex = 2,
  cex = .8,
  bty = "n",
  ncol = 1
)
```

![](https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-42-1.png?raw=true)<!-- -->

### Setting colours to groups of vertices

We can emphasize groups of vertices in the graph. Find the vertex with
the highest degree centrality and mark the adjacent vertices in a group.

``` r
class <- adjacent_vertices(g1, which.max(degree(g1)), mode = c("all"))
plot(
  g1,
  vertex.size = 15,
  vertex.color = ifelse(V(g1)$gender == "male", "light blue", "pink"),
  edge.arrow.size = .3,
  vertex.shape = shape,
  layout = layout_nicely,
  mark.groups = class,
  mark.col = rainbow(length(class))
)
```

![](https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-43-1.png?raw=true)<!-- -->

### Set colours and thickness to edges

``` r
g1 <- graph.data.frame(data.frame(
  from = c('A', 'A', 'A', 'A', 'B', 'B', 'C', 'D', 'E', 'F'),
  to = c('B', 'C', 'D', 'E', 'C', 'E', 'D', 'E', 'F', 'G')
), directed = F)

# and plot it:
cl <- cliques(g1, min = 3, max = 3)
c.ed <- lapply(cl, function(x)
  E(g1, path = c(x, x[1])))
plot(g1,
  layout = layout.star,
  edge.width = edge.betweenness(g1),
  edge.color = ifelse(E(g1) %in% unlist(c.ed), "red", "gray"))
```

![](https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-44-1.png?raw=true)<!-- -->

### Subgraphs

Find the vertices adjacent to the vertex A and then plot a subgraph of
the neighborhood.

``` r
g1 <- graph.data.frame(data.frame(
  from = c('A', 'A', 'A', 'A', 'B', 'B', 'C', 'D', 'E', 'F'),
  to = c('B', 'C', 'D', 'E', 'C', 'E', 'D', 'E', 'F', 'G')
), directed = F)

# Find the vertices adjacent to A
v <- 'A'
neig.a <- adjacent_vertices(g1, v, mode = c("all"))

# Subgraph the neighborhood of A
g2 <- induced.subgraph(g1, c(v, names(neig.a[[1]])))

# Plot the Graphs
par(mfrow = c(1, 2))
plot(g1)
plot(g2)
```

![](https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-45-1.png?raw=true)<!-- -->

## Network Statistics

### Local Clustering

Local clustering of a vertex $v$ is the ratio of the number of
3-cliques, or triangles, that fall in to $v$ and the number of connected
triplets from which two edges are incident to $v$. For instance, for
vertex $A$, the number of triangles, is defined as the cardinality of
the set of vertices $\Delta_{A}=\{(A,C,B), (A,C,D), (A,D,E), (A,E,D)\}$.
Similarly the number of connected triplets is the set
$T=\{(A,C,B), (A,C,D), (A,D,E), (A,E,D), (C,A,E), (D,A,B) \}$. The local
clustering coefficient $C_{A}=\frac{|\Delta_{A}|}{|T|}=\frac{2}{3}$. The
local clustering is not defined for topologies, such as *stars*,
*trees*, *lattices*.

``` r
 g <-
    graph.data.frame(data.frame(
    from = c('A', 'A', 'A', 'A', 'B', 'B', 'C', 'D'),
    to = c('B', 'C', 'D', 'E', 'C', 'E', 'D', 'E')
    ), directed = F)

    #Graph
    plot(g, layout = layout.star)
```

![](https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-46-1.png?raw=true)<!-- -->

``` r
    #Transitivity of A
    transitivity(g, v = "A", "local")
```

    ## [1] 0.6666667

``` r
    transitivity(graph.lattice(5), "local")
```

    ## [1] NaN   0   0   0 NaN

``` r
    transitivity(graph.star(5, mode = "undirected"), "local")
```

    ## [1]   0 NaN NaN NaN NaN

``` r
    transitivity(graph.tree(5, mode = "undirected"), "local")
```

    ## [1]   0   0 NaN NaN NaN

### Degree and Strength

Add two new edges to the graph, from to , and from to , and plot the
graph. Compare the measurements of and for the vertex $A$, notice that
the vertices adjacent to are $\{B,C,D,E)\}$ but both measurements have a
value of $7$. Simplify the graph, remove multiples edges and loops, and
compute the `degree` centrality. Finally, use the `count\_multiple`
function to compute weights for each edge in the graph and calculate
`strength` centrality one more time.

``` r
    g <- graph.data.frame(data.frame(
      from = c('A', 'A', 'A', 'A', 'B', 'B', 'C', 'D'),
      to = c('B', 'C', 'D', 'E', 'C', 'E', 'D', 'E')
      ), directed = F)

    # Add edge
    g <- add_edges(g, c('A', 'B', 'A', 'A'))

    # Plot the graph
    plot(g)
```

<img src="https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-47-1.png?raw=true" style="display: block; margin: auto;" />

``` r
    # Degree vs Strength
    degree(g, V(g)$name == 'A', mode = 'all')
```

    ## A 
    ## 7

``` r
    strength(g, V(g)$name == 'A', mode = 'all')
```

    ## A 
    ## 7

``` r
    # Simplify Degree
    degree(simplify(g, remove.multiple = T, remove.loops = T),
    V(g)$name == 'A',
    mode = 'all')
```

    ## A 
    ## 4

``` r
    # Strength with Weights
    E(g)$weight <- count_multiple(g)
    g <- simplify(g)
    strength(g, V(g)$name == 'A', mode = 'all')
```

    ## A 
    ## 7

### Eigenvector Centrality

The intuition of is to capture the importance of the neighborhood of
each vertex. Vertices who are connected to adjacent vertices with higher
degree centrality will perform better in this measurement. The interest
lies in finding a vector that represents a ranking of relative
importance for each vertex. This is similar to finding a solution for
the eigenvalue problem.

$$Aw = \lambda w$$

Suppose that we can assign equal weights $w_1$, to each vertex, and then
perform $Aw_1=w_2$, similar to computing a weighted degree. Then use
$w_2$ to perform $n$ iterations till difference between
$Aw_{n} - \lambda w_{n+1}$ gets closer to zero. Run a algorithm of
[eigenvector
centrality](https://www.sci.unich.it/~francesc/teaching/network/eigenvector.html)
and compare the results with the function.

``` r
# graph: 
    g <- graph.data.frame(data.frame(
      from = c('A', 'A', 'A', 'A', 'B', 'B', 'C', 'D'),
      to = c('B', 'C', 'D', 'E', 'C', 'E', 'D', 'E')
      ), directed = F)

# Eigen vector centrality algorithm    
eigenvector.centrality = function(g, t=7) {
  A = get.adjacency(g)
  n <- nrow(A)
  #Degree
  # w <- max(A%*%rep(1, n))
  w <- n
  #Create a vector of weights
  x1 <- rep(1/w, n)
  #Create a vector of zeros (for the initial interation)
  x0 <- rep(0, n)
  #Presicion of the computation
  pre <- 1/10^t
  #Index of interaction
  iter <- 0
  while ( sum(abs(x0 - x1)) > pre) {
    #Store the current weight for comparison in the next interaction
    x0 <- x1
    #Compute a weighted degree
    x1 <- as.vector(A %*% x1)
    #Get the biggest weight
    w <- x1[which.max(abs(x1))]
    #Get a new vector of weights
    x1 <- x1 / w
    #Save the interations
    iter <- iter + 1
  }
  return(list(vector = x1, value = w, iter = iter))
}

#Compute eigenvector centrality scores
eigen_centrality(g)$vector
```

    ##        A        B        C        D        E 
    ## 1.000000 0.809017 0.809017 0.809017 0.809017

``` r
eigenvector.centrality(g, 7)$vector
```

    ## [1] 1.000000 0.809017 0.809017 0.809017 0.809017

### Weighted Measurements of centrality

The [](https://cran.r-project.org/web/packages/tnet/tnet.pdf) package
has implementations of weighted versions of , and . Lets generate a
graph of $n$ vertices and, compare the difference between the weighted
and unweighted centrality measurements.

``` r
  n <- 20
    # Generate an undirected weighted graph
    w <- matrix(0L, nrow = n, ncol = n)
    
    # Squewed distributon
    val <- rnbinom(sum(upper.tri(w)), prob=1/5, size = 1)
    w[upper.tri(w)] <- val
    w <- w + t(w)
    g_w <- as.tnet(w, type = 'weighted one-mode tnet')
    g_w.1 <- graph_from_adjacency_matrix(w)
    E(g_w.1)$weight <- count.multiple(g_w.1)

    # Generate an undirected unweighted graph
    uw <- matrix(0L, nrow = n, ncol = n)
    uw[w > 0] <- 1
    g_uw <- graph_from_adjacency_matrix(uw, mode = 'undirected')
    # Strength
    st <- strength(g_w.1)
    d <- degree(g_w.1)
    dw <- degree_w(g_w)
      
    # Betweeness
    bu <- betweenness(g_uw)
    bw <- betweenness_w(g_w)
    
    # Closeness
    cu <- closeness(g_uw)
    cw <- closeness_w(g_w)
    out <-
    data.frame(
    vertex = 1:n,
    degree = d,
    w.degree = dw[,3],
    strength = st,
    betweenness = bu,
    w.betweenness = bw[, 2],
    closeness = cu,
    w.closeness = cw[, 3]
    )
    
   kable(out, format = "markdown")
```

| vertex | degree | w.degree | strength | betweenness | w.betweenness | closeness | w.closeness |
|-------:|-------:|---------:|---------:|------------:|--------------:|----------:|------------:|
|      1 |    136 |       68 |     1360 |    2.104459 |             7 | 0.0400000 |   0.0027701 |
|      2 |    206 |      103 |     3390 |    2.850419 |            29 | 0.0400000 |   0.0033045 |
|      3 |    142 |       71 |     1310 |    3.630675 |             6 | 0.0434783 |   0.0024859 |
|      4 |    132 |       66 |     1664 |    1.697183 |             7 | 0.0384615 |   0.0029117 |
|      5 |    144 |       72 |     1240 |    2.774312 |             9 | 0.0434783 |   0.0027380 |
|      6 |     84 |       42 |      496 |    2.129892 |             0 | 0.0384615 |   0.0022731 |
|      7 |    104 |       52 |      476 |    4.233103 |             1 | 0.0454545 |   0.0020333 |
|      8 |    148 |       74 |     1496 |    1.338850 |            13 | 0.0370370 |   0.0027492 |
|      9 |    130 |       65 |      762 |    2.880625 |             1 | 0.0434783 |   0.0023273 |
|     10 |    180 |       90 |     3248 |    3.568456 |            18 | 0.0434783 |   0.0031294 |
|     11 |    194 |       97 |     2246 |    3.685820 |            21 | 0.0454545 |   0.0032645 |
|     12 |    116 |       58 |     1212 |    2.174228 |             3 | 0.0384615 |   0.0022673 |
|     13 |     86 |       43 |      590 |    1.078691 |             0 | 0.0370370 |   0.0024054 |
|     14 |    144 |       72 |      988 |    4.050985 |             8 | 0.0434783 |   0.0028601 |
|     15 |     88 |       44 |      404 |    1.909510 |             0 | 0.0384615 |   0.0020143 |
|     16 |    126 |       63 |      822 |    4.247017 |             1 | 0.0454545 |   0.0025134 |
|     17 |    162 |       81 |     1314 |    1.615571 |            18 | 0.0384615 |   0.0033866 |
|     18 |    178 |       89 |     2278 |    2.254387 |            16 | 0.0400000 |   0.0032046 |
|     19 |    104 |       52 |      644 |    1.613647 |             5 | 0.0384615 |   0.0025963 |
|     20 |    196 |       98 |     2500 |    4.162168 |            32 | 0.0454545 |   0.0032223 |

### Structural Holes

Structural Holes are separations between groups observed from
discontinuities in network structure. The absence of structural holes
signals saturation in the capacity of individuals(vertices) to create
novel connections outside their group. Saturation occurs when
individuals reach a limit on the number of connections they can create
and maintain. When individual’s resources are concentrated in a single
group structural holes are absent or scare. The scarcity of holes
represent constraints to collaborate outside a single research team that
leads to redundancy of information and inability to capitalize novel
ideas from different research teams.

``` r
g <- graph.data.frame(data.frame(
  from = c('A', 'A', 'A', 'A', 'B', 'B', 'C', 'D', 'E', 'F'),
  to = c('B', 'E', 'F', 'G', 'D', 'G', 'G', 'G', 'G', 'G')
), directed = F)


plot(g)
```

![](https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-50-1.png?raw=true)<!-- -->

``` r
A <- as.matrix(get.adjacency(g))
kable(A, format = "markdown")
```

|     |   A |   B |   C |   D |   E |   F |   G |
|:----|----:|----:|----:|----:|----:|----:|----:|
| A   |   0 |   1 |   0 |   0 |   1 |   1 |   1 |
| B   |   1 |   0 |   0 |   1 |   0 |   0 |   1 |
| C   |   0 |   0 |   0 |   0 |   0 |   0 |   1 |
| D   |   0 |   1 |   0 |   0 |   0 |   0 |   1 |
| E   |   1 |   0 |   0 |   0 |   0 |   0 |   1 |
| F   |   1 |   0 |   0 |   0 |   0 |   0 |   1 |
| G   |   1 |   1 |   1 |   1 |   1 |   1 |   0 |

To calculate the constraints to bridge structural holes, the first step
is to calculate, $i$, individual proportion of resources allocated to
$j$ connections.

$$
p_{ij} = z_{ij} / z_{iq}
$$

``` r
# degree for undirected (Sum of resources spend in each connection)
d <- (A * upper.tri(A)) %*% matrix(1, nrow = nrow(A), ncol = 1)

# Matrix of degree
D <- matrix(rep(d, ncol(A)), nrow = nrow(A), ncol = ncol(A))

#  Matrix of time and enery invested on others z_iq = d - z_ij
z_iq <- (D * upper.tri(D)) - (A * upper.tri(A))

# Matrix of proportion of i's time an energy allocated to j's connections.
P <- (A * upper.tri(A))/z_iq
```

### Redundancy of Centrality in Complete graphs

There are some cases in which the measurements of centrality will not
provide relevant information. For instance, if the structure of an
undirected network approaches a complete graph, each pair of different
vertices is connected by a unique edge
$\forall \{i \neq j\}:E(v_i,v_j)=1$, then the centrality measures will
not yield relevant information. Take into consideration the following
example, where I generate a fully connected graph:

``` r
## Creating Adjacency Matrix
A <- matrix(rep(1,25), ncol = 5, nrow = 5) 
diag(A) <- 0
G <- graph_from_adjacency_matrix(A, mode = "undirected")

## Creating the 
cols <- data.frame(
    degree(G),
    closeness(G),
    constraint(G),
    transitivity(G, type = 'local'),
    eigen_centrality(G)$vector,
    betweenness(G)
  )


colnames(cols) <- gsub("\\.G\\..*", "", colnames(cols))

kable(cols,  format = "markdown")
```

| degree | closeness | constraint | transitivity | eigen_centrality | betweenness |
|-------:|----------:|-----------:|-------------:|-----------------:|------------:|
|      4 |      0.25 |   0.765625 |            1 |                1 |           0 |
|      4 |      0.25 |   0.765625 |            1 |                1 |           0 |
|      4 |      0.25 |   0.765625 |            1 |                1 |           0 |
|      4 |      0.25 |   0.765625 |            1 |                1 |           0 |
|      4 |      0.25 |   0.765625 |            1 |                1 |           0 |

To see more clearly the issue of redundancy of network measurements, I
have created this snipped of code with a simulation. The code calculates
the different network statistics keeping constant the number of edges
but increasing the number of connections until the network is fully
connected. In a nutshell the snipped, calculates network statistics for
networks with the same number of vertices but an increasing number of
connections
`conn <- c(seq(from=points, to=triag.matrix, by=round(triag.matrix/points)), triag.matrix)`.
Using a loop, we iterate this sequence sampling randomly the connections
in the `conn` sequence as follows: `sample(triag.matrix, conn[i])`.

``` r
#### Compute the average for each network centrality ####
n <- 100
triag.matrix <- ((n^2)-n)/2
points <-100
conn <- c(seq(from=points, to=triag.matrix, by=round(triag.matrix/points)), triag.matrix)
i <- 20
out.list <- list()
for(i in seq_along(conn)){
g <- matrix(0, ncol = n, nrow = n)  
val <- sample(triag.matrix, conn[i])
g[upper.tri(g)][val]<- 1
g <- t(g)+g
g <- graph_from_adjacency_matrix(g, mode = 'undirected')
t <- transitivity(g, type = 'localundirected')
t[is.na(t)]<- 0
out.list[[i]] <-
  data.frame(
    degree = mean(degree(g)),
    closeness = mean(closeness(g)),
    betweennes = mean(betweenness(g)),
    transitivity = mean(t),
    eigen.cent = mean(eigen_centrality(g)$vector),
    struc.holes = mean(constraint(g))
  )
}
```

Now that we have calculated the network statistics the goal of this
snippet is to plot the network statistics accordingly. Each plot shows
how a specific network statistic changes as the number of connections in
the network increases. The vertical axis represents the values of
various network statistics.The horizontal axis represents the number of
connections in the network as they increase gradually untill they reach
the fully connected graph.

As it becomes clear, when the connectivity level of the graph increases,
the network centrality measurements become more and more similar. The
results of this simulation suggest that network centrality measurements
become redundant as a graph approaches a fully connected network. This
is because all nodes in a fully connected network have the same
fundamental network structure.

``` r
out.data <- rbindlist(out.list)
rm(out.list)
par(mfrow = c(2, 3))

x <- 1:nrow(out.data)
for(j in 1:ncol(out.data)){
y <- out.data[[j]]
y[is.na(y)] <- 0
st <- sqrt(var(y))
plot (x, y, ylim=c(0,max(y)), main = colnames(out.data)[j] )
segments(x,y-st,x,y+st)
epsilon <- 0.02
segments(x-epsilon,y-st,x+epsilon,y-st)
segments(x-epsilon,y+st,x+epsilon,y+st)

}
```

![](https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-54-1.png?raw=true)<!-- -->

## Network analysis with Data

In this code snippet, you will learn how to perform a basic network
analysis on a real-world dataset. We start by downloading a network
dataset, specifically the “ca-netscience” dataset, from an online
source. This dataset represents a co-authorship network in the field of
network science.

The code proceeds to unzip and load the dataset into R. We then
construct a graph from the dataset using the igraph package,
representing the relationships between authors. And finally, we
calculate various network metrics such as degree centrality, closeness
centrality, betweenness centrality and other network statistics.

I encourage you to explore similar datasets on the [Stanford Large
Network Dataset Collection](https://snap.stanford.edu/data/) and the
[NetworkRepository](http://networkrepository.com/), they have a wide
range of sample empirical data for your analyses.

``` r
# Download network data
 # setwd('C:/r_tutorial') 
# Data from: https://arxiv.org/abs/physics/0605087    
 download.file('http://nrvis.com/download/data/ca/ca-netscience.zip',
                  destfile = 'ca-netscience.zip')
 unzip('ca-netscience.zip')
 g <- read.csv('ca-netscience.mtx', sep = " ", header = F, skip = 2)
 g <- graph_from_data_frame(g, directed = F)
 E(g)$weight <- count.multiple(g)

 # Perform a basic network analysis (degree, closeness, betweenness, 
 # transitivity, eigenvector.centrality)
 # Store the results in a data.frame for analysis, add a column of ids. 
 
 na <- data.frame(
    id = V(g)$name,
    closeness = closeness(g, mode = "all", normalized = F),
    degree = degree(g, mode = "all", normalized = F, loops = F),
    strength= strength(g),
    betweenness = betweenness(g, directed = F, normalized = F),
    struc_hole = constraint(g),
    transitivity = transitivity(g, "localundirected"),
    eigen_centrality= eigen_centrality(g, scale = F)$vector)
 
kable(na[1:10,],  format = "markdown")
```

|     | id  | closeness | degree | strength | betweenness | struc_hole | transitivity | eigen_centrality |
|:----|:----|----------:|-------:|---------:|------------:|-----------:|-------------:|-----------------:|
| 2   | 2   | 0.0004627 |      2 |        2 |       0.000 |  0.8650000 |    1.0000000 |        0.0148383 |
| 3   | 3   | 0.0004627 |      2 |        2 |       0.000 |  0.8650000 |    1.0000000 |        0.0148383 |
| 4   | 4   | 0.0005643 |     34 |       34 |   10834.473 |  0.0955073 |    0.1336898 |        0.4142993 |
| 5   | 5   | 0.0006075 |     27 |       27 |   17858.003 |  0.1071098 |    0.1823362 |        0.3562072 |
| 16  | 16  | 0.0005211 |     21 |       21 |    1131.347 |  0.1690397 |    0.2761905 |        0.3464503 |
| 44  | 44  | 0.0005882 |      4 |        4 |   12460.579 |  0.2941086 |    0.5000000 |        0.0885522 |
| 113 | 113 | 0.0005033 |     15 |       15 |    4601.692 |  0.1901735 |    0.2571429 |        0.0222461 |
| 131 | 131 | 0.0004760 |     12 |       12 |    3238.339 |  0.2118647 |    0.3333333 |        0.0213000 |
| 250 | 250 | 0.0005089 |      6 |        6 |      13.200 |  0.3374061 |    0.8666667 |        0.1470503 |
| 259 | 259 | 0.0004735 |      3 |        3 |       0.000 |  0.4537654 |    1.0000000 |        0.0176052 |

## Community Detection

Lastly, I would like to show you how to perform a basic community
detection analysis. Community detection in network analysis is the
process of identifying groups or communities of nodes within a network
that are more densely connected to each other than to nodes outside
their community. These communities represent subsets of nodes which may
possess similar characteristics, functions, or roles within the network.

Here’s a brief explanation of some community detection methods available
in `igraph`:

`edge.betweenness.community`: This method identifies communities based
on edge betweenness centrality. It removes edges with the highest
betweenness values iteratively, eventually breaking the network into
communities.

`fastgreedy.community`: It uses a greedy optimization approach to find
hierarchical communities by optimizing modularity, a measure of
community structure quality.

`infomap.community`: This method employs the Infomap algorithm, which
treats the network as a flow of information and detects communities by
minimizing the expected description length of the information flow.

`label.propagation.community`: Nodes are assigned labels, and
communities form based on the propagation of these labels through the
network. It’s a simple and fast method.

`leading.eigenvector.community`: This approach uses spectral graph
theory and the leading eigenvector of the network’s adjacency matrix to
detect communities.

`multilevel.community`: It’s a multilevel algorithm that optimizes
modularity by moving nodes between communities, iteratively improving
the community structure.

`spinglass.community`: This method is based on spin glass models from
statistical physics, which maximize a Hamiltonian function to find
communities.

`walktrap.community`: It uses random walks to find communities by
detecting nodes that are more likely to be visited together during
random walks on the network.

For this example I will use the same data as the previos snipped.

``` r
comms <- c("edge.betweenness.community", "fastgreedy.community", "infomap.community",
"label.propagation.community", "leading.eigenvector.community",
"multilevel.community", "spinglass.community",
"walktrap.community")

V(g)$frame.color <- "white"
V(g)$label <- ""
E(g)$arrow.mode <- 0

plot.comm <- function(comm){
V(g)$color <- colors37[get(comm)(g)$membership]
l <- qgraph.layout.fruchtermanreingold(get.edgelist(g, names = F), vcount=vcount(g),
      area=8*(vcount(g)^2),repulse.rad=(vcount(g)^3.1))
plot(g,layout=l,vertex.size=5, main= comm)
}

invisible(lapply(comms, plot.comm))
```

![](https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-56-1.png?raw=true)<!-- -->![](https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-56-2.png?raw=true)<!-- -->![](https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-56-3.png?raw=true)<!-- -->![](https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-56-4.png?raw=true)<!-- -->![](https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-56-5.png?raw=true)<!-- -->![](https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-56-6.png?raw=true)<!-- -->![](https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-56-7.png?raw=true)<!-- -->![](https://github.com/Wario84/blog/raw/main/assets/imgs/2023-09-14-intro_net_anlysis_R/unnamed-chunk-56-8.png?raw=true)<!-- -->
