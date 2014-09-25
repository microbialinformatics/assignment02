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
  * How many columns are in the table? What are their names?
  * How many samples came from mice that weighed 15 or more grams?
  * What is the median weight of the samples?
  * How many PMG samples were there?
  * How many female PL samples were there?
  * Alphabetize `wild.metadata.txt` by the ear tag number (only show the first 5 rows of the table)
  * Sort the table by the weight of the mice that each sample came from
  * The `Station` column indicates where the mice were sampled. Where were the most mice captured?
  * How many mice were captured there?


2.	Describe what each of the following commands does in a text block above the code, be specific. Put the code into the appropriate knitr code chunk. If something throws an error or looks weird, fix it.

```
seq(1,100,3)
```

```
rep(c("a","b"),10)
```

```
r <- runif(10); order(r)
```

```
100 % 3
```

```
metadata[metadata$weight==16 && metadata$SP=="PMG",]
```


3.	Calculate the mode for the weights in `wild.metadata.txt`


4.	Usign R commands, write the table to a new text file, but exclude the `Ear` and `Repro` columns.

