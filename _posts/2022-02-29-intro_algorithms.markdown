---

layout: post
title: "Introduction to Algorithms"
author: "Mario H. Gonzalez-Sauri"
date: "2022-03-27"
mermaid: true
---

# Introduction

In lectures one to four, we have set the stage to introduce the heart of Applied Data Science: algorithmic thinking for problem-solving. In lecture one, we learn about the scope of Data Science and the rise of Big Data. Lecture two, is an introduction to the use of inductive reasoning applied to Data Science. Lectures three and four are an overview on basic estimation using statistics and econometrics applied with **R** Programming. In this lecture, I cover another pillar of Data Science: Algorithm programming using *control flow structures* and *functions*.

Functions and control flow structures are the building blocks of algorithm programming. So far, we have use `r-packages` and more specifically `FUN(X)` functions, that take arguments and perform certain action. However, in this lecture, we will learn the elementary building blocks from algorithmic programming. Learning the elementary building blocks of algorithmic programming has two main advantages in your formation in Data Science. Firstly, algorithmic programming allows you to understand in detail how the functions work. I’m sure that thus far, you know that if we pass a numeric vector `x`, inside the function`mean(x)`, **R** somehow computes the mean. However, after learning the building blocks of algorithmic programming, we are going to be able to understand how the functions work. What is the series of steps behind the computation of certain functions? And how do the arguments of the function being used, in which order? In a nutshell, algorithmic programming enables you to deeply understand functions and packages in **R**.

The second advantage of algorithmic programming is that enables you to go beyond the "out-of-the-shelf" functions from the **R-base** and other packages. Indeed, instead of being bound to only functions from the **R-base**  and other packages, algorithmic programming, gives you the tools to create your own functions. In general, is recommended to search first if there are no functions available to perform the action that you want. But, knowing algorithmic programming removes the constraints of only using available tools and gives you the freedom of developing tools that fulfil your particular needs. Indeed, we would like to build our own functions and algorithms in two cases. Firstly, when we can’t find a similar function in [The R Base](https://stat.ethz.ch/R-manual/R-devel/library/base/html/00Index.html) or in the packages maintained by [The Comprehensive R Archive Network (CRAN)](https://cran.r-project.org/web/packages/available_packages_by_name.html). Especially, if this is your first course in Data Science, you would like to verify first if there is a function on CRAN that fulfils your needs before investing time building your own function. Using a function from CRAN’s database is typically a better option, not only because we save time, but also because the code is audited by lead experts in their corresponding fields. Secondly, we may opt to build our own function when we often perform a sequential series of functions or repetitive steps. For instance, I typically use the function `lapply` combined with the function `class` to verify the class of each column from a `df` (`data.frame`) in the following manner `lapply(df, class)`.

# What is an algorithm?


An algorithm is simply a "well-defined computational procedure that takes some value, or set of values, as input and produces some value, or set of values, as output" [@cormen2022introduction]. Indeed, an algorithm serves a specific purpose and has a specific procedure designed to solve a problem. Before we start learning the necessary syntax to produce algorithms in **R**, we are going to understand the structure (procedure) of examples of algorithms employing pseudo-code or flow diagrams. Later, in a second step, we will revise the specific R-code that we need to produce the algorithm in **R**.


## Example 1: Fibonacci Sequence

> Input: A variable `x` that is the number of numbers to generate in the Fibonacci serie.

> Output: A series `z` that is the Fibonacci serie of lenght `x`.

<!-- [![](https://mermaid.ink/img/pako:eNpdkEFrwzAMhf-K0CmF9rJjYB1tskMvGzS7rMsOXqy0gdhObRkakvz32W0CYzpJz5_fExqwMpIwxbMV3QU-8lJDqN3XQXee4ZaC9uqHLJh67hywgTNpsoLpGzab7ViwsDzCPim8Ar4QtMIxPC0fVg_PfUAhS3ZS3pnZN5jFyZFtaCGzSOZJZrzm-2sf45dM-c83j_RpODi4wXP_Mj3UU1THt_ewFvxVPsmNcEyOxN7qOfrqSVe0ghnENSqySjQy3GWIWokBVFRiGlpJtfAtl1jqKaC-k2GpV9mwsZjWonW0RuHZFL2uMGXraYHyRoQzq5mafgEpe3o8)](https://mermaid-js.github.io/mermaid-live-editor/edit#pako:eNpdkEFrwzAMhf-K0CmF9rJjYB1tskMvGzS7rMsOXqy0gdhObRkakvz32W0CYzpJz5_fExqwMpIwxbMV3QU-8lJDqN3XQXee4ZaC9uqHLJh67hywgTNpsoLpGzab7ViwsDzCPim8Ar4QtMIxPC0fVg_PfUAhS3ZS3pnZN5jFyZFtaCGzSOZJZrzm-2sf45dM-c83j_RpODi4wXP_Mj3UU1THt_ewFvxVPsmNcEyOxN7qOfrqSVe0ghnENSqySjQy3GWIWokBVFRiGlpJtfAtl1jqKaC-k2GpV9mwsZjWonW0RuHZFL2uMGXraYHyRoQzq5mafgEpe3o8) -->


<div>
 <script src="https://cdn.jsdelivr.net/npm/mermaid/dist/mermaid.min.js"></script>
    Fibonacci Sequence Generator:
    <div class="mermaid">
    graph TD
    A[Input x: lenght of sequence to generate] -->|Start| B(Sum the last 2 numbers)
    B--> C(Add the number to the series z)
    C--> D(Count the y of generated numbers)
    D--> Z{Is x = y?}
    Z--> |NO| B
    Z--> |Yes| R(Return the sequence z)
    </div>
</div>
<br>

# Flow controls: `while` and `if` 

To implement the algorithm in Example one, we need to expand our knowledge of **R** operators. The operator `if` and `while` are always followed by a `(...)` that assesses a logical condition and some `{...}` brackets that perform a set of actions, `...` if the condition is fulfilled. For instance, in Example 1, the input of the algorithm is a variable `x` that defines the number of elements to generate in the sequence. The output of the algorithm is a sequence `z` that has `y` number of elements. To generate the series we need to add one number to the series `z` that corresponds to the sum of the last two elements of the previous series until the total length is `y`. To start the algorithm we need the variable `x` that inputs the number of values to generate in the series `z`. followed by `y` which is the initial value of the length of `z`. Assuming that the user is going to request more than two numbers in the series then `y>2` (Requesting less than two numbers makes the algorithm redundant).

Next, the algorithm needs to be programmed to continue doing a series of steps until the goal is reached. Remember that the goal is to produce a series `z` that has a total length of `x`. Notice that `y` is then the actual number of elements in the series `z` in each iteration of the process of adding one element to the series. To operationalize the algorithm we are going to use `while(y<x){...}`, which assesses the condition where `y<x`. The operator will perform the set of actions `...` only while the condition is satisfied `y<x`. That means that the algorithm using `while` stops when `y>=x` (when the corresponding series `z` has a total length of `x` or more).



```{r}

x <- 20L
y <- 0L
z <- c(0L, 1L)

while (y < x) {
    z[length(z) + 1L] <- sum(z[c(length(z) - 1L, length(z))])
    y <- length(z)
}
z

```

## Example 2: Sorthing Algorithm


> Input: A variable $$x={a_1, a_2, \dots, a_n}$$ of `n` rational numbers.

> Output: A permutation (reordering) of `x` called `y` such that $$y={a_1^*, a_2^*, \dots, a_n^*}$$

*Source: (Cormen, Leiserson, Rivest, and Stein, 2022).*




<!-- [![](https://mermaid.ink/img/pako:eNpdkc1uwjAQhF9l5EtAIof0GIlULfSAVLUHuISmqlyyAUNiR_4pQYR3r5OAVGofbO9-s6Ndn9lG5cRiBr-2mtc7rOaZ7F5PHwtZO4smBochLQiqgOZWKMlLSFd9kzYoSW7tDvITYZi0S8u1bfE8WvEDIZDJdJ9EAQqtKgRNAC5zGKs0QVgIieBAp2A8GD53FTAbvapNb9LZ2R2h1vQjlLk6xgjEdB9GN9WsV63PC4PmSyAcaGdCJPDFEUpqbIhHXAZ-3fNtSqZFGo2WR17fC3EUvp8_0qtRGnlh-jAofLrPDvA_4_Gd09u7n0cmu91FbyebsIp0xUXup3_uYhnz3VaUsdhfcyq4K23GMnnxqKtzbuklF352LC54aWjCuLNqeZIbFlvt6AbNBfcfWV2pyy-iLJg9)](https://mermaid.live/edit#pako:eNpdkc1uwjAQhF9l5EtAIof0GIlULfSAVLUHuISmqlyyAUNiR_4pQYR3r5OAVGofbO9-s6Ndn9lG5cRiBr-2mtc7rOaZ7F5PHwtZO4smBochLQiqgOZWKMlLSFd9kzYoSW7tDvITYZi0S8u1bfE8WvEDIZDJdJ9EAQqtKgRNAC5zGKs0QVgIieBAp2A8GD53FTAbvapNb9LZ2R2h1vQjlLk6xgjEdB9GN9WsV63PC4PmSyAcaGdCJPDFEUpqbIhHXAZ-3fNtSqZFGo2WR17fC3EUvp8_0qtRGnlh-jAofLrPDvA_4_Gd09u7n0cmu91FbyebsIp0xUXup3_uYhnz3VaUsdhfcyq4K23GMnnxqKtzbuklF352LC54aWjCuLNqeZIbFlvt6AbNBfcfWV2pyy-iLJg9) -->


<div>
 <script src="https://cdn.jsdelivr.net/npm/mermaid/dist/mermaid.min.js"></script>
    Sorting Algorithm
    <div class="mermaid">
    graph TD
    A[Input x: a series of rational numbers length n] -->|Start| B(Take 'n>=j>1' from 'x' and store it in 'key')
    B --> C(Location of the previous number: 'i=j-1')
    C --> Z{Is x_i -previous- > key -next- ? }
    Z --> |Yes| Y1(Swap x_i -previous with key -next- )
    Y1-->Y2(Swap key-next with x_i -previous- )
    Z --> |NO| B
    </div>
</div>
<br>

## `for` loop

The sorting algorithm of Example 2, takes a series `x` of unsorted rational numbers and using an iterative procedure (`for` loop) compares each value on the list with all other values in the series. Using an index of previous value `i` and next value `j` and a storing vector `key` the algorithm swaps places when a previous number `x[i]` is greater than the current number being compared (`key`). This algorithm performs the same action as the function `sort(x)` with the argument `decreasing = FALSE`. Therefore, the algorithm itself has no more purpose than learning how the `for` loop is being used in **R**. The most fundamental aspect of the `for` loop is that takes `n` values in a series to perform a list of steps in each iteration of the loop. In this case, the algorithm evaluates each number in the series `x` to verify if a previous number is bigger than the next number in the series `x[i]>x[j]`. If that is the case, the algorithm replaces (swaps) the previous number `x[i]` with the current number being evaluated `x[j]`


```{r}

# Unsorted
x <- sample(1L:99L, 15)
x

# sorted with the function
sort(x, decreasing = FALSE)

# iterative sorting algorithm
for(j in 2L:length(x)){
    key <- x[j]
    i <- j - 1
    while(i>0&&x[i]>key){ #previous number in the series (x[i]) is greater than next number (key)
        x[i+1] <-  x[i] #swap previous number (x[i]) with the next number (x[i+1])
        i <- i - 1 
        x[i + 1] <- key # swap next number (key) with previous number (x[i+1])
    }
}
# Sorted
x
```


## Example 3: Odds and Even numbers

This example is may have only a pedagogical application. The algorithm samples one random number  `sample(..., 1)` between one and `lim` to generate an `x` numeric series of length `y` of *even* or *odd* numbers.

> Input: A variable `lim` that defines the range of numbers to sample $$[1, lim]$$ and the length of the series to generate. Also, we need a binary variable to switch the series from  *even* to *odd* numbers.

> Output: A series `x` of *even* or *odd* numbers.


## `if`, `else` 

A good analogy to understand the dynamics of `if` and `else` operators is a choice or selection between a set of possible categories.

## Example 5: Choice Algorithm

Suppose you have a bag of candies with the following flavours: `c("orange", "lemon", "strawberry", "mango")`. Your preference is `lemon` above all and `strawberry` over `orange`, you dislike `mango`. Suppose that the bag contains `100` candies, and you are interested in how many candies you would need to take (by chance) before getting `3 lemon` candies in total?

> Input: A random sample `c` with repetition of size 100 of candies (the bag).

> Output: A series `x` of at least three lemon candies.

```{r}

candies <- c("orange", "lemon", "strawberry", "mango")

candy_bag <- sample(candies, 100L, replace = T)

lemon <- 0L
picks <- ""
c <- 1L



while(sum(picks=="lemon")<3){
  pick <- sample(candy_bag, 1L)
  if(pick=="lemon"){
    picks[c] <- pick
    c <- c + 1L
  }else if(pick=="strawberry"){
    picks[c] <- pick
    c <- c + 1L
  }else if(pick=="orange"){
    picks[c] <- pick
    c <- c + 1L
  }
  
}

# Number of picks
length(picks)

# Distribution of picks
library(ggplot2)
ggplot(as.data.frame(table(picks)), aes(x=picks, y = Freq)) +
  geom_bar(stat="identity")
```

## `Functions`


`FUN(...)`, functions make explicit the kind of input that we the algorithms need in the form of **arguments**. Functions can take `n=...` arguments as our implementation may require. As we mention before the operator `if(...)` evaluates a logical condition and it is the gatekeeper of a set of operations grouped within `{}` brackets. Finally, the `ifelse` and the `else` operators evaluate a set of logical conditions always after the first condition stated in the `if` operator. 


## Example 6: Even or Odd numbers
In the implementation of Example 6, the algorithm employs `if` and `else if` to select between an *odd* or *even* number. Instead of using a `for` loop, that has a deterministic number of iterations, the examples use a `while` to prevent the algorithm to stop before generating a series length `y` of even or odd numbers.

> Input: A random sample `lim` that generates 

> Output: A series `x` of at least three lemon candies.

```{r}

odd_even <- function(lim=100L, y=25L, even=TRUE){
    x <-  vector(mode = "numeric")
    i <- 1L
    while (length(x)<y) {
        n <- sample(1L:lim, 1L)
    if(even & n %% 2 == 0){
        x[i] <- n
        i <- i + 1L
    }else if(!even & n %% 2 != 0 ){
        x[i] <- n
        i <- i + 1L
    }}
  x  
}

# Generate 20 odd numbers between 1 and 1000L
odd_even(lim=1000L, y=20L, even = FALSE)

# Generate 20 even numbers between 1 and 50L
odd_even(lim=1000L, y=20L, even = TRUE)

```

## Example 7:  Randomized Hire-Assistant


Finally, example 7 employs previous control flows. Starts by assuming that there is a fixed supply of assistants in the labor market of data science. Further, it assumes that by a process of selection and interview their ability is explicit. Each candidate arrives at the interview randomly, and the goal is then to select the top candidate on a fixed number of interviews.


> Input: A vector of candidates `supply` with a vector `a` of ability. Additionally, a vector of `interviews` that contains the max number of interviews in each experiment.

> Output: A matrix `H` with i-rows hired assistant ability per j-column round of interviews. From this matrix, we are interested in estimating the total number of hires for each round of interviews, `c(150L, 250L, 1000L, 3000L, 5000L, 10000L, 15000L)`, 
 
The algorithm uses a `for` loop to perform an iterative selection of candidates using the vector `interviews`. Then selects a random sample of candidates `selected` for the interviews. Using a `while` operator each iteration continues to run until `length(selected)==0`. For each run, I sample one candidate for `interview` and remove it from the `selected` vector. Finally, using an `if(best<interview)` operator the algorithm hires a candidate if their ability is higher than the current best candidate.

```{r}
h <- 1L
supply <- 20000L
hires <- 0L
a <- runif(supply)
interviews <- c(150L, 250L, 1000L, 3000L, 5000L, 10000L, 15000L)

H <- matrix(NA, nrow = supply, ncol = length(interviews))

j <- 2L
for(j in seq_along(interviews)){
    selected <- sample(a, interviews[j]) #interview candidate
    h <- 1L
    best <- 0
    while(length(selected)!=0){
        i <- sample(1L:length(selected), 1)
        interview <- selected[i]
        selected <- selected[-i]
        
        if(best<interview){
        best <- interview
        H[h,j] <- interview
        h <- h + 1L
        }
        }
    }



# Total Hires
hires <-  colSums(!is.na(H))
names(hires) <- paste0(interviews)
hires

# Average Hiring Ability
ability <- colSums(H, na.rm = T)
avg_ability <- ability/hires
avg_ability

# Plot
plot(x=interviews, y=avg_ability)



```

# References


<div id="refs" class="references csl-bib-body hanging-indent">
<div id="ref-cormen2022introduction" class="csl-entry">
Cormen, T. H., C. E. Leiserson, R. L. Rivest, and C. Stein. 2022.
<em>Introduction to Algorithms, Fourth Edition</em>. MIT Press. <a href="https://books.google.nl/books?id=RSMuEAAAQBAJ">https://books.google.nl/books?id=RSMuEAAAQBAJ</a>.
</div>
</div>