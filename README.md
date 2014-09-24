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

```r
n.samples <- nrow(metadata[,])
```
<!---
Does this count include headers?
-->
There were 111 samples described in the `wild.metadata.txt`.
  
  * How many columns are in the table? What are their names? 

```r
n.columns <- ncol(metadata[,])
names <- colnames(metadata)
```
There are 9 columns in the table.
Their names are Date, ET, Station, SP, Sex, Age, Repro, Weight, Ear.

  * How many mice weighed 15 or more grams?

```r
more.weight <- metadata$Weight >= 15
n.more.weight <- nrow(metadata[more.weight,])
```
There were 77 mice that weighed 15 or more grams.

  * What is the median weight for the mice sampled?

```r
med <- median(metadata$Weight, na.rm = FALSE)
```
The median weight for the mice sampled was 16.

  * How many PMG mice were there?

```r
PMG <- metadata$SP == "PMG"
n.PMG <- nrow(metadata[PMG,])
```
There were 53 PMG mice.

  * How many female PL mice were there?

```r
PL.F <- metadata$SP == "PL" & metadata$Sex == "F"
n.PL.F <- nrow(metadata[PL.F,])
```
There were 24 mice.

  * Alphabetize `wild.metadata.txt` by the ear tag number (only show the first 5 rows of the table)

```r
sorted.metadata <- metadata[order(metadata$ET), ]
```
The first 5 rows of the sorted table are:

```
##        Date ET Station SP Sex Age Repro Weight Ear
## 5_26m1 5_26  1     A12 PL   F   A    NE   19.5  14
## 6_14m1 6_14  1    AA13 PL   F   A    NE   22.0  14
## 7_13m1 7_13  1    AA13 PL   F   A    NE   23.5  14
## 7_14m1 7_14  1    CC13 PL   F   A    NE   21.0  15
## 5_31m2 5_31  2     CC4 PL   M  SA   ABD   15.0  14
```

  * Sort the table by the weight of each animal

```r
sortw.metadata <- metadata[order(metadata$Weight), ]
```
The first 5 rows of the sorted table are:

```
##         Date ET Station  SP Sex Age Repro Weight Ear
## 6_16m37 6_16 37     A12  PL   M   J     A    7.0  12
## 7_14m74 7_14 74     N17 PMG   F   J    NT    7.0  14
## 5_25m3  5_25  3    BB18  PL   M   J   ABD    7.5  13
## 6_29m48 6_29 48      P7  PL   F   J    NT    9.0  11
## 7_14m79 7_14 79     J20 PMG   F   J    NT    9.0  12
```

  * The `Station` column indicates where the mice were sampled. Where were the most mice captured?
  * How many mice were captured there?

```r
temp <- table(as.vector(metadata$Station))
station <- names(temp)[temp == max(temp)]
many.mice <- metadata$Station == station
n.many.mice <- nrow(metadata[many.mice,])
```
The most mice were captured at the N20 station.
There were 4 mice captured there.

2.	Describe what each of the following commands does in a text block above the code, be specific. Put the code into the appropriate knitr code chunk. If something throws an error or looks weird, fix it.

This command will generate a vector of numerical values that is every third number from 1 to 100.

```r
seq(1,100,3)
```

```
##  [1]   1   4   7  10  13  16  19  22  25  28  31  34  37  40  43  46  49
## [18]  52  55  58  61  64  67  70  73  76  79  82  85  88  91  94  97 100
```

This command will generate a vector of the characters "a" "b" repeated 10 times, for a total vector length of 20 characters.

```r
rep(c("a","b"),10)
```

```
##  [1] "a" "b" "a" "b" "a" "b" "a" "b" "a" "b" "a" "b" "a" "b" "a" "b" "a"
## [18] "b" "a" "b"
```

This command will generate a vector named 'r'. The 'runif' part of the command creates a vector named 'r' containing ten random values between 0 and 1. The 'order' part of the command yields a vector with the values of 'r' ranked from lowest to highest, denoting these by their position in vector 'r'.

```r
r <- runif(10); order(r)
```

```
##  [1]  8  5  6  7  3 10  1  4  2  9
```

This command needs to have an second '%' added. With two '%%', this command divides the first number by the second number, and yields the remainder as a whole number. So 3 goes into 100 33 times, with 1 left over, so 100 %% 3 returns a 1. 

```r
100 %% 3
```

```
## [1] 1
```

This command searches the data table 'metadata' and looks to output rows where the Weight column value is 16 AND the SP column character is PMG. However, there only needs to be one '&' (for vectors) and the capitalization on 'weight' needed to be fixed as well.

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

3.	Calculate the mode for the weight of the mice in `wild.metadata.txt`


```r
temp1 <- table(as.vector(metadata$Weight))
mode.weight <- names(temp1)[temp1 == max(temp1)]
```
The mode for the weight of the mice in the 'wild.metadata.txt' is 16, 17.

4.	Usign R commands, write the table to a new text file, but exclude the `Ear` and `Repro` columns.


```r
newmetadata <- metadata[,-9]
finalmetadata <- newmetadata[,-7]
write.table(finalmetadata, "/Users/daniellegoodman/assignment02/finalmetadata.txt", sep="\t")
```
Here are the first 5 rows of the updated file.

```
##         Date ET Station  SP Sex Age Weight
## 5_25m3  5_25  3    BB18  PL   M   J    7.5
## 5_25m4  5_25  4     K19  PL   M   A   16.0
## 5_26m1  5_26  1     A12  PL   F   A   19.5
## 5_26m9  5_26  9      M9  PL   F   A   25.0
## 5_31m11 5_31 11      F2 PMG   F   J   16.0
```

