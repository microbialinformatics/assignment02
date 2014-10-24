# Assignment 2
Patrick D. Schloss  
September 15, 2014  

Complete the exercises listed below and submit as a pull request to the [Assignment 2 repository](http://www.github.com/microbialinformatics/assignment02).  Format this document approapriately using R markdown and knitr. I would like to see your code blocks and output in the final documents you submit. As much as possible, you should output your solutions by embedding the solution within the text [see this example](https://github.com/microbialinformatics/assignment02/blob/master/example.Rmd). For those cases where there are multiple outputs, make it clear in how you format the text and interweave the solution, what the solution is.

Your pull request needs to include your *.Rmd and *.md files. Do not alter the `.gitignore` file. You may work with a partner, but you must submit your own assignment and give credit to anyone that worked with you on the assignment.


```r
metadata <- read.table(file="wild.metadata.txt", header=T)
rownames(metadata) <- metadata$Group
metadata <- metadata[,-1]
```

1.  Calculate the following on the data we read in from the `wild.metadata.txt` file that we discussed in class on 9/16/2014.

  * How many samples were described in the `wild.metadata.txt`?
  
There were 111 samples described in the file


  * How many columns are in the table? What are their names?

There were 9 columns described in the file that were named Date, ET, Station, SP, Sex, Age, Repro, Weight, Ear


  * How many samples came from mice that weighed 15 or more grams?

There were 77 samples from mice that weighed at least 15 g.


  * What is the median weight of the samples?
  
The median weight of the samples was 16.
  
  * How many PMG samples were there?
  
There were 53 samples from PMG mice.

  
  * How many female PL samples were there?
  
There were 24 samples from female PL mice.
  
  * Alphabetize `wild.metadata.txt` by the ear tag number (only show the first 5 rows of the table)


```r
o <- order(metadata$ET)
sorted <- metadata[o,]
head(sorted, n=5)
```

```
##        Date ET Station SP Sex Age Repro Weight Ear
## 5_26m1 5_26  1     A12 PL   F   A    NE   19.5  14
## 6_14m1 6_14  1    AA13 PL   F   A    NE   22.0  14
## 7_13m1 7_13  1    AA13 PL   F   A    NE   23.5  14
## 7_14m1 7_14  1    CC13 PL   F   A    NE   21.0  15
## 5_31m2 5_31  2     CC4 PL   M  SA   ABD   15.0  14
```

  * Sort the table by the weight of the mice that each sample came from


```r
o <- order(metadata$Weight)
sorted <- metadata[o,]
head(sorted, n=5)
```

```
##         Date ET Station  SP Sex Age Repro Weight Ear
## 6_16m37 6_16 37     A12  PL   M   J     A    7.0  12
## 7_14m74 7_14 74     N17 PMG   F   J    NT    7.0  14
## 5_25m3  5_25  3    BB18  PL   M   J   ABD    7.5  13
## 6_29m48 6_29 48      P7  PL   F   J    NT    9.0  11
## 7_14m79 7_14 79     J20 PMG   F   J    NT    9.0  12
```


  * The `Station` column indicates where the mice were sampled. Where were the most mice captured?
  

```r
count.sites <- table(metadata$Station)
most.freq <- names(count.sites)[which.max(count.sites)]
n.most.freq <- max(count.sites)
```

More mice were sampled from Station N20 than from any other site.

  
  * How many mice were captured there?

A total of 4 mice were captured there.


2.	Describe what each of the following commands does in a text block above the code, be specific. Put the code into the appropriate knitr code chunk. If something throws an error or looks weird, fix it.

This code generates a list of numbers from 1 to 100 by 3s:


```r
seq(1,100,3)
```

```
##  [1]   1   4   7  10  13  16  19  22  25  28  31  34  37  40  43  46  49
## [18]  52  55  58  61  64  67  70  73  76  79  82  85  88  91  94  97 100
```


This code repeats the characters "a" and "b" 10 times:


```r
rep(c("a","b"),10)
```

```
##  [1] "a" "b" "a" "b" "a" "b" "a" "b" "a" "b" "a" "b" "a" "b" "a" "b" "a"
## [18] "b" "a" "b"
```


This code outputs the order of the indices of 10 randomly drawn numbers from a uniform distribution between 0 and 1 when they are sorted


```r
r <- runif(10); order(r)
```

```
##  [1]  6  2  1  3  7 10  9  4  5  8
```


This code doesn't actually work. You probably want two `%` characters. If that is the case then it returns the integer remainder of dividing 100 by 3

```r
100 %% 3
```

```
## [1] 1
```


This code also doesn't work because you have two `&` characters and because the column in the metadata file is actually `Weight`. When you fix these errors, you get the rows from the metadata file that correspond to PMG mice that weighed 16 g.


```r
metadata[metadata$Weight==16 & metadata$SP=="PMG",]
```

```
##         Date ET Station  SP Sex Age Repro Weight Ear
## 5_31m11 5_31 11      F2 PMG   F   J    NT     16  18
## 6_15m16 6_15 16     L11 PMG   M   A   SCR     16  17
## 6_1m12   6_1 12     H18 PMG   M   A   SCR     16  14
## 6_30m43 6_30 43    CC13 PMG   F   J     N     16  15
## 6_5m16   6_5 16     H20 PMG   M   A   SCR     16  16
## 7_14m59 7_14 59     CC3 PMG   M  SA   SCR     16  17
## 7_2m25   7_2 25     P17 PMG   F   A    NE     16  15
## 7_3m43   7_3 43    CC13 PMG   F  SA    NT     16  16
```


3.	Calculate the mode for the weights in `wild.metadata.txt`


```r
weight.count <- table(metadata$Weight)
max.freq <- max(weight.count)
mode <- as.numeric(names(weight.count[weight.count==max.freq]))
```

The mode(s) was/were 16, 17.


4.	Usign R commands, write the table to a new text file, but exclude the `Ear` and `Repro` columns.


```r
mod.table <- metadata[,-c(7,9)]
write.table(mod.table, file="modified.txt")
```
