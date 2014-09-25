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
  nrow(metadata)
  ```
  
  ```
  ## [1] 111
  ```
  There are 111 samples described in the `wild.metadata.txt`
  
  * How many columns are in the table? What are their names?
  
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
  FifteenPlus<-subset(metadata,Weight>=15)
  FifteenPlus
  ```
  
  ```
  ##         Date ET Station  SP Sex Age Repro Weight Ear
  ## 5_25m4  5_25  4     K19  PL   M   A   SCR   16.0  15
  ## 5_26m1  5_26  1     A12  PL   F   A    NE   19.5  14
  ## 5_26m9  5_26  9      M9  PL   F   A    NE   25.0  13
  ## 5_31m11 5_31 11      F2 PMG   F   J    NT   16.0  18
  ## 5_31m2  5_31  2     CC4  PL   M  SA   ABD   15.0  14
  ## 5_31m4  5_31  4     L18  PL   M   A   SCR   18.0  14
  ## 5_31m9  5_31  9      L7  PL   F   A    NE   30.0  15
  ## 6_14m1  6_14  1    AA13  PL   F   A    NE   22.0  14
  ## 6_14m23 6_14 20    AA18  PL   M   A   SCR   17.0  16
  ## 6_15m11 6_15 11      E2 PMG   F   A    NE   22.5  16
  ## 6_15m16 6_15 16     L11 PMG   M   A   SCR   16.0  17
  ## 6_15m20 6_15 20     M16  PL   M   A   SCR   17.0  16
  ## 6_15m24 6_15 24     M18 PMG   F  SA    NT   18.0  17
  ## 6_15m28 6_15 28     CC5  PL   M   A   SCR   17.5  14
  ## 6_15m2  6_15  2      B2  PL   M   A   SCR   17.0  14
  ## 6_15m33 6_15 33      A2 PMG   M   A   SCR   18.0  17
  ## 6_15m9  6_15  9      M8  PL   F   A    NE   26.0  16
  ## 6_16m33 6_16 33      B2 PMG   M   A   SCR   18.0  15
  ## 6_16m36 6_16 36     B19  PL   M   A   SCR   25.0  17
  ## 6_16m38 6_16 38     CC3 PMG   F   J    NT   17.0  18
  ## 6_17m2  6_17  2      E3  PL   M   A   SCR   18.0  14
  ## 6_17m7  6_17  7     I12 PMG   F   A    NE   21.0  17
  ## 6_1m10   6_1 10     B18  PL   F   J    NT   15.0  14
  ## 6_1m12   6_1 12     H18 PMG   M   A   SCR   16.0  14
  ## 6_1m2    6_1  2      D3  PL   M  SA   ABD   16.0  15
  ## 6_29m24 6_29 24     N20 PMG   F  SA    NE   17.0  15
  ## 6_29m25 6_29 25     P15 PMG   F   A    NE   23.0  16
  ## 6_29m34 6_29 34      P5 PMG   M  SA   SCR   15.0  16
  ## 6_29m38 6_29 38     CC2 PMG   F   A    NE   18.0  17
  ## 6_29m7  6_29  7      F8 PMG   F   A    NE   23.0  17
  ## 6_29m9  6_29  9      P6  PL   F   A    NE   27.0  15
  ## 6_2m10   6_2 10     D17  PL   F   J    NT   16.5  16
  ## 6_2m12   6_2 12     F19 PMG   M   A   SCR   18.0  17
  ## 6_30m24 6_30 24     N20 PMG   F   A    NE   17.0  15
  ## 6_30m2  6_30  2      B3  PL   M   A   SCR   19.0  15
  ## 6_30m33 6_30 33      F1 PMG   M   A   SCR   19.0  16
  ## 6_30m34 6_30 34      P6 PMG   M  SA   SCR   15.0  15
  ## 6_30m43 6_30 43    CC13 PMG   F   J     N   16.0  15
  ## 6_30m44 6_30 44     J16  PL   M  SA   SCR   17.0  17
  ## 6_5m13   6_5 13      N2 PMG   F   J    NT   18.0  17
  ## 6_5m16   6_5 16     H20 PMG   M   A   SCR   16.0  16
  ## 6_5m7    6_5  7     I11 PMG   F  SA    NT   22.0  16
  ## 7_13m1  7_13  1    AA13  PL   F   A    NE   23.5  14
  ## 7_13m25 7_13 25     P15 PMG   F   A    NE   18.5  15
  ## 7_13m34 7_13 34      D7 PMG   F  SA    NT   15.0  14
  ## 7_13m37 7_13 37     AA6  PL   F   A    NE   15.0  15
  ## 7_13m38 7_13 38     CC2 PMG   F   A    NT   22.5  18
  ## 7_13m46 7_13 46      N4 PMG   F   A    NT   21.0  16
  ## 7_13m57 7_13 57     L20  PL   F  SA    NE   15.5  15
  ## 7_13m61 7_13 61     CC6  PL   M   A   SCR   17.0  18
  ## 7_14m1  7_14  1    CC13  PL   F   A    NE   21.0  15
  ## 7_14m2  7_14  2     CC6  PL   M   A   SCR   18.5  13
  ## 7_14m21 7_14 21    AA10 PMG   F   A    NE   17.5  18
  ## 7_14m24 7_14 24     N19 PMG   F   A    NE   24.0  15
  ## 7_14m25 7_14 25     P16 PMG   F  SA    NE   18.0  16
  ## 7_14m33 7_14 33      P2 PMG   M   A   SCR   20.0  15
  ## 7_14m34 7_14 34      H6 PMG   M   A   SCR   17.5  16
  ## 7_14m35 7_14 35      J1 PMG   F   A    NE   23.0  17
  ## 7_14m38 7_14 38     CC2 PMG   F   A    NE   21.0  19
  ## 7_14m56 7_14 56     N20  PL   M   A   SCR   18.0  15
  ## 7_14m57 7_14 57     L19  PL   F  SA    NE   15.0  15
  ## 7_14m59 7_14 59     CC3 PMG   M  SA   SCR   16.0  17
  ## 7_14m61 7_14 61     CC5  PL   M   A   SCR   19.0  14
  ## 7_2m21   7_2 21      B8 PMG   F   A    NT   19.0  18
  ## 7_2m25   7_2 25     P17 PMG   F   A    NE   16.0  15
  ## 7_2m27   7_2 27     P11  PL   M  SA   ABD   15.0  16
  ## 7_2m38   7_2 38    AA20 PMG   F   A    NE   17.0  16
  ## 7_2m46   7_2 46      P2 PMG   F  SA    NT   15.0  15
  ## 7_2m52   7_2 52     L16 PMG   M   A   SCR   18.0  17
  ## 7_2m53   7_2 53     J17  PL   M  SA   SCR   17.0  14
  ## 7_2m56   7_2 56      N4  PL   M   A   SCR   16.0  16
  ## 7_3m2    7_3  2      A3  PL   M   A   SCR   19.0  17
  ## 7_3m20   7_3 20     M17  PL   M   A   SCR   17.0  18
  ## 7_3m34   7_3 34      P6 PMG   M  SA   SCR   15.0  17
  ## 7_3m38   7_3 38     CC3 PMG   F  SA    NT   17.0  19
  ## 7_3m43   7_3 43    CC13 PMG   F  SA    NT   16.0  16
  ## 7_3m44   7_3 44     N16  PL   M  SA   SCR   16.0  16
  ```
  
  ```r
  nrow(FifteenPlus)
  ```
  
  ```
  ## [1] 77
  ```
  77 mice weighed 15 or more grams
  
  * What is the median weight for the mice sampled?
  
  ```r
  median(metadata$Weight)
  ```
  
  ```
  ## [1] 16
  ```
  
  * How many PMG mice were there?
  
  ```r
  summary(metadata$"SP")
  ```
  
  ```
  ##  PL PMG 
  ##  58  53
  ```
  
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

