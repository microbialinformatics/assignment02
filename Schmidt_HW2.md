# Assignment 2
Marian L. Schmidt  
September 18, 2014  

>Complete the exercises listed below and submit as a pull request to the [Assignment 2 repository](http://www.github.com/microbialinformatics/assignment02).  Format this document approapriately using R markdown and knitr. I would like to see your code blocks and output in the final documents you submit. Your pull request needs to include your *.Rmd and *.md files. Do not alter the `.gitignore` file. You may work with a partner, but you must submit your own assignment and give credit to anyone that worked with you on the assignment.


```r
metadata <- read.table(file="wild.metadata.txt", header=T)
rownames(metadata) <- metadata$Group
metadata <- metadata[,-1]
```

*******************
>**1.  Calculate the following on the data we read in from the `wild.metadata.txt` file that we discussed in class on 9/16/2014.**


  *  *How many samples were described in the `wild.metadata.txt`?*  

```r
num_samps <- length(unique(row.names(metadata)))
```
**Answer:** *There are 111 samples described in the wild.metadata.txt.*
  
   
  *  *How many columns are in the table? What are their names*

```r
num_cols <- ncol(metadata)
name_cols <- colnames(metadata)
```
 **Answer:** *There are 9 columns in the table.  The name of the columns are Date, ET, Station, SP, Sex, Age, Repro, Weight, Ear.*
  
  *  *How many mice weighed 15 or more grams?*

```r
weight15a <- length(metadata$Weight[metadata$Weight < 15])
#OR
weight15b <- sum(metadata$Weight<15)
```
**Answer:** *34 mice weighed 15 grams or more.  Using the second line of code it is 34 .*
   
  *  *What is the median weight for the mice sampled?*

```r
median_weight <- median(metadata$Weight)
```
**Answer:** *The median weight for the mice sampled is 16.*

  *  *How many PMG mice were there?*

```r
num_PMG <- nrow(metadata[metadata$SP=="PMG",])
```
 **Answer:** *The number of PMG mice sampled is 53.*
 
  *  *How many female PL mice were there?*

```r
female_PL <- nrow(metadata[metadata$SP=="PMG" & metadata$Sex == "F",])
```
**Answer:** *The number of female PL mice sampled is 36.*
  
  *  *Alphabetize `wild.metadata.txt` by the ear tag number (only show the first 5 rows of the table)*

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
 
  *  *Sort the table by the weight of each animal*

```r
metadata <- metadata[order(metadata$Weight), ]
head(metadata)
```

```
##     Date ET Station  SP Sex Age Repro Weight Ear
## 66  6_16 37     A12  PL   M   J     A    7.0  12
## 108 7_14 74     N17 PMG   F   J    NT    7.0  14
## 12  5_25  3    BB18  PL   M   J   ABD    7.5  13
## 81  6_29 48      P7  PL   F   J    NT    9.0  11
## 90   7_2 54      H4  PL   F   J    NT    9.0  12
## 101  7_3 60     P11  PL   M   J     A    9.0  14
```
  
  *  *The `Station` column indicates where the mice were sampled. Where were the most mice captured?*

```r
which.max(table(metadata$Station)) #The second row in the output is the index of the value in the table
```

```
## N20 
##  70
```

```r
station <- table(metadata$Station)
station_mode <- station[70]; station_mode # The second row in the output is the number of samples at that station.
```

```
## N20 
##   4
```
**Answer:** *The most mice were sampled at station N20.*
  
  *  *How many mice were captured there?*

```r
num_PMGmice <- max(table(metadata$Station))
```
**Answer:** *4 were captured at N20.*
 
***************************

>**2.	Describe what each of the following commands does in a text block above the code, be specific. Put the code into the appropriate knitr code chunk. If something throws an error or looks weird, fix it.**


*  **Answer:** The following command generates a sequence of numbers that is every 3rd number between 1 and 100.


```r
seq(1,100,3)
```

```
##  [1]   1   4   7  10  13  16  19  22  25  28  31  34  37  40  43  46  49
## [18]  52  55  58  61  64  67  70  73  76  79  82  85  88  91  94  97 100
```


*  **Answer:** The following command first generates a sequence of "a" and "b" and then repeats it 10 times.


```r
rep(c("a","b"),10)
```

```
##  [1] "a" "b" "a" "b" "a" "b" "a" "b" "a" "b" "a" "b" "a" "b" "a" "b" "a"
## [18] "b" "a" "b"
```

*  **Answer:** The following commands are actually 2 lines of code separated by a semicolon.  The first line assigns a variable r, which are 10 random numbers from a uniform distribution.  The second function in the code (order(r)) tells us which element of the vector should be put 1st, 2nd, 3rd, and so on.  It is a way of telling us _how_ to sort the data.


```r
r <- runif(10); order(r)
```

```
##  [1]  4  8 10  5  3  2  1  7  6  9
```


*  **Answer:** The following code was modified from "100 % 3" to "100 %% 3", as "100 % 3" showed an error "unexpected input in "100 % 3."  100 %% 3 is a modulus binary operator (100 mod 3).


```r
100 %% 3
```

```
## [1] 1
```

*  **Answer:** The following code searches the rows of the metadata data frame for a mouse that is 16g that is species PMG.  First, the code creates a vector of trues/falses that say if the weight of the mouse is equal to 16g.  Second, another vector of trues and falses are created if the species is PMG.  Finally, both data frames are searched for matching "TRUE" values, which means there's a 16g mouse of species PMG.  For this combination, there's no match.


```r
metadata[metadata$Weight==16 && metadata$SP=="PMG",]
```

```
## [1] Date    ET      Station SP      Sex     Age     Repro   Weight  Ear    
## <0 rows> (or 0-length row.names)
```

**********************************

>**3.	Calculate the mode for the weight of the mice in `wild.metadata.txt`**


```r
weight <- metadata$Weight
weight <- table(as.vector(weight))
mode_weight <- names(weight)[weight == max(weight)]
```
**Answer:** *The mode for the weight of the mice is 16, 17.*

************************

>**4.	Usign R commands, write the table to a new text file, but exclude the `Ear` and `Repro` columns.**


```r
newdata <- metadata #Assign variable with metadata data frame
newdata$Ear = NULL; newdata$Repro = NULL #Delete Ear and Repro columns
write.csv(newdata, file = "metadata_exludes_Ear&Repro.csv")
```




```r
test <- newdata
test <- tableCat(test)
test <- cat(test, sep = "\n")
```

Date | ET | Station | SP | Sex | Age | Weight
--- | --- | --- | --- | --- | --- | ---
6_16 | 37 | A12 | PL | M | J |  7.0
7_14 | 74 | N17 | PMG | F | J |  7.0
5_25 |  3 | BB18 | PL | M | J |  7.5
6_29 | 48 | P7 | PL | F | J |  9.0
7_2 | 54 | H4 | PL | F | J |  9.0
7_3 | 60 | P11 | PL | M | J |  9.0
7_14 | 79 | J20 | PMG | F | J |  9.0
7_14 | 77 | F17 | PMG | M | J |  9.5
7_2 | 55 | P13 | PL | F | J | 10.0
6_5 | 21 | D13 | PMG | F | J | 10.5
7_3 | 51 | B18 | PMG | F | J | 11.0
6_16 | 18 | A13 | PL | M | SA | 11.5
6_2 | 14 | B6 | PL | M | J | 12.0
6_15 | 27 | J10 | PL | M | SA | 12.0
7_2 | 51 | B18 | PMG | F | J | 12.0
7_2 | 57 | N20 | PL | F | J | 12.0
7_14 | 71 | D20 | PL | F | J | 12.0
6_2 | 15 | N19 | PMG | F | J | 13.0
6_5 | 19 | L11 | PMG | M | J | 13.0
6_17 | 32 | J6 | PL | M | SA | 13.0
7_3 | 37 | CC6 | PL | F | SA | 13.0
7_13 | 54 | N3 | PL | F | SA | 13.0
7_3 | 57 | L19 | PL | F | J | 13.0
7_14 | 64 | B4 | PMG | M | J | 13.0
7_14 | 80 | N1 | PL | M | J | 13.0
6_16 | 32 | I6 | PL | M | J | 13.5
7_14 | 51 | B16 | PMG | F | SA | 13.5
7_14 | 54 | P1 | PL | F | J | 13.5
7_14 | 55 | L15 | PL | F | SA | 13.5
7_13 | 51 | B16 | PMG | F | J | 14.0
7_13 | 55 | J15 | PL | F | SA | 14.0
7_14 | 69 | H20 | PL | M | SA | 14.0
6_15 | 32 | D8 | PL | M | J | 14.5
7_13 | 69 | H20 | PL | M | SA | 14.5
5_31 |  2 | CC4 | PL | M | SA | 15.0
6_1 | 10 | B18 | PL | F | J | 15.0
7_2 | 27 | P11 | PL | M | SA | 15.0
6_29 | 34 | P5 | PMG | M | SA | 15.0
6_30 | 34 | P6 | PMG | M | SA | 15.0
7_13 | 34 | D7 | PMG | F | SA | 15.0
7_3 | 34 | P6 | PMG | M | SA | 15.0
7_13 | 37 | AA6 | PL | F | A | 15.0
7_2 | 46 | P2 | PMG | F | SA | 15.0
7_14 | 57 | L19 | PL | F | SA | 15.0
7_13 | 57 | L20 | PL | F | SA | 15.5
6_1 |  2 | D3 | PL | M | SA | 16.0
5_25 |  4 | K19 | PL | M | A | 16.0
5_31 | 11 | F2 | PMG | F | J | 16.0
6_1 | 12 | H18 | PMG | M | A | 16.0
6_15 | 16 | L11 | PMG | M | A | 16.0
6_5 | 16 | H20 | PMG | M | A | 16.0
7_2 | 25 | P17 | PMG | F | A | 16.0
6_30 | 43 | CC13 | PMG | F | J | 16.0
7_3 | 43 | CC13 | PMG | F | SA | 16.0
7_3 | 44 | N16 | PL | M | SA | 16.0
7_2 | 56 | N4 | PL | M | A | 16.0
7_14 | 59 | CC3 | PMG | M | SA | 16.0
6_2 | 10 | D17 | PL | F | J | 16.5
6_15 |  2 | B2 | PL | M | A | 17.0
6_14 | 20 | AA18 | PL | M | A | 17.0
6_15 | 20 | M16 | PL | M | A | 17.0
7_3 | 20 | M17 | PL | M | A | 17.0
6_29 | 24 | N20 | PMG | F | SA | 17.0
6_30 | 24 | N20 | PMG | F | A | 17.0
6_16 | 38 | CC3 | PMG | F | J | 17.0
7_2 | 38 | AA20 | PMG | F | A | 17.0
7_3 | 38 | CC3 | PMG | F | SA | 17.0
6_30 | 44 | J16 | PL | M | SA | 17.0
7_2 | 53 | J17 | PL | M | SA | 17.0
7_13 | 61 | CC6 | PL | M | A | 17.0
7_14 | 21 | AA10 | PMG | F | A | 17.5
6_15 | 28 | CC5 | PL | M | A | 17.5
7_14 | 34 | H6 | PMG | M | A | 17.5
6_17 |  2 | E3 | PL | M | A | 18.0
5_31 |  4 | L18 | PL | M | A | 18.0
6_2 | 12 | F19 | PMG | M | A | 18.0
6_5 | 13 | N2 | PMG | F | J | 18.0
6_15 | 24 | M18 | PMG | F | SA | 18.0
7_14 | 25 | P16 | PMG | F | SA | 18.0
6_15 | 33 | A2 | PMG | M | A | 18.0
6_16 | 33 | B2 | PMG | M | A | 18.0
6_29 | 38 | CC2 | PMG | F | A | 18.0
7_2 | 52 | L16 | PMG | M | A | 18.0
7_14 | 56 | N20 | PL | M | A | 18.0
7_14 |  2 | CC6 | PL | M | A | 18.5
7_13 | 25 | P15 | PMG | F | A | 18.5
6_30 |  2 | B3 | PL | M | A | 19.0
7_3 |  2 | A3 | PL | M | A | 19.0
7_2 | 21 | B8 | PMG | F | A | 19.0
6_30 | 33 | F1 | PMG | M | A | 19.0
7_14 | 61 | CC5 | PL | M | A | 19.0
5_26 |  1 | A12 | PL | F | A | 19.5
7_14 | 33 | P2 | PMG | M | A | 20.0
7_14 |  1 | CC13 | PL | F | A | 21.0
6_17 |  7 | I12 | PMG | F | A | 21.0
7_14 | 38 | CC2 | PMG | F | A | 21.0
7_13 | 46 | N4 | PMG | F | A | 21.0
6_14 |  1 | AA13 | PL | F | A | 22.0
6_5 |  7 | I11 | PMG | F | SA | 22.0
6_15 | 11 | E2 | PMG | F | A | 22.5
7_13 | 38 | CC2 | PMG | F | A | 22.5
6_29 |  7 | F8 | PMG | F | A | 23.0
6_29 | 25 | P15 | PMG | F | A | 23.0
7_14 | 35 | J1 | PMG | F | A | 23.0
7_13 |  1 | AA13 | PL | F | A | 23.5
7_14 | 24 | N19 | PMG | F | A | 24.0
5_26 |  9 | M9 | PL | F | A | 25.0
6_16 | 36 | B19 | PL | M | A | 25.0
6_15 |  9 | M8 | PL | F | A | 26.0
6_29 |  9 | P6 | PL | F | A | 27.0
5_31 |  9 | L7 | PL | F | A | 30.0


************************
