---

layout: post
title: "Introduction to Descriptive Statistics using R."
author: "Mario H. Gonzalez-Sauri"
date: "2022-02-22"
mermaid: true

---

<!--  FORMAT: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet -->

# Introduction to Statistics for Data Science.

In the first lecture, we learn about the scope of Data Science and in lecture two, we set our minds to use inductive reasoning to analyze patterns in data. In this lecture,, we are going to build upon the last two lectures by giving a brief introduction to the powerhouse of Data Science: Statistic Using **R**.

## What is statistics?

Suppose you have a question, for instance, what is the proportion of international students in your university? What is the chance of passing a course in econometrics? What is the percentage of expats living in the Netherlands from Latin American origin?... To find an answer to any of these questions you probably will use your inductive reasoning and collect information from friends, the internet and your own experience. However, if you want to convince people that you have a solid answer for some question, you may want to collect some evidence. Namely, to put together or find a dataset suitable to answer your question in an objective manner. Statistics is simply the art of learning from data [(Ross, 2010)](https://www.sciencedirect.com/science/article/pii/B9780123743886000016). We use objective recollections of certain events to put together a dataset. Statistics is thus the set of methods that we use to answer questions from data.

## Descriptive and Inferential Statistics.

There are two kinds of questions that we can answer from data using statistics. One group of questions, uses  *descriptive statistics* to summarize facts from the given data. For instance, what is the frequency of late arrivals from Utrecht to Amsterdam by train? Which is the most popular song on the Radio? What is the chance of getting divorced after marriage? What is the average time of train arrival? The second group of questions makes use of *inferential statistics* to draw conclusions using the data about an underlying population. For instance, what is the effect of education on income? What is the effect of a vaccine on a variant of COVID-19? What is the change in the outcome variable for one unit of the dependent variable? The latter kind of questions are covered in [lecture 4](https://wario84.github.io/idsc_mgs/2022/02/22/w4_2_Lecture_04.html) where we dive into some basic inferential techniques, and we draw the line between correlation, causation and prediction.



# Samples, Population and Data Generation Process.

In Data Science and Statistics, it is crucial to distinguish between two different process. The first process is called,  **data generation process** is a higher level process that corresponds to certain **population**. The second process is called **data collection**, and it is concern on ways of collecting data from the population. The goal of Statistics is to use the sample to describe or draw conclusions about the population that remains hidden or latent. The population is the collection of all elements that we are interested. A simple example of these two processes are clearer if we reflect upon a *census*. The census is oriented towards collecting data about a population or certain country, region or state. The collective behavior of individuals in this population generates the data. A second process aims to collect the sample from the corresponding population. We use a sample, because almost impossible and costly to have data of all the individuals that belong to a country at every point in time. Even if the census have a good representation of the population, daily deaths and births of every day are very difficult to collect instantaneously.

## Parameters and Estimators

 In Statistics, we assume that there is a set of **population parameters** that we can estimate using samples called **estimators**. Because this course revolves around application rather than on theory, the following sections pay attention to the estimators rather than the parameters. What you have to keep in mind, is that the parameters remain hidden because they are the outcome of the data generation process from the population. Instead, what we observe is only the estimators from our sample, such as the measurements of central tendency, dispersion and association [(Next Section)](#Basics of Descriptive Statistics.). 
 
 
 When we talk about the parameters, we are talking in an abstract level about key values from our population that we are estimating from our sample. Don't get confused, a good way to get your mind around parameters and estimators is using your knowledge from the past lecture about *inductive reasoning*. The parameters are similar to deductive statements, because knowing the parameters (although almost impossible), it knows the estimators. However, statistics does not work in that way, most of the time we are confronted with the problem of estimating the parameters with samples from the population. Namely, we use *inductive* reasoning to calculate what could be the parameter from our samples, namely, the **estimators**. The following tables provide an overview of the common symbols used to describe the parameters and sample estimators.

<table border=1>
<caption align="top"> Table: Parameters vs Estimators </caption>
<tr> <th>  </th> <th> Parameter </th> <th> Estimator </th>  </tr>
  <tr> <td align="right"> Mean </td> <td>$$\mu_x=E[X]$$</td> <td> $$\bar{X}$$ </td> </tr>
  <tr> <td align="right"> Variance </td> <td> $$\sigma^2$$  </td> <td> $$S^2$$  </td> </tr>
  <tr> <td align="right"> Standard Dev. </td> <td>  $$\sigma$$ </td> <td> $$S$$ </td> </tr>
  <tr> <td align="right"> Covariance </td>  <td> $$\sigma_{XY}$$ </td> <td> $$S_{XY}$$ </td> </tr>
  <tr> <td align="right"> Correlation </td> <td> $$\rho_{XY}$$  </td> <td> $$R_{XY}$$ </td> </tr>
   </table>


## Types of Data

Not all variables are arranged in the same way. For instance, in a census, it makes sense to use discrete or whole numbers to describe the *number of household* members. Similarly, the inventories of companies producing items are filled with whole numbers; for instance, A manager shows 100 computers in the monthly production report. **Discrete Variables** are things that we can count. In **R**, this class of atomic element and variables is called `class = integer`. There are other type of variables that we approximate or measure, these are called **Continuous Variables**. For instance, we measure the temperature of every day, also we measure the GDP growth of a given country and the time of waking up every day. These variables are called `class = numeric` in **R**.


Then, we have also **Categorical** variables, this can be *binary* or also called *dummy* variables in economics, because they describe two mutually exclusive types or kinds. Categorical variables can also describe more than two levels of categories, and when they have order, then we call them *ordinal*. In the language of **R**, they are called `class = factor`. Aside from these 4 main kinds (discrete, continuous, categorical and ordinal), we have another kind called **Strings**, `class = string`. This type of data is not straightforward to analyze because contain alphanumeric characters that are not so easy to manipulate. In lecture 7, we will learn some techniques to manipulate and analyze strings.

To illustrate the kinds of data using **R**, let's explore the `cars` data set from the `ggplot2` package that contains characteristics of car models released between 1999 and 2008, you can read more about this data set [here](https://ggplot2.tidyverse.org/reference/mpg.html).

```
library(ggplot2)

data(mpg)
mpg_ <- mpg
mpg_ <- as.data.frame(unclass(mpg_), stringsAsFactors = TRUE)    # Convert all columns to factor

# Classes of each variable
sapply(mpg_, class)

# The first 20 observations of the mpg dataset
head(mpg, 10L)

```

<!-- html table generated in R 4.1.2 by xtable 1.8-4 package -->
<!-- Fri Mar 18 17:21:37 2022 -->
<table border=1>
<caption align="top"> Table: 5 </caption>
<tr> <th>  </th> <th> manufacturer </th> <th> model </th> <th> displ </th> <th> year </th> <th> cyl </th> <th> trans </th> <th> drv </th> <th> cty </th> <th> hwy </th> <th> fl </th> <th> class </th>  </tr>
  <tr> <td align="right"> 1 </td> <td> audi </td> <td> a4 </td> <td align="right"> 1.80 </td> <td align="right"> 1999 </td> <td align="right">   4 </td> <td> auto(l5) </td> <td> f </td> <td align="right">  18 </td> <td align="right">  29 </td> <td> p </td> <td> compact </td> </tr>
  <tr> <td align="right"> 2 </td> <td> audi </td> <td> a4 </td> <td align="right"> 1.80 </td> <td align="right"> 1999 </td> <td align="right">   4 </td> <td> manual(m5) </td> <td> f </td> <td align="right">  21 </td> <td align="right">  29 </td> <td> p </td> <td> compact </td> </tr>
  <tr> <td align="right"> 3 </td> <td> audi </td> <td> a4 </td> <td align="right"> 2.00 </td> <td align="right"> 2008 </td> <td align="right">   4 </td> <td> manual(m6) </td> <td> f </td> <td align="right">  20 </td> <td align="right">  31 </td> <td> p </td> <td> compact </td> </tr>
  <tr> <td align="right"> 4 </td> <td> audi </td> <td> a4 </td> <td align="right"> 2.00 </td> <td align="right"> 2008 </td> <td align="right">   4 </td> <td> auto(av) </td> <td> f </td> <td align="right">  21 </td> <td align="right">  30 </td> <td> p </td> <td> compact </td> </tr>
  <tr> <td align="right"> 5 </td> <td> audi </td> <td> a4 </td> <td align="right"> 2.80 </td> <td align="right"> 1999 </td> <td align="right">   6 </td> <td> auto(l5) </td> <td> f </td> <td align="right">  16 </td> <td align="right">  26 </td> <td> p </td> <td> compact </td> </tr>
  <tr> <td align="right"> 6 </td> <td> audi </td> <td> a4 </td> <td align="right"> 2.80 </td> <td align="right"> 1999 </td> <td align="right">   6 </td> <td> manual(m5) </td> <td> f </td> <td align="right">  18 </td> <td align="right">  26 </td> <td> p </td> <td> compact </td> </tr>
  <tr> <td align="right"> 7 </td> <td> audi </td> <td> a4 </td> <td align="right"> 3.10 </td> <td align="right"> 2008 </td> <td align="right">   6 </td> <td> auto(av) </td> <td> f </td> <td align="right">  18 </td> <td align="right">  27 </td> <td> p </td> <td> compact </td> </tr>
  <tr> <td align="right"> 8 </td> <td> audi </td> <td> a4 quattro </td> <td align="right"> 1.80 </td> <td align="right"> 1999 </td> <td align="right">   4 </td> <td> manual(m5) </td> <td> 4 </td> <td align="right">  18 </td> <td align="right">  26 </td> <td> p </td> <td> compact </td> </tr>
  <tr> <td align="right"> 9 </td> <td> audi </td> <td> a4 quattro </td> <td align="right"> 1.80 </td> <td align="right"> 1999 </td> <td align="right">   4 </td> <td> auto(l5) </td> <td> 4 </td> <td align="right">  16 </td> <td align="right">  25 </td> <td> p </td> <td> compact </td> </tr>
  <tr> <td align="right"> 10 </td> <td> audi </td> <td> a4 quattro </td> <td align="right"> 2.00 </td> <td align="right"> 2008 </td> <td align="right">   4 </td> <td> manual(m6) </td> <td> 4 </td> <td align="right">  20 </td> <td align="right">  28 </td> <td> p </td> <td> compact </td> </tr>
   </table>


Looking at this first 10 rows, we can tell that the `model` column is a *categorical* variable, the variable `trans` describes the year of the model, andit is a *discrete variable*. To have a better overview of each column class, we can run `sapply(mpg, class)`


<table border=1>
<caption align="top"> Table: 6 </caption>
<tr> <th>  </th> <th> manufacturer </th> <th> model </th> <th> displ </th> <th> year </th> <th> cyl </th> <th> trans </th> <th> drv </th> <th> cty </th> <th> hwy </th> <th> fl </th> <th> class </th>  </tr>
  <tr> <td align="right"> 1 </td> <td> factor </td> <td> factor </td> <td> numeric </td> <td> integer </td> <td> integer </td> <td> factor </td> <td> factor </td> <td> integer </td> <td> integer </td> <td> factor </td> <td> factor </td> </tr>
   </table>



In the next section, I define random variables and simulate the data generation process using R. Think of this random variables as your population, because they contain all the elements that we are interested in. Using **R**, I perform a simulated experiment that yields one or more realizations of a random variable to compute the frequency, the sample mean and the empirical probability.


# Basics of Descriptive Statistics.

This lecture covers different techniques to summarize and describe facts and patterns withing our data. First, we start with some methods to summarize data using tables.

## Frequency Tables

Frequency tables eliminate the redundancy of the values and present how often the values appear in the data set. First, let's give an example from a random variable $$X = \{A, B, \dots, J\}$$. I assume that each realization, letters from A-J, has equal chance of being selected, and sample $$n=100$$ with replacement. This sample is with replacement because the total number of elements in the sample space (10 letters) is smaller than the sample (100).


```

set.seed(7953)
# Sample 100 from the set 1 to 10.
n <- 100L
X <- sample(LETTERS[1:10], n, replace = T)

# Create a data.frame with the frequencies.
df <- as.data.frame(table(X))

# Add a column of the cumulative sum of the frequencies
df$cum_sum <- cumsum(df$Freq)

```

With the cumulative sum on the third column, we can observe that around 60% of the values in the series lie between $$[A-F]$$.

<table border=1>
<caption align="top"> Table: 7 </caption>
<tr> <th>  </th> <th> X </th> <th> Freq </th> <th> cum_sum </th>  </tr>
  <tr> <td align="right"> 1 </td> <td> A </td> <td align="right">   5 </td> <td align="right">   5 </td> </tr>
  <tr> <td align="right"> 2 </td> <td> B </td> <td align="right">   7 </td> <td align="right">  12 </td> </tr>
  <tr> <td align="right"> 3 </td> <td> C </td> <td align="right">  11 </td> <td align="right">  23 </td> </tr>
  <tr> <td align="right"> 4 </td> <td> D </td> <td align="right">  14 </td> <td align="right">  37 </td> </tr>
  <tr> <td align="right"> 5 </td> <td> E </td> <td align="right">  12 </td> <td align="right">  49 </td> </tr>
  <tr> <td align="right"> 6 </td> <td> F </td> <td align="right">   7 </td> <td align="right">  56 </td> </tr>
  <tr> <td align="right"> 7 </td> <td> G </td> <td align="right">  13 </td> <td align="right">  69 </td> </tr>
  <tr> <td align="right"> 8 </td> <td> H </td> <td align="right">  11 </td> <td align="right">  80 </td> </tr>
  <tr> <td align="right"> 9 </td> <td> I </td> <td align="right">  11 </td> <td align="right">  91 </td> </tr>
  <tr> <td align="right"> 10 </td> <td> J </td> <td align="right">   9 </td> <td align="right"> 100 </td> </tr>
   </table>


For *continuous variables*, we do not have differentiated intervals or breaks. Simply because of the continuous nature of the variable. For instance, let's define another random variable  $$Y = \{1-10\}$$ of real numbers (contains decimals and other rational numbers) with equal chance of being selected. Similarly, we sample only $$n=100$$ values.


```
set.seed(7953)
# Sample 100 from the set 1 to 10.
Y <- rep(seq(from=1, to=10, by=sample(1:10, 1)/10), 100L)
n <- 100L
Y_hat <- sample(Y, n)

# Create breaks to summarize the realizations
breaks = seq(1, 10, by=0.5)
Y_breaks = cut(Y_hat, breaks, right=FALSE) 

# Create a data.frame with the frequencies.
df <- as.data.frame(table(Y_breaks))

# Add a column of the cumulative sum of the frequencies
df$cum_sum <- cumsum(df$Freq)
```
From this frequency table summarizing a continuous variable we can observe that the $$60\%$$ of the values lie between $$[1-6)$$.

<!-- html table generated in R 4.1.2 by xtable 1.8-4 package -->
<!-- Fri Mar 18 15:35:54 2022 -->
<table border=1>
<caption align="top"> Table: 8 </caption>
<tr> <th>  </th> <th> Y_breaks </th> <th> Freq </th> <th> cum_sum </th>  </tr>
  <tr> <td align="right"> 1 </td> <td> [1,1.5) </td> <td align="right">  10 </td> <td align="right">  10 </td> </tr>
  <tr> <td align="right"> 2 </td> <td> [1.5,2) </td> <td align="right">   6 </td> <td align="right">  16 </td> </tr>
  <tr> <td align="right"> 3 </td> <td> [2,2.5) </td> <td align="right">   5 </td> <td align="right">  21 </td> </tr>
  <tr> <td align="right"> 4 </td> <td> [2.5,3) </td> <td align="right">   0 </td> <td align="right">  21 </td> </tr>
  <tr> <td align="right"> 5 </td> <td> [3,3.5) </td> <td align="right">   8 </td> <td align="right">  29 </td> </tr>
  <tr> <td align="right"> 6 </td> <td> [3.5,4) </td> <td align="right">  10 </td> <td align="right">  39 </td> </tr>
  <tr> <td align="right"> 7 </td> <td> [4,4.5) </td> <td align="right">   0 </td> <td align="right">  39 </td> </tr>
  <tr> <td align="right"> 8 </td> <td> [4.5,5) </td> <td align="right">  10 </td> <td align="right">  49 </td> </tr>
  <tr> <td align="right"> 9 </td> <td> [5,5.5) </td> <td align="right">   8 </td> <td align="right">  57 </td> </tr>
  <tr> <td align="right"> 10 </td> <td> [5.5,6) </td> <td align="right">   6 </td> <td align="right">  63 </td> </tr>
  <tr> <td align="right"> 11 </td> <td> [6,6.5) </td> <td align="right">   0 </td> <td align="right">  63 </td> </tr>
  <tr> <td align="right"> 12 </td> <td> [6.5,7) </td> <td align="right">  10 </td> <td align="right">  73 </td> </tr>
  <tr> <td align="right"> 13 </td> <td> [7,7.5) </td> <td align="right">   7 </td> <td align="right">  80 </td> </tr>
  <tr> <td align="right"> 14 </td> <td> [7.5,8) </td> <td align="right">   0 </td> <td align="right">  80 </td> </tr>
  <tr> <td align="right"> 15 </td> <td> [8,8.5) </td> <td align="right">   6 </td> <td align="right">  86 </td> </tr>
  <tr> <td align="right"> 16 </td> <td> [8.5,9) </td> <td align="right">   4 </td> <td align="right">  90 </td> </tr>
  <tr> <td align="right"> 17 </td> <td> [9,9.5) </td> <td align="right">  10 </td> <td align="right"> 100 </td> </tr>
  <tr> <td align="right"> 18 </td> <td> [9.5,10) </td> <td align="right">   0 </td> <td align="right"> 100 </td> </tr>
   </table>

## Frequency, Average and Probability.

Let's define the following random variable,  $$X = \{1,2, \dots, 6\}$$, that describes the *experiment* of rolling a die. Every time we roll a die is called an $$n$$-*trial* in the experiment of rolling the die $$X$$. And each trial has an outcome that is called *realization* of the random variable $$X$$.

The concept of *probability*, is defined with a *probability space* of an experiment that has three elements: $$(\Omega, \mathcal{F}, \mathcal{P})$$.

- $$\Omega$$ is a set that contains all possible outcomes of an experiment called *sample space*. For instance, in the experiment of rolling a die $$X$$, the sample space are all posible outcomes, namely, $$\Omega_X = \{1, 2, \dots, 6\}$$.
- $$\mathcal{F}$$ is set one or more *events* $$E$$ whose elements are subsets of $$\Omega$$ called *field*. Imagine the event of rolling a pair number $$E_1$$, the corresponding field $$\mathcal{F}_1 = \{ 2, 4, 6 \}$$.
- The last element of the probability space is $$\mathcal{P}$$, a function that maps the outcomes of events $$P(\mathcal{F}) \rightarrow [0,1]$$ with a corresponding measurement of uncertainty whose range is between 0 and 1.

I'm sure all this sounds very abstract to some of you. But that is precisely why I am explaining probability in this section, so you will build upon the use of the frequency table to understand the concept of probability and the average or mean. So we go back out our experiment $$X$$ of rolling a die $$n=1000$$ times. Since, the number of trials $$n>\Omega$$, is bigger than the sample space, we have to use a sample by replacement `sample(1L:6L, n, replace = T)`.


```
set.seed(7953)
# Sample 1000 from the set 1 to 6.
n <- 1000L
X <- sample(1L:6L, n, replace = T)
# Create a data.frame with the frequencies.
df <- as.data.frame(table(X))

# Add a column of the cumulative sum of the frequencies
df$cum_sum <- cumsum(df$Freq)

# Add a column with the corresponding emp. probability of each realization
df$prob <- df$Freq/n

```

Naturally, we know that if the die is fair, and all sides have equal chance of showing off, then the probability of each event it $$P[X=1]={1/6}=0.16$$. Now look at the fourth column we have added the empirical probability of $$X$$. It seems that $$n=1000$$ is approaching the theoretical probability of $$1/6$$.

<table border=1>
<caption align="top"> Table: 9 </caption>
<tr> <th>  </th> <th> X </th> <th> Freq </th> <th> cum_sum </th> <th> prob </th>  </tr>
  <tr> <td align="right"> 1 </td> <td> 1 </td> <td align="right"> 164 </td> <td align="right"> 164 </td> <td align="right"> 0.16 </td> </tr>
  <tr> <td align="right"> 2 </td> <td> 2 </td> <td align="right"> 159 </td> <td align="right"> 323 </td> <td align="right"> 0.16 </td> </tr>
  <tr> <td align="right"> 3 </td> <td> 3 </td> <td align="right"> 166 </td> <td align="right"> 489 </td> <td align="right"> 0.17 </td> </tr>
  <tr> <td align="right"> 4 </td> <td> 4 </td> <td align="right"> 165 </td> <td align="right"> 654 </td> <td align="right"> 0.16 </td> </tr>
  <tr> <td align="right"> 5 </td> <td> 5 </td> <td align="right"> 175 </td> <td align="right"> 829 </td> <td align="right"> 0.17 </td> </tr>
  <tr> <td align="right"> 6 </td> <td> 6 </td> <td align="right"> 171 </td> <td align="right"> 1000 </td> <td align="right"> 0.17 </td> </tr>
   </table>

*Probability* is defined as relative frequency of occurrence or *realization* of outcomes of an event $$X$$ given $$n$$ trials of an experiment. If $$x_i$$ is a realization of $$X$$, an $$1(.)$$ indicator function takes a value of $$1$$ or $$0$$ otherwise, such a *function of probability* is defined as follows:

<br>
$$P(X=x_i)=\frac{1}{n}\sum_{i=1}^n 1_{\{ X = x_i\}}$$
<br>


From the table, we can put some numbers to the formula to make it less abstract, using our induction skills. First, we take one event $$X=5$$, then we write the formula:

<br>
$$P(X=5)= \frac{1}{1000}\sum_{i=1}^n 1_{\{ X = 5\}}=\frac{1}{1000}*(175)=0.175$$
<br>

That wasn't that hard, isn't?


Now we can link the frequency and probability to the *sample mean* and the *expectation*. We conclude that if the die is fair then we expect that on average each event show up $$16$$ times for every $$100$$ trials. That means the expectation of the random variable $$X$$ is defined as:

<br>
$$E[X]= \mu_{X} =\frac{1}{6}$$
<br>

Bear in mind that the $$E[X]$$ describes the behavior of the random variables when we observe the population. Or in other words, when our sample size is sufficiently large to approximate the $$E[X]$$. In the previous example, we only have $$n=1000$$ trials, and for this sample we can compute the *sample mean* or average in the following way:

<br>
$$\bar{X}=\sum^i \frac{x_i *1_{\{ X = x_i\}}}{n}$$
<br>

To understand this equation better, we should use our deductive reasoning to expand the current formula. To make explicit the connection between the frequency, average and probability, let's follow the follow steps:


a. Replace $$n=1000$$ in the formula.

b. Replace $$x_i$$ for each realization of $$X = \{1,2, \dots, 6\}$$.

c. Replace $$1_{\{ X = x_1\}}$$ for the **Freq** of Table 3.

This yields the following expansion:

<br>
$$\bar{X}= \frac{1 * 164}{1000}+ \dots + \frac{6 * 171}{1000}$$
<br>

Now, to make the computation easier we can add the Table 3, one additional column equal to **X** times **Freq** divided by $$n$$. Summing this column completes the procedure of the computation of the *sample average* or mean, $$\hat{X}=3.541$$, given by `sum(df$x_freq)`. 

```
df$x_freq <- (as.integer(df$X) * df$Freq)/n
sum(df$x_freq)
```

<table border=1>
<caption align="top"> Table: 10 </caption>
<tr> <th>  </th> <th> X </th> <th> Freq </th> <th> cum_sum </th> <th> prob </th> <th> x_freq </th>  </tr>
  <tr> <td align="right"> 1 </td> <td> 1 </td> <td align="right"> 164 </td> <td align="right"> 164 </td> <td align="right"> 0.16 </td> <td align="right"> 0.16 </td> </tr>
  <tr> <td align="right"> 2 </td> <td> 2 </td> <td align="right"> 159 </td> <td align="right"> 323 </td> <td align="right"> 0.16 </td> <td align="right"> 0.32 </td> </tr>
  <tr> <td align="right"> 3 </td> <td> 3 </td> <td align="right"> 166 </td> <td align="right"> 489 </td> <td align="right"> 0.17 </td> <td align="right"> 0.50 </td> </tr>
  <tr> <td align="right"> 4 </td> <td> 4 </td> <td align="right"> 165 </td> <td align="right"> 654 </td> <td align="right"> 0.16 </td> <td align="right"> 0.66 </td> </tr>
  <tr> <td align="right"> 5 </td> <td> 5 </td> <td align="right"> 175 </td> <td align="right"> 829 </td> <td align="right"> 0.17 </td> <td align="right"> 0.88 </td> </tr>
  <tr> <td align="right"> 6 </td> <td> 6 </td> <td align="right"> 171 </td> <td align="right"> 1000 </td> <td align="right"> 0.17 </td> <td align="right"> 1.03 </td> </tr>
   </table>

<br>

The previous procedure is exactly the same if you compute `mean(X)`, prove it yourself. This formula, $$\hat{X}=\sum_1^S \frac{x_i *1_{\{ X = x_i\}}}{n}$$,  of the mean is very tedious, and normally it does not appear in the text books. Instead, what typically shows up is the simpler version of the average, similarly to [Wikipedia's Formula](https://en.wikipedia.org/wiki/Sample_mean_and_covariance).

<br>

$$\hat{X}=\frac{1}{n}\sum_{i=1}^n x_i$$
<br>

You, may be wondering then, if we have a simpler manner of computing the mean, why bother? Well, the purpose of this exercise was to teach you the use of frequency tables to summarize variables. Then a second purpose is to make explicit the link between the mean, the frequency and the probability of a random variable.


## Measurements of Central Tendency.

In the last section, we learn that our data sets are collected to summarize and assert something about a certain population of interest. Further, we use **frequency tables** to group the realizations of random variable, and to calculate the **probability** of certain event. Most importantly, we learn the connection between frequency, probability and **average**. The average is only one way to describe the event that most often shows-up, the most popular. In this section, I will show you other measurements to describe the behavior of our variables. Namely, the `mean`, `median`, `mode` and `variance` and `standard deviation`.

To give these measurements a flavor, let use a real data set that is rich in variables describing the behavior of credit card users. You may want to download this data set using the following [link](https://www.kaggle.com/code/amanpatyal/exploratory-analysis-bankchurners-csv/data). First, let's compute the `mean` of some important variables such as `age`, `credit limit`, number of `dependents` in the past year.  
```

df_chunkers <- read.csv("BankChurners.csv")
df_chunkers <- as.data.frame(unclass(df_chunkers), 
                             stringsAsFactors = TRUE) # Convert all columns to factor

mean(df_chunkers$Customer_Age)
mean(df_chunkers$Credit_Limit)
mean(df_chunkers$Dependent_count)


```
<table border=1>
<caption align="top"> Table: 11 </caption>
<tr> <th>  </th> <th> mean_cust_age </th> <th> mean_cred_lim </th> <th> mean_inac_months </th>  </tr>
  <tr> <td align="right"> 1 </td> <td align="right"> 46.33 </td> <td align="right"> 8631.95 </td> <td align="right"> 2.35 </td> </tr>
   </table>

   

One issue of the mean or average is that unfortunately changes rapidly with higher values that may not come from the same data generation process as the described variable. In Data science and statistics, we call these values outlines, to detect them we have to do a separate lecture. But for demonstration purposes, follow this example with artificial data, so you can understand the use of the next measurement of central tendency: median. The variables `X` and `Y` both contain `10` elements, they are identical. The first `9` numbers of are actually the same $$[1-9]$$, however, the variable `Y` last number is `576`, whereas for `X` is `10`. Table 12, summarizes the `mean` of `X` and `Y`, followed by the `median` of `Y`. The value of the mean $$\hat{Y}=62.10$$ is 10 times more than the mean of $$\hat{X}=5.5$$. The difference is huge, and the increase of $$\hat{Y}$$ is only due to one large value. The median thus reflects better the central tendency of a random variable in the presence of outliers.



```{r}
X <- 1L:10L
mean(X)

Y <- c(1L:9L, 576)
mean(Y)
median(Y)

```


<table border=1>
<caption align="top"> Table: 12 </caption>
<tr> <th>  </th> <th> X_mean </th> <th> mean_Y </th> <th> median_Y </th>  </tr>
  <tr> <td align="right"> 1 </td> <td align="right"> 5.50 </td> <td align="right"> 62.10 </td> <td align="right"> 5.50 </td> </tr>
   </table>

- **The median**, similar to the mean, aims to capture the central value of a set of realizations of a random variable. But different to the mean, the calculation starts by sorting the values from the smallest to the largest. Then if $$n$$ is an odd number, the median is the value in the $$(n+1)/2$$ position in the set. Conversely, if $$n$$ is an even number, the median is defined as the average of the positions $$n/2$$ and $$(n/2)+1$$. In **R** we compute the median, by passing a vector through the function `median()`. In the next table, we compare the three selected variables from the data set of credit card users using the `mean` and `median`.


```

median(df_chunkers$Customer_Age)
median(df_chunkers$Credit_Limit)
median(df_chunkers$Dependent_count)

```
<div id="tab_13">
<table border=1>
<caption align="top"> Table: 13 </caption>
<tr> <th>  </th> <th> mean_cust_age </th> <th> median_cust_age </th> <th> mean_cred_lim </th> <th> median_cred_lim </th> <th> mean_dep_count </th> <th> median_dep_count </th>  </tr>
  <tr> <td align="right"> 1 </td> <td align="right"> 46.33 </td> <td align="right">  46 </td> <td align="right"> 8631.95 </td> <td align="right"> 4549.00 </td> <td align="right"> 2.35 </td> <td align="right">   2 </td> </tr>
   </table>
</div>

What we can observe, is that the variable `Credit_Limit`, must be loaded of few consumers with high credit card limit. We know that because the *mean* is significantly bigger than the *median*, or what is called **right-skewness**.  Is called right skewness because there are few values significantly bigger than the rest of the realizations of the random variable. Conversely, **left-skewness*** happens when the *mean* is smaller than the *median*. In the section of visualizing continuous variables, you can see a graphic representation of these two kinds of data arrangements.

- **The mode** is the element with the highest frequency in a set of realizations of a random variable, or in other words the most popular value. In **R**, it is a good practice to calculate the `mode`, alongside the minimum and maximum value of a random variable. Unfortunately, there is no straightforward manner to calculate the `mode`, so what we typically do, is to compute a frequency by computing a `table(X)`, and retrieving the value with the highest frequency. In [Stackoverflow](https://stackoverflow.com/questions/2547402/how-to-find-the-statistical-mode), there is a nice `function` that we can apply to simplify the computation of the mode, as follows:



```

Mode <- function(x) {
  ux <- unique(x)
  ux[which.max(tabulate(match(x, ux)))]
}

Mode(df_chunkers$Customer_Age)
min(df_chunkers$Customer_Age)
max(df_chunkers$Customer_Age)

Mode(df_chunkers$Credit_Limit)
min(df_chunkers$Credit_Limit)
max(df_chunkers$Credit_Limit)

Mode(df_chunkers$Dependent_count)
min(df_chunkers$Dependent_count)
max(df_chunkers$Dependent_count)

```


<div id="tab_14">
<table border=1>
<caption align="top"> Table: 14 </caption>
<tr> <th>  </th> <th> cust_age </th> <th> cred_lim </th> <th> dep_count </th>  </tr>
  <tr> <td align="right"> Mean </td> <td align="right"> 46.33 </td> <td align="right"> 8631.95 </td> <td align="right"> 2.35 </td> </tr>
  <tr> <td align="right"> Median </td> <td align="right"> 46.00 </td> <td align="right"> 4549.00 </td> <td align="right"> 2.00 </td> </tr>
  <tr> <td align="right"> Mode </td> <td align="right"> 44.00 </td> <td align="right"> 34516.00 </td> <td align="right"> 3.00 </td> </tr>
  <tr> <td align="right"> Min </td> <td align="right"> 26.00 </td> <td align="right"> 1438.30 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> Max </td> <td align="right"> 73.00 </td> <td align="right"> 34516.00 </td> <td align="right"> 5.00 </td> </tr>
</table>
 </div>

## Measurements of Dispersion.

In the last sections, I show you measurements that summarize the central tendency of the variables. In this section, I am presenting the basic measurements that describe the dispersion of the variables. First, it is useful to know the spread of a variable in terms of the minimum and maximum variable in the set, using the function `range`. This however is not very informative because we do not have an idea of the values within these two extreme points. To have a better understanding of the spread of the values, we compute the `variance` the and `standard deviation`. These two measurements describe the spread of a variable, taking the mean as the point of comparison. The two measurements are related, because the standard deviation is simply the square root of the variance $$\sqrt{s^2}$$. 


- The **variance** starts by comparing all $$x_i$$ realizations to the mean of the random variable. These deviations are simply the difference of the realization to the mean $$\sum^n_{i=1}\frac{(x_i - \hat{x})}{(n-1)}$$. Naturally, the previous expression yields positive and negative that attenuate the real dispersion of the variable. For instance, imagine that we roll two dice, $$X=\{1, 2, \dots 12\}$$ 4 times, assume that the average is $$E[X]=6$$, and the field of realizations is $$[4,8,2,10]$$. Computing the average of deviations from the mean yields $$[4-6,\ 8-6,\ 2-6,\ 10-6]= (-2)+(2)+(-4)+(4)=0$$. This previous measurement is not informative because positive and negative deviations from the mean cancel each other out. Because of that reason, the variance takes the squared deviations from the mean as follows:

<br>
 $$S^2=\sum^n_{i=1}\frac{(x_i - \hat{x})^2}{(n-1)}$$
<br>

- The **standard deviation** is based on the variance, and it is defined as the squared root of the average squared deviations from the mean. In plain words the standard deviations tells us the average deviations from the mean. This measurement of dispersion helps us to map realizations of a random variable with corresponding probabilities (Section Normal Distribution).

<br>
 $$S=\sqrt{S^2}$$
<br>


From our previous analysis of measurements of central tendency [(Table 14)](/idsc_mgs/2022/02/22/w2_2_Lecture_03.html#tab_14), we found that the credit `card limit` is a right-skewed variable. We may suspect already that this variable has a high dispersion in comparison to the `age` and `number of dependents` because there is large difference between the minim value and the maximum value, that is the `range`. Lets verify this suspicion using our R-skills.


```

mean(df_chunkers$Customer_Age)
median(df_chunkers$Customer_Age)
Mode(df_chunkers$Customer_Age)
range(df_chunkers$Customer_Age)
var(df_chunkers$Customer_Age)
sd(df_chunkers$Customer_Age)


mean(df_chunkers$Credit_Limit)
median(df_chunkers$Credit_Limit)
Mode(df_chunkers$Credit_Limit)
range(df_chunkers$Credit_Limit)
var(df_chunkers$Credit_Limit)
sd(df_chunkers$Credit_Limit)

mean(df_chunkers$Dependent_count)
median(df_chunkers$Dependent_count)
Mode(df_chunkers$Dependent_count)
range(df_chunkers$Dependent_count)
var(df_chunkers$Dependent_count)
sd(df_chunkers$Dependent_count)


```

<div id="tab_15">
<table border=1>
<caption align="top"> Table: 15 </caption>
<tr> <th>  </th> <th> cust_age </th> <th> cred_lim </th> <th> dep_count </th>  </tr>
  <tr> <td align="right"> Mean </td> <td align="right"> 46.33 </td> <td align="right"> 8631.95 </td> <td align="right"> 2.35 </td> </tr>
  <tr> <td align="right"> Median </td> <td align="right"> 46.00 </td> <td align="right"> 4549.00 </td> <td align="right"> 2.00 </td> </tr>
  <tr> <td align="right"> Mode </td> <td align="right"> 44.00 </td> <td align="right"> 34516.00 </td> <td align="right"> 3.00 </td> </tr>
  <tr> <td align="right"> Range-Min </td> <td align="right"> 26.00 </td> <td align="right"> 1438.30 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> Range-Max </td> <td align="right"> 73.00 </td> <td align="right"> 34516.00 </td> <td align="right"> 5.00 </td> </tr>
  <tr> <td align="right"> Variance </td> <td align="right"> 64.27 </td> <td align="right"> 82605861.00 </td> <td align="right"> 1.69 </td> </tr>
  <tr> <td align="right"> S.D </td> <td align="right"> 8.02 </td> <td align="right"> 9088.78 </td> <td align="right"> 1.30 </td> </tr>
   </table>
 </div>



What can we conclude from [(Table 15)](/idsc_mgs/2022/02/22/w2_2_Lecture_03.html#tab_15)? As we suspected, the variables `credit card limit` depicts a very large dispersion from the mean; around $$9000.00$$ US dollars. The `number of dependents` does not depart much from the mean, on average all the observations departs around $$1.3$$ units from the mean. Also the variable `age` does not have a high dispersion, as we find customers ranging from 26 to 76 but the observations only deviate $$8$$ years on average from the mean of $$46$$ years.



## Measurements of Association.

Aside from describing the data using the measurements of central tendency and dispersion, descriptive statistics, also involve measuring relations between pairs of variables. In [Lecture 4](https://wario84.github.io/idsc_mgs/2022/02/22/w4_2_Lecture_04.html), is all about the kind of relationships between variables. As we will learn, an association is not a synonym of causation, and we should be careful about the claim you make about the relationship between two variables using the following measurements. These two measurements of association are not causal, which means they only inform about the way the pair of variables change together, namely *positive*, *negative* or *no-relation*.


- **Covariance** measures the extent from which two random variables change together. We compute the sample co-variance by adding the product of the deviations between two variables $$X$$ and $$Y$$.

<br>
$$S_{XY}= \sum_i^{n} \frac{(x_i - \bar{x})(y_i - \bar{y})}{(n-1)}$$
<br>

- **Correlation** is the standardized version of the co-variance. The output of the co-variance is difficult to interpret, because the units of $$X$$ are multiplied times the units of $$Y$$. To avoid this problem, the correlations standardizes the change between the two variables by dividing the co-variance by the product of the sample standard deviation of the two variables. The result is an index that varies between $$[-1,1]$$, indicating the strengh of the relationship as it approxes the extreme values, and the type of relationship if the computation of the index yields positive or negative values.


<br>
$$R_{XY}=  \frac{S_{XY}}{S_x \, S_y}$$
<br>


In **R**, the computation of the co-variance and correlation is straight fordward. The most common ways to present the co-variances and correlations between variables in a data set is by using a matrix.



```

cov(df_chunkers$Customer_Age, df_chunkers$Credit_Limit)
cor(df_chunkers$Customer_Age, df_chunkers$Credit_Limit)

cov(df_chunkers$Customer_Age, df_chunkers$Dependent_count)
cor(df_chunkers$Customer_Age, df_chunkers$Dependent_count)

cor(df_chunkers$Dependent_count, df_chunkers$Credit_Limit)
cov(df_chunkers$Dependent_count, df_chunkers$Credit_Limit)


cols <- c("Customer_Age", "Dependent_count", "Total_Revolving_Bal", 
"Avg_Utilization_Ratio") # subset of variables.
  
cov(df_chunkers[,cols]) # covariance matrix
cor(df_chunkers[,cols]) # correlation matrix


```

<div id="tab_16">
<table border=1>
<caption align="top"> Table 16: Co-variance Matrix </caption>
<tr> <th>  </th> <th> Customer_Age </th> <th> Dependent_count </th> <th> Total_Revolving_Bal </th> <th> Avg_Utilization_Ratio </th>  </tr>
  <tr> <td align="right"> Customer_Age </td> <td align="right"> 64.27 </td> <td align="right">  </td> <td align="right">  </td> <td align="right">  </td> </tr>
  <tr> <td align="right"> Dependent_count </td> <td align="right"> -1.27 </td> <td align="right"> 1.69 </td> <td align="right">  </td> <td align="right">  </td> </tr>
  <tr> <td align="right"> Total_Revolving_Bal </td> <td align="right"> 96.57 </td> <td align="right"> -2.85 </td> <td align="right"> 664204.36 </td> <td align="right">  </td> </tr>
  <tr> <td align="right"> Avg_Utilization_Ratio </td> <td align="right"> 0.02 </td> <td align="right"> -0.01 </td> <td align="right"> 140.21 </td> <td align="right"> 0.08 </td> </tr>
   </table>
</div> 

As expected, the co-variance matrix [(Table 16)](/idsc_mgs/2022/02/22/w2_2_Lecture_03.html#tab_16) is only able to describe if the relationship between the variables is positive or negative. However, the values of the matrix does not tell anything about the strength of the relationship between pairs of variables.

<div id="tab_17">
<table border=1>
<caption align="top"> Table 17: Correlation Matrix </caption>
<tr> <th>  </th> <th> Customer_Age </th> <th> Dependent_count </th> <th> Total_Revolving_Bal </th> <th> Avg_Utilization_Ratio </th>  </tr>
  <tr> <td align="right"> Customer_Age </td> <td align="right"> 1.00 </td> <td align="right">  </td> <td align="right">  </td> <td align="right">  </td> </tr>
  <tr> <td align="right"> Dependent_count </td> <td align="right"> -0.12 </td> <td align="right"> 1.00 </td> <td align="right">  </td> <td align="right">  </td> </tr>
  <tr> <td align="right"> Total_Revolving_Bal </td> <td align="right"> 0.01 </td> <td align="right"> -0.00 </td> <td align="right"> 1.00 </td> <td align="right">  </td> </tr>
  <tr> <td align="right"> Avg_Utilization_Ratio </td> <td align="right"> 0.01 </td> <td align="right"> -0.04 </td> <td align="right"> 0.62 </td> <td align="right"> 1.00 </td> </tr>
   </table>
</div> 

The correlation matrix [(Table 17)](/idsc_mgs/2022/02/22/w2_2_Lecture_03.html#tab_17) show more clearly the relationship between pairs of variables. Similarly to x [(Table 16)](/idsc_mgs/2022/02/22/w2_2_Lecture_03.html#tab_16), the main diagonal (composed of ones) is not informative, as it only measures the correlation with the variable itself. Assessing the first column of the matrix, we can compare the correlation between `Customer_Age` and all the other variables in the sub-sample. We can tell that there is a negative relationship between `Dependent_count` and `Customer_Age`. This signifies that there when the age of the customers increases (for instance above the mean of 46 years) the tendency to have children reduces. Although, this association is weak, as the correlation coefficient is only $$-0.12$$. `Customer_Age` shows no correlation to the other variables `Total_Revolving_Bal` and `Avg_Utilization_Ratio`. Focusing on column three or the row number four of [(Table 17)](/idsc_mgs/2022/02/22/w2_2_Lecture_03.html#tab_17), we can see that there is a positive relationship between the `Avg_Utilization_Ratio` and `Total_Revolving_Bal`. This correlation follows our intuition, as customers use more often their credit card also most likely have a higher balance.


# Visualizing Data.

Another important way to understand data is by using graphical techniques or plots. I will use the `ggplot2` package, that is an elegant environment to graph data using **R**. It is out of the scope of the course to describe in details the use of `ggplot2`. For that reason you may read the following resources before continuing:

- [First Steps to `ggplot2`](https://ggplot2-book.org/getting-started.html).

- [`ggplot2` Cheatsheet](https://github.com/rstudio/cheatsheets/blob/main/data-visualization-2.1.pdf)

## Normal Distribution.

The measurements of *centrality* and *dispersion* are better observed if we sort them, and we arrange the realizations of the random variable using plots. The first plot is called **histogram** and a smother version of this plot is called **density** plot. Histograms are excellent to visualize the arrangement of discrete variables, for instance `age` and `number of dependents` in the credit card data set. However, continuous variables like `credit card` limit are better observed with the density plot.

If we pay attention to column three, from [(Table 15)](/idsc_mgs/2022/02/22/w2_2_Lecture_03.html#tab_15), we can see how come the arrangement or **distribution** of a random variable `Credit_Limit` is **right-skewed**. The reason, is due to the fact that most observations lie to the left of the mean, but there are few individuals with a very high credit limit. This is also observed in the third row of the picture below. Here, we can observe the distribution of `Credit_Limit` leaning towards the left, because, there are few high values, the `mean` is bigger than the `median` and the `QQ-plot` deviates from at 45 degree line, but it is heavily loaded on the tails of the distribution.

The variables `age` and `number of dependents` show a symmetrical arrangement. When the variables display this pattern, we called them approximately **normally distributed**. Many empirical variables render this pattern, when the `mean` and `median` do not deviate largely, such as the variables `age` and `number of dependents`. Furthermore, we can observe that the `QQ-plot` renders a line that is closer to a 45 degree line from origin to the top-right of the plot in rows one and two. Similarly, we can observe the symmetry of the distributions because the mean and the median are close to each other in the center of the distribution, and values to the right and left have a lower frequency.

<br>

```
library(ggplot2)
library(gridExtra)

p <- ggplot(df_chunkers, aes(x =  Customer_Age)) # Customer age.
c <- ggplot(df_chunkers, aes(x = Dependent_count)) # Number of dependents.
m <- ggplot(df_chunkers, aes(x =  Credit_Limit )) # Credit card limit.


grid.arrange(
  p + geom_histogram() +
    ggtitle("Histogram"),
  
  p + geom_density() +
    ggtitle("Density"),
  
  ggplot(df_chunkers) + geom_qq(aes(sample = Customer_Age)) +
    ggtitle("QQ-Plot"),
  
  c + geom_histogram() +
    ggtitle("Histogram"),
  
  c + geom_density() +
    ggtitle("Density"),
  
  ggplot(df_chunkers) + geom_qq(aes(sample = Dependent_count)) +
    ggtitle("QQ-Plot"),
  
  m + geom_histogram() +
    ggtitle("Histogram"),
  
  m + geom_density() +
    ggtitle("Density"),
  
  ggplot(df_chunkers) + geom_qq(aes(sample = Credit_Limit)) +
    ggtitle("QQ-Plot"),
  
  ncol = 3
)

```

![](https://github.com/Wario84/idsc_mgs/raw/master/assets/imgs/histo_densi_qq.svg?raw=true)


## Visualizing Discrete and Categorical Variables

Categorical variables are different in nature to continuous or discrete variables. Categorical variables, typically map a list of mutually exclusive categories. The list of categories is typically smaller range in comparison to spread of continuous or discrete variables. The purpose of categorical variables is mapping changes in kind, state or quality, in comparison of numerical and discrete variables that map subtle changes of one kind. In the data set of credit card customers, we have examples of numerical variables that map changes in one dimension in terms of `age`, `number of dependents` or `utilization ratio`. But categorical variables map changes of different kinds, for instance, the `mpg` data set of the `ggplot2` package is rich in categorical variables. The selected categorical variables, `year`, map changes in production from two years; the variable `cyl` maps the number of motor cylinders of a car; the variable `manufacturer` maps different brands of cars and the variable `trans` specifies the type of gear of the cars. This kind of variables are better visualized using **Bar Plots** and **Pie Charts**, as follows:


<!-- https://dk81.github.io/dkmathstats_site/rvisual-piecharts.html -->

```
library(ggplot2)
library(gridExtra)

data(mpg)
mpg_ <- mpg
mpg_ <-  as.data.frame(unclass(mpg_),
stringsAsFactors = TRUE)    # Convert all columns to factor



p <- ggplot(mpg_, aes(y =  year )) # year of car production, discrete.
c <- ggplot(mpg_, aes(y =  cyl )) # number of cylinders, categorical.
m <- ggplot(mpg_, aes(y =  manufacturer )) # manufacturer, categorical.
t <- ggplot(mpg_, aes(y =  trans )) # transmission, categorical.

# Create tables for frequency for each variable
year <- as.data.frame(table(mpg_$year)/nrow(mpg_))
cyl <- as.data.frame(table(mpg_$cyl)/nrow(mpg_))
man <- as.data.frame(table(mpg_$manufacturer)/nrow(mpg_))
trans <- as.data.frame(table(mpg_$trans)/nrow(mpg_))



grid.arrange(
  # Plots year 
  p + geom_bar() +
    ggtitle("Barplot"),
  
  ggplot(year, aes(x = "", y = Freq, fill = Var1)) +
    geom_bar(width = 1, stat = "identity") +
    coord_polar(theta = "y", start = 0) +
    ggtitle("Pie Chart"),
  
  # Plots Cylinders
  c + geom_bar(),
  
  ggplot(cyl, aes(x = "", y = Freq, fill = Var1)) +
    geom_bar(width = 1, stat = "identity") +
    coord_polar(theta = "y", start = 0),
  
  # Plots Manufacturer
  m + geom_bar(),

  ggplot(man, aes(x = "", y = Freq, fill = Var1)) +
    geom_bar(width = 1, stat = "identity") +
    coord_polar(theta = "y", start = 0),
  
  # Plots Transmission
  t + geom_bar(),

  ggplot(trans, aes(x = "", y = Freq, fill = Var1)) +
    geom_bar(width = 1, stat = "identity") +
    coord_polar(theta = "y", start = 0),
  
  
  ncol = 2
)

```


![](https://github.com/Wario84/idsc_mgs/raw/master/assets/imgs/pie_bar_charts.svg?raw=true)





