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
```{r}
nrow(metadata)
n.row <- nrow(metadata)
```
  
  * How many columns are in the table? What are their names?
```{r}
ncol(metadata)
n.col <- ncol(metadata)
colnames(metadata)
col.names <- colnames(metadata)
```
  * How many mice weighed 15 or more grams?
```{r}
sum(metadata$Weight>15)
```
  * What is the median weight for the mice sampled?
```{r}
median(metadata$Weight)
```
  * How many PMG mice were there?
```{r}
summary(metadata$SP)
```
  * How many female PL mice were there?
```{r}
aggregate(SP~Sex, data=metadata, summary)
```
  * Alphabetize `wild.metadata.txt` by the ear tag number (only show the first 5 rows of the table)
```{r}
metadata.Ear <- metadata[order(metadata$Ear), ]
metadata.Ear[1:5,]
```
  * Sort the table by the weight of each animal
```{r}
metadata.weight<- metadata[order(metadata$Weight),]
```
  * The `Station` column indicates where the mice were sampled. Where were the most mice captured?
  * How many mice were captured there?
```{r}
metadata.station <- summary(metadata$Station)
sort.metadata.station<- sort(metadata.station, decreasing=T)
sort.metadata.station[1]
```

2.	Describe what each of the following commands does in a text block above the code, be specific. Put the code into the appropriate knitr code chunk. If something throws an error or looks weird, fix it.

This command will generate a vector of every third number between 1 and 100
```
seq(1,100,3)
```
This command will generate a vector with the letters "a" and "b" 10 times  
```
rep(c("a","b"),10)
```
This command will create a vector ("r"). The vector contain random values between 0 and 1. The "order" in the command line mean that all numbers are ranked from lowest to highest in the vector 
```
r <- runif(10); order(r)
```
This command is missing another "%" to use as a operation. This is a modulus operator, which will result a remainder of 3 into 100, that is 1. That is the first number by the second number
```
100 % 3
```
This command do a search in the table for data and return all data, that the weight is "16" and SP is "PMG". But it is necessary to change the "&&" to just one "&" and the first letter of "weight" should be capitalized
```
metadata[metadata$weight==16 && metadata$SP=="PMG",]
```


3.	Calculate the mode for the weight of the mice in `wild.metadata.txt`
```{r}
weight <- table(as.vector(metadata$Weight))
weight.mode <- names(weight)[weight == max(weight)]
```

4.	Usign R commands, write the table to a new text file, but exclude the `Ear` and `Repro` columns.
```{r}
metadata.new <- metadata[c(-7, -9)]
write.table(metadata.new, file="new_metadata.txt")
```
