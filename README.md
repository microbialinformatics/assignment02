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

```r
med.weight<-median(metadata$Weight)
```
      The median mice weight was 16 grams.
      
  * How many PMG mice were there?
  

```r
pmg.mice<-nrow(metadata[metadata$SP=="PMG",])
```
      There were 53 PMG mice sampled.
      
      
        * How many female PL mice were there?

```r
pl.mice.f<-nrow(metadata[metadata$SP=="PL" & metadata$Sex=="F",])
```
      There were 24 female PL mice.
      
      
 * Alphabetize `wild.metadata.txt` by the ear tag number (only show the first 5 rows of the table)

```r
metadata$ET<-factor(metadata$ET)
et.sort<-metadata[order(metadata$ET),]
et.sort[1:5,]
```

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
metadata$Weight<-factor(metadata$Weight)
weight.sort<-metadata[order(metadata$Weight),]
weight.sort[1:5,]
```

```
##         Date ET Station  SP Sex Age Repro Weight Ear
## 6_16m37 6_16 37     A12  PL   M   J     A      7  12
## 7_14m74 7_14 74     N17 PMG   F   J    NT      7  14
## 5_25m3  5_25  3    BB18  PL   M   J   ABD    7.5  13
## 6_29m48 6_29 48      P7  PL   F   J    NT      9  11
## 7_14m79 7_14 79     J20 PMG   F   J    NT      9  12
```
  
  * The `Station` column indicates where the mice were sampled. Where were the most mice captured?

```r
best.station<-sort(table(metadata["Station"]), decreasing=TRUE)[1]
```
      The most mice were sampled at stationN20.
  
   
  * How many mice were captured there?
         

```r
N20mice<-metadata[metadata["Station"]=="N20",]
N20.unique<-N20mice[!duplicated(N20mice["ET"]),]
```
There were 4 captures of 3 unique individuals at  N20.


2.	Describe what each of the following commands does in a text block above the code, be specific. Put the code into the appropriate knitr code chunk. If something throws an error or looks weird, fix it.
Create a sequence from 1-100 by showing every 3 numbers.

```r
seq(1,100,3)
```

```
##  [1]   1   4   7  10  13  16  19  22  25  28  31  34  37  40  43  46  49
## [18]  52  55  58  61  64  67  70  73  76  79  82  85  88  91  94  97 100
```


Repeat the sequence a b ten times.

```r
rep(c("a","b"),10)
```

```
##  [1] "a" "b" "a" "b" "a" "b" "a" "b" "a" "b" "a" "b" "a" "b" "a" "b" "a"
## [18] "b" "a" "b"
```

Give a random distribution of 10 numbers and sort by their distribution.

```r
r <- runif(10); order(r)
```

```
##  [1]  3  8  5  9  6 10  1  7  4  2
```

What is 100 divided by 3?

```r
100 %/% 3
```

```
## [1] 33
```

List all the PMG mice that weigh 16 grams?

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
weight.mode<-sort(table(metadata$Weight), decreasing=TRUE)[1]
```

The mode of the mice weight is 12.


4.	Usign R commands, write the table to a new text file, but exclude the `Ear` and `Repro` columns.


```r
new.metadata1<-metadata[,-7]
new.metadata<-new.metadata1[,-8]
write.table(new.metadata, file="new.metadata.txt")
```

