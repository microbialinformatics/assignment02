# Assignment 2
Kat Wiles  
September 26, 2014  

Data Source:

```r
metadata <- read.table(file="wild.metadata.txt", header=T)
rownames(metadata) <- metadata$Group
metadata <- metadata[,-1]
```

1.  Calculate the following on the data we read in from the `wild.metadata.txt` file that we discussed in class on 9/16/2014.

  * How many samples were described in the `wild.metadata.txt`?
  

```r
num.samples<-nrow(metadata)
```
  There were 111 samples
  
  
   * How many columns are in the table? What are their names
  

```r
num.columns<-ncol(metadata)
col.names<-colnames(metadata)
```
  There are 9 columns with the following names: Date, ET, Station, SP, Sex, Age, Repro, Weight, Ear
  
  
  * How many mice weighed 15 or more grams?

```r
mice.weight15<-nrow(metadata[metadata$Weight>=15,])
```
    There were 77 mice that weighed 15 or more grams.
  
  * What is the median weight for the mice sampled?
  * How many PMG mice were there?
  * How many female PL mice were there?
  * Alphabetize `wild.metadata.txt` by the ear tag number (only show the first 5 rows of the table)
  * Sort the table by the weight of each animal
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


3.	Calculate the mode for the weight of the mice in `wild.metadata.txt`


4.	Usign R commands, write the table to a new text file, but exclude the `Ear` and `Repro` columns.

