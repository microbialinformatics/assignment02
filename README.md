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
  There is one sample per row, so if I find the number of rows in the table, I know 
the number of samples. Here I am considering different samples from the same mouse
to be separate.

```r
num_rows <- nrow(metadata)
num_rows
```

```
## [1] 111
```

There are 111 samples in this table.

  * How many columns are in the table? What are their names?
  
  
  ```r
  num_col <- ncol(metadata)
  num_col
  ```
  
  ```
  ## [1] 9
  ```
  
  ```r
  #names of the columns
  colnames(metadata)
  ```
  
  ```
  ## [1] "Date"    "ET"      "Station" "SP"      "Sex"     "Age"     "Repro"  
  ## [8] "Weight"  "Ear"
  ```

The number of columns is 9 and the column names are 
Date, ET, Station, SP, Sex, Age, Repro, Weight, Ear

  * How many mice weighed 15 or more grams?
  
  I can find this by deleting replicate entries in the table, then subsetting the table
by weights to only include the mice that weigh more than 15 g.


```r
# I remove duplicates based on the their ear tag number
mouse.unique.mat <- metadata[!duplicated(metadata["ET"]),]
# then remove all mice with weights less than 15 g
weightGreater15 <- mouse.unique.mat[mouse.unique.mat["Weight"]>15,]
# then count the remaining rows
nrow(mouse.unique.mat)
```

```
## [1] 49
```

There are 49 mice with at least one recorded weight greater than 15 g.

  * What is the median weight for the mice sampled?
  
  

```r
median.weight <- median(metadata[,8])
```

The median weight is 16. Note - I first tried this with the command 
median(metadata["Weight"]), which returned an error message, indicating that the input file
subset by column name is not a numeric object. When extracted the weight values using the 
column number, R recognized them as a vector.


  * How many PMG mice were there?
  

```r
# first find the mouse records that have species "PMG" and subset the matrix
mouse.PMG <- metadata[metadata["SP"]=="PMG",]

# then remove duplicates

PMG.unique.mat <- mouse.PMG[!duplicated(mouse.PMG["ET"]),]
```

There are 53 separate records of PMG mice, and 23 unique
PMG mice.

  * How many female PL mice were there?
  

```r
# first I find the number of "PL" mice
mouse.PL <- metadata[metadata["SP"]=="PL",]

# then I find the number of those that are female

mouse.fem.PL <- mouse.PL[mouse.PL["Sex"]=="F",]

# remove duplicates

mouse.fem.PL.unique <- mouse.fem.PL[!duplicated(mouse.fem.PL["ET"]),]
```

There are 24 separate records of female PL mice, and 
9 individual female PL mice.

  * Alphabetize `wild.metadata.txt` by the ear tag number (only show the first 5 rows of the table)
  

```r
sorted <- metadata[order(metadata["ET"]),]
```

The first 5 rows of `metadata` sorted on ear tag number are: 


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
weight <- metadata[order(metadata["Weight"]),]
```

The table sorted by weight is:


```
##         Date ET Station  SP Sex Age Repro Weight Ear
## 6_16m37 6_16 37     A12  PL   M   J     A    7.0  12
## 7_14m74 7_14 74     N17 PMG   F   J    NT    7.0  14
## 5_25m3  5_25  3    BB18  PL   M   J   ABD    7.5  13
## 6_29m48 6_29 48      P7  PL   F   J    NT    9.0  11
## 7_14m79 7_14 79     J20 PMG   F   J    NT    9.0  12
## 7_2m54   7_2 54      H4  PL   F   J    NT    9.0  12
## 7_3m60   7_3 60     P11  PL   M   J     A    9.0  14
## 7_14m77 7_14 77     F17 PMG   M   J   ABD    9.5  15
## 7_2m55   7_2 55     P13  PL   F   J    NT   10.0  13
## 6_5m21   6_5 21     D13 PMG   F   J    NT   10.5  18
## 7_3m51   7_3 51     B18 PMG   F   J    NT   11.0  15
## 6_16m18 6_16 18     A13  PL   M  SA     A   11.5  14
## 6_15m27 6_15 27     J10  PL   M  SA   SCR   12.0  16
## 6_2m14   6_2 14      B6  PL   M   J   ABD   12.0  15
## 7_14m71 7_14 71     D20  PL   F   J    NT   12.0  14
## 7_2m51   7_2 51     B18 PMG   F   J     N   12.0  16
## 7_2m57   7_2 57     N20  PL   F   J    NT   12.0  15
## 6_17m32 6_17 32      J6  PL   M  SA   SCR   13.0  17
## 6_2m15   6_2 15     N19 PMG   F   J    NT   13.0  17
## 6_5m19   6_5 19     L11 PMG   M   J   SCR   13.0  18
## 7_13m54 7_13 54      N3  PL   F  SA    NT   13.0  14
## 7_14m64 7_14 64      B4 PMG   M   J   SCR   13.0  16
## 7_14m80 7_14 80      N1  PL   M   J   SCR   13.0  15
## 7_3m37   7_3 37     CC6  PL   F  SA     N   13.0  14
## 7_3m57   7_3 57     L19  PL   F   J    NT   13.0  15
## 6_16m32 6_16 32      I6  PL   M   J   SCR   13.5  17
## 7_14m51 7_14 51     B16 PMG   F  SA    NT   13.5  17
## 7_14m54 7_14 54      P1  PL   F   J    NE   13.5  15
## 7_14m55 7_14 55     L15  PL   F  SA    NT   13.5  14
## 7_13m51 7_13 51     B16 PMG   F   J    NT   14.0  17
## 7_13m55 7_13 55     J15  PL   F  SA    NT   14.0  14
## 7_14m69 7_14 69     H20  PL   M  SA   ABD   14.0  12
## 6_15m32 6_15 32      D8  PL   M   J   ABD   14.5  17
## 7_13m69 7_13 69     H20  PL   M  SA   SCR   14.5  12
## 5_31m2  5_31  2     CC4  PL   M  SA   ABD   15.0  14
## 6_1m10   6_1 10     B18  PL   F   J    NT   15.0  14
## 6_29m34 6_29 34      P5 PMG   M  SA   SCR   15.0  16
## 6_30m34 6_30 34      P6 PMG   M  SA   SCR   15.0  15
## 7_13m34 7_13 34      D7 PMG   F  SA    NT   15.0  14
## 7_13m37 7_13 37     AA6  PL   F   A    NE   15.0  15
## 7_14m57 7_14 57     L19  PL   F  SA    NE   15.0  15
## 7_2m27   7_2 27     P11  PL   M  SA   ABD   15.0  16
## 7_2m46   7_2 46      P2 PMG   F  SA    NT   15.0  15
## 7_3m34   7_3 34      P6 PMG   M  SA   SCR   15.0  17
## 7_13m57 7_13 57     L20  PL   F  SA    NE   15.5  15
## 5_25m4  5_25  4     K19  PL   M   A   SCR   16.0  15
## 5_31m11 5_31 11      F2 PMG   F   J    NT   16.0  18
## 6_15m16 6_15 16     L11 PMG   M   A   SCR   16.0  17
## 6_1m12   6_1 12     H18 PMG   M   A   SCR   16.0  14
## 6_1m2    6_1  2      D3  PL   M  SA   ABD   16.0  15
## 6_30m43 6_30 43    CC13 PMG   F   J     N   16.0  15
## 6_5m16   6_5 16     H20 PMG   M   A   SCR   16.0  16
## 7_14m59 7_14 59     CC3 PMG   M  SA   SCR   16.0  17
## 7_2m25   7_2 25     P17 PMG   F   A    NE   16.0  15
## 7_2m56   7_2 56      N4  PL   M   A   SCR   16.0  16
## 7_3m43   7_3 43    CC13 PMG   F  SA    NT   16.0  16
## 7_3m44   7_3 44     N16  PL   M  SA   SCR   16.0  16
## 6_2m10   6_2 10     D17  PL   F   J    NT   16.5  16
## 6_14m23 6_14 20    AA18  PL   M   A   SCR   17.0  16
## 6_15m20 6_15 20     M16  PL   M   A   SCR   17.0  16
## 6_15m2  6_15  2      B2  PL   M   A   SCR   17.0  14
## 6_16m38 6_16 38     CC3 PMG   F   J    NT   17.0  18
## 6_29m24 6_29 24     N20 PMG   F  SA    NE   17.0  15
## 6_30m24 6_30 24     N20 PMG   F   A    NE   17.0  15
## 6_30m44 6_30 44     J16  PL   M  SA   SCR   17.0  17
## 7_13m61 7_13 61     CC6  PL   M   A   SCR   17.0  18
## 7_2m38   7_2 38    AA20 PMG   F   A    NE   17.0  16
## 7_2m53   7_2 53     J17  PL   M  SA   SCR   17.0  14
## 7_3m20   7_3 20     M17  PL   M   A   SCR   17.0  18
## 7_3m38   7_3 38     CC3 PMG   F  SA    NT   17.0  19
## 6_15m28 6_15 28     CC5  PL   M   A   SCR   17.5  14
## 7_14m21 7_14 21    AA10 PMG   F   A    NE   17.5  18
## 7_14m34 7_14 34      H6 PMG   M   A   SCR   17.5  16
## 5_31m4  5_31  4     L18  PL   M   A   SCR   18.0  14
## 6_15m24 6_15 24     M18 PMG   F  SA    NT   18.0  17
## 6_15m33 6_15 33      A2 PMG   M   A   SCR   18.0  17
## 6_16m33 6_16 33      B2 PMG   M   A   SCR   18.0  15
## 6_17m2  6_17  2      E3  PL   M   A   SCR   18.0  14
## 6_29m38 6_29 38     CC2 PMG   F   A    NE   18.0  17
## 6_2m12   6_2 12     F19 PMG   M   A   SCR   18.0  17
## 6_5m13   6_5 13      N2 PMG   F   J    NT   18.0  17
## 7_14m25 7_14 25     P16 PMG   F  SA    NE   18.0  16
## 7_14m56 7_14 56     N20  PL   M   A   SCR   18.0  15
## 7_2m52   7_2 52     L16 PMG   M   A   SCR   18.0  17
## 7_13m25 7_13 25     P15 PMG   F   A    NE   18.5  15
## 7_14m2  7_14  2     CC6  PL   M   A   SCR   18.5  13
## 6_30m2  6_30  2      B3  PL   M   A   SCR   19.0  15
## 6_30m33 6_30 33      F1 PMG   M   A   SCR   19.0  16
## 7_14m61 7_14 61     CC5  PL   M   A   SCR   19.0  14
## 7_2m21   7_2 21      B8 PMG   F   A    NT   19.0  18
## 7_3m2    7_3  2      A3  PL   M   A   SCR   19.0  17
## 5_26m1  5_26  1     A12  PL   F   A    NE   19.5  14
## 7_14m33 7_14 33      P2 PMG   M   A   SCR   20.0  15
## 6_17m7  6_17  7     I12 PMG   F   A    NE   21.0  17
## 7_13m46 7_13 46      N4 PMG   F   A    NT   21.0  16
## 7_14m1  7_14  1    CC13  PL   F   A    NE   21.0  15
## 7_14m38 7_14 38     CC2 PMG   F   A    NE   21.0  19
## 6_14m1  6_14  1    AA13  PL   F   A    NE   22.0  14
## 6_5m7    6_5  7     I11 PMG   F  SA    NT   22.0  16
## 6_15m11 6_15 11      E2 PMG   F   A    NE   22.5  16
## 7_13m38 7_13 38     CC2 PMG   F   A    NT   22.5  18
## 6_29m25 6_29 25     P15 PMG   F   A    NE   23.0  16
## 6_29m7  6_29  7      F8 PMG   F   A    NE   23.0  17
## 7_14m35 7_14 35      J1 PMG   F   A    NE   23.0  17
## 7_13m1  7_13  1    AA13  PL   F   A    NE   23.5  14
## 7_14m24 7_14 24     N19 PMG   F   A    NE   24.0  15
## 5_26m9  5_26  9      M9  PL   F   A    NE   25.0  13
## 6_16m36 6_16 36     B19  PL   M   A   SCR   25.0  17
## 6_15m9  6_15  9      M8  PL   F   A    NE   26.0  16
## 6_29m9  6_29  9      P6  PL   F   A    NE   27.0  15
## 5_31m9  5_31  9      L7  PL   F   A    NE   30.0  15
```

  * The `Station` column indicates where the mice were sampled. Where were the most mice captured?
  

```r
best.station <- sort(table(metadata["Station"]), decreasing=TRUE)[1]
```

The station where the most mice were sampled was N20.

  * How many mice were captured there?


```r
N20mice <- metadata[metadata["Station"]=="N20",]

N20.unique <- N20mice[!duplicated(N20mice["ET"]),]
```

There were 4 captures of 3 unique individuals at 
station N20.


2.	Describe what each of the following commands does in a text block above the code, be specific. Put the code into the appropriate knitr code chunk. If something throws an error or looks weird, fix it.

```
seq(1,100,3)
```
This code gives us a sequence of numbers begining at 1 and going to 100, increasing by 3 at each step

```
rep(c("a","b"),10)
```
This code repeats the letters a and b ten times.

```
r <- runif(10); order(r)
```
This code generates 10 numbers drawn from a uniform distribution between 0 and 1. For each element of the vector r, the "order" code gives that element's place in a ranked vector that places the elements of r in order from lowest to highest.

To get the final output vector 6.4977 &times; 10<sup>-4</sup>, 0.0215, 0.1, 0.1308, 0.3657, 0.3745, 0.504, 0.5543, 0.8798, 0.9641, you subset the vector r by the vector rr, using the code


```r
r[rr]
```

```
100 % 3
```

As far as I can tell, the % sign is not an operator on its own in R. The %% is the modulus operator, which gives the remainder when the first number is divided by the second.


```r
100 %% 3
```

```
## [1] 1
```



```
metadata[metadata$weight==16 && metadata$SP=="PMG",]
```

This operator subsets the table metadata such that it only shows the individuals that are both of the species PMG and weigh 16 g. For this case, the && operator returns an error, while the & operator returns the (presumable) table of interest.



3.	Calculate the mode for the weight of the mice in `wild.metadata.txt`


4.	Usign R commands, write the table to a new text file, but exclude the `Ear` and `Repro` columns.

