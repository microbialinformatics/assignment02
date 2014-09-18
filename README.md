# Assignment 2
Patrick D. Schloss  
September 15, 2014  

Complete the exercises listed below and submit as a pull request to the [Assignment 2 repository](http://www.github.com/microbialinformatics/assignment02).  Format this document approapriately using R markdown and knitr. I would like to see your code blocks and output in the final documents you submit. Your pull request needs to include your *.Rmd and *.md files. Do not alter the `.gitignore` file. You may work with a partner, but you must submit your own assignment and give credit to anyone that worked with you on the assignment.


```r
metadata <- read.table(file="wild.metadata.txt", header=T)
rownames(metadata) <- metadata$Group
metadata <- metadata[,-1]
```

1.  Calculate the following on the data we read in from the `wild.metadata.txt` file that we discussed in class on 9/16/2014.

  * How many samples were described in the `wild.metadata.txt`?

```r
length(unique(row.names(metadata)))
```

```
## [1] 111
```
  
  * How many columns are in the table? What are their names

```r
ncol(metadata)
```

```
## [1] 9
```

```r
colnames(metadata)
```

```
## [1] "Date"    "ET"      "Station" "SP"      "Sex"     "Age"     "Repro"  
## [8] "Weight"  "Ear"
```
  
  * How many mice weighed 15 or more grams?

```r
length(metadata$Weight[metadata$Weight < 15])
```

```
## [1] 34
```

```r
#OR
sum(metadata$Weight<15)
```

```
## [1] 34
```
  
  * What is the median weight for the mice sampled?

```r
median(metadata$Weight)
```

```
## [1] 16
```
 
  * How many PMG mice were there?

```r
nrow(metadata[metadata$SP=="PMG",])
```

```
## [1] 53
```
  
  * How many female PL mice were there?

```r
nrow(metadata[metadata$SP=="PMG" & metadata$Sex == "F",])
```

```
## [1] 36
```
  
  * Alphabetize `wild.metadata.txt` by the ear tag number (only show the first 5 rows of the table)

```r
library(plyr)
metadata  <- arrange(metadata, ET)
head(metadata)
```

```
##   Date ET Station SP Sex Age Repro Weight Ear
## 1 5_26  1     A12 PL   F   A    NE   19.5  14
## 2 6_14  1    AA13 PL   F   A    NE   22.0  14
## 3 7_13  1    AA13 PL   F   A    NE   23.5  14
## 4 7_14  1    CC13 PL   F   A    NE   21.0  15
## 5 5_31  2     CC4 PL   M  SA   ABD   15.0  14
## 6 6_15  2      B2 PL   M   A   SCR   17.0  14
```
  
  * Sort the table by the weight of each animal

```r
metadata <- metadata[order(metadata$Weight), ]
```
  
  * The `Station` column indicates where the mice were sampled. Where were the most mice captured?

```r
which.max(table(metadata$Station)) #The second row is the index of the value in the table
```

```
## N20 
##  70
```
  
  * How many mice were captured there?

```r
max(table(metadata$Station))
```

```
## [1] 4
```


2.	Describe what each of the following commands does in a text block above the code, be specific. Put the code into the appropriate knitr code chunk. If something throws an error or looks weird, fix it.

```
The following command generates a sequence of numbers that is every 3rd number between 1 and 100.
```

```r
seq(1,100,3)
```

```
##  [1]   1   4   7  10  13  16  19  22  25  28  31  34  37  40  43  46  49
## [18]  52  55  58  61  64  67  70  73  76  79  82  85  88  91  94  97 100
```

```
The following command first generates a sequence of "a" and "b" and then repeats it 10 times.
```

```r
rep(c("a","b"),10)
```

```
##  [1] "a" "b" "a" "b" "a" "b" "a" "b" "a" "b" "a" "b" "a" "b" "a" "b" "a"
## [18] "b" "a" "b"
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

