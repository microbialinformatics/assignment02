# Assignment 2
Shawn Whitefield  
September 16, 2014  

Complete the exercises listed below and submit as a pull request to the [Assignment 2 repository](http://www.github.com/microbialinformatics/assignment02).  Format this document approapriately using R markdown and knitr. I would like to see your code blocks and output in the final documents you submit. Your pull request needs to include your *.Rmd and *.md files. Do not alter the `.gitignore` file. You may work with a partner, but you must submit your own assignment and give credit to anyone that worked with you on the assignment.


```r
metadata <- read.table(file="wild.metadata.txt", header=T)
rownames(metadata) <- metadata$Group
metadata <- metadata[,-1]
```

1.  Calculate the following on the data we read in from the `wild.metadata.txt` file that we discussed in class on 9/16/2014.

  * How many samples were described in the `wild.metadata.txt`?


```r
## getting summary information
summary(metadata)
```

```
##       Date          ET          Station     SP     Sex    Age     Repro   
##  7_14   :23   Min.   : 1.0   N20    : 4   PL :58   F:60   A :51   A  : 3  
##  7_13   :12   1st Qu.:13.5   B18    : 3   PMG:53   M:51   J :30   ABD: 8  
##  7_2    :12   Median :33.0   CC13   : 3                   SA:30   N  : 3  
##  6_15   :10   Mean   :32.3   CC2    : 3                           NE :27  
##  7_3    :10   3rd Qu.:51.0   CC3    : 3                           NT :30  
##  6_29   : 7   Max.   :80.0   CC6    : 3                           SCR:40  
##  (Other):37                  (Other):92                                   
##      Weight          Ear      
##  Min.   : 7.0   Min.   :11.0  
##  1st Qu.:13.5   1st Qu.:14.0  
##  Median :16.0   Median :15.0  
##  Mean   :16.4   Mean   :15.4  
##  3rd Qu.:18.0   3rd Qu.:17.0  
##  Max.   :30.0   Max.   :19.0  
## 
```

```r
# getting number of observations in metadata file
obs <-nrow(metadata)
obs
```

```
## [1] 111
```
 Answer: there are 111 samples in wild.metadata.txt.
 
 * How many columns are in the table? What are their names?

```r
#getting column number
columns<-ncol(metadata)
columns
```

```
## [1] 9
```

```r
#getting column names
metadatanames<-colnames(metadata)
```
Answer: There are 9. They are called; Date, ET, Station, SP, Sex, Age, Repro, Weight, Ear

* How many mice weighed 15 or more grams?

```r
# There are repeat measurements for the same mouse
#First, assess how many individual mice are in the file
  # making ET a factor
factor(metadata$ET)
```

```
##   [1] 3  4  1  9  11 2  4  9  1  20 11 16 20 24 27 28 2  32 33 9  18 32 33
##  [24] 36 37 38 2  32 7  10 12 2  24 25 34 38 48 7  9  10 12 14 15 24 2  33
##  [47] 34 43 44 13 16 19 21 7  1  25 34 37 38 46 51 54 55 57 61 69 1  2  21
##  [70] 24 25 33 34 35 38 51 54 55 56 57 59 61 64 69 71 74 77 79 80 21 25 27
##  [93] 38 46 51 52 53 54 55 56 57 2  20 34 37 38 43 44 51 57 60
## 49 Levels: 1 2 3 4 7 9 10 11 12 13 14 15 16 18 19 20 21 24 25 27 28 ... 80
```

```r
metadata$ET<-factor(metadata$ET)
#checking work
levels(metadata$ET)
```

```
##  [1] "1"  "2"  "3"  "4"  "7"  "9"  "10" "11" "12" "13" "14" "15" "16" "18"
## [15] "19" "20" "21" "24" "25" "27" "28" "32" "33" "34" "35" "36" "37" "38"
## [29] "43" "44" "46" "48" "51" "52" "53" "54" "55" "56" "57" "59" "60" "61"
## [43] "64" "69" "71" "74" "77" "79" "80"
```

```r
summary(metadata)
```

```
##       Date          ET        Station     SP     Sex    Age     Repro   
##  7_14   :23   2      : 7   N20    : 4   PL :58   F:60   A :51   A  : 3  
##  7_13   :12   38     : 6   B18    : 3   PMG:53   M:51   J :30   ABD: 8  
##  7_2    :12   34     : 5   CC13   : 3                   SA:30   N  : 3  
##  6_15   :10   1      : 4   CC2    : 3                           NE :27  
##  7_3    :10   9      : 4   CC3    : 3                           NT :30  
##  6_29   : 7   24     : 4   CC6    : 3                           SCR:40  
##  (Other):37   (Other):81   (Other):92                                   
##      Weight          Ear      
##  Min.   : 7.0   Min.   :11.0  
##  1st Qu.:13.5   1st Qu.:14.0  
##  Median :16.0   Median :15.0  
##  Mean   :16.4   Mean   :15.4  
##  3rd Qu.:18.0   3rd Qu.:17.0  
##  Max.   :30.0   Max.   :19.0  
## 
```

```r
head(metadata)
```

```
##         Date ET Station  SP Sex Age Repro Weight Ear
## 5_25m3  5_25  3    BB18  PL   M   J   ABD    7.5  13
## 5_25m4  5_25  4     K19  PL   M   A   SCR   16.0  15
## 5_26m1  5_26  1     A12  PL   F   A    NE   19.5  14
## 5_26m9  5_26  9      M9  PL   F   A    NE   25.0  13
## 5_31m11 5_31 11      F2 PMG   F   J    NT   16.0  18
## 5_31m2  5_31  2     CC4  PL   M  SA   ABD   15.0  14
```

```r
#There are 49 individual mice
#subsetting for weight >= 15, calling this set weightet
weightet<- subset(metadata, Weight>=15)
weightet
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
#check work
levels(weightet$ET)
```

```
##  [1] "1"  "2"  "3"  "4"  "7"  "9"  "10" "11" "12" "13" "14" "15" "16" "18"
## [15] "19" "20" "21" "24" "25" "27" "28" "32" "33" "34" "35" "36" "37" "38"
## [29] "43" "44" "46" "48" "51" "52" "53" "54" "55" "56" "57" "59" "60" "61"
## [43] "64" "69" "71" "74" "77" "79" "80"
```

```r
#determine number of individual mice (ET) in weightet
uniquebigmice<- sort(weightet$ET)
nunique<-unique(uniquebigmice)
uniquemice<-length(unique(nunique))
uniquemice
```

```
## [1] 31
```
Answer: There are 77 observations from 31 mice with weights greater than or equal to 15 grams


What is the median weight for the mice sampled?

```r
#assuming this means meadian over all weight observations
medianmouseweight<-median(metadata$Weight)
medianmouseweight
```

```
## [1] 16
```
Answer: median weight among all observations is 16



* How many PMG mice were there?

```r
#using summary feature to look at number in SP categories
summary(metadata)
```

```
##       Date          ET        Station     SP     Sex    Age     Repro   
##  7_14   :23   2      : 7   N20    : 4   PL :58   F:60   A :51   A  : 3  
##  7_13   :12   38     : 6   B18    : 3   PMG:53   M:51   J :30   ABD: 8  
##  7_2    :12   34     : 5   CC13   : 3                   SA:30   N  : 3  
##  6_15   :10   1      : 4   CC2    : 3                           NE :27  
##  7_3    :10   9      : 4   CC3    : 3                           NT :30  
##  6_29   : 7   24     : 4   CC6    : 3                           SCR:40  
##  (Other):37   (Other):81   (Other):92                                   
##      Weight          Ear      
##  Min.   : 7.0   Min.   :11.0  
##  1st Qu.:13.5   1st Qu.:14.0  
##  Median :16.0   Median :15.0  
##  Mean   :16.4   Mean   :15.4  
##  3rd Qu.:18.0   3rd Qu.:17.0  
##  Max.   :30.0   Max.   :19.0  
## 
```

```r
#subsetting for only PMG values of SP
nPMG<- metadata[ which(metadata$SP=='PMG'), ]
#listing number of unique ET (mice) with PMG
sortnPMG<- sort(nPMG$ET)
sortnPMG
```

```
##  [1] 7  7  7  11 11 12 12 13 15 16 16 19 21 21 21 24 24 24 24 25 25 25 25
## [24] 33 33 33 33 34 34 34 34 34 35 38 38 38 38 38 38 43 43 46 46 51 51 51
## [47] 51 52 59 64 74 77 79
## 49 Levels: 1 2 3 4 7 9 10 11 12 13 14 15 16 18 19 20 21 24 25 27 28 ... 80
```

```r
unique(sortnPMG)
```

```
##  [1] 7  11 12 13 15 16 19 21 24 25 33 34 35 38 43 46 51 52 59 64 74 77 79
## 49 Levels: 1 2 3 4 7 9 10 11 12 13 14 15 16 18 19 20 21 24 25 27 28 ... 80
```

```r
nPMGmice<-length(unique(sortnPMG))
```
Answer: There are 53 observations of PMG from 23 mice


* How many female PL mice were there?

```r
#selecting for SP = PL
nPL<- metadata[ which(metadata$SP=='PL'), ]
#checking work
nPL
```

```
##         Date ET Station SP Sex Age Repro Weight Ear
## 5_25m3  5_25  3    BB18 PL   M   J   ABD    7.5  13
## 5_25m4  5_25  4     K19 PL   M   A   SCR   16.0  15
## 5_26m1  5_26  1     A12 PL   F   A    NE   19.5  14
## 5_26m9  5_26  9      M9 PL   F   A    NE   25.0  13
## 5_31m2  5_31  2     CC4 PL   M  SA   ABD   15.0  14
## 5_31m4  5_31  4     L18 PL   M   A   SCR   18.0  14
## 5_31m9  5_31  9      L7 PL   F   A    NE   30.0  15
## 6_14m1  6_14  1    AA13 PL   F   A    NE   22.0  14
## 6_14m23 6_14 20    AA18 PL   M   A   SCR   17.0  16
## 6_15m20 6_15 20     M16 PL   M   A   SCR   17.0  16
## 6_15m27 6_15 27     J10 PL   M  SA   SCR   12.0  16
## 6_15m28 6_15 28     CC5 PL   M   A   SCR   17.5  14
## 6_15m2  6_15  2      B2 PL   M   A   SCR   17.0  14
## 6_15m32 6_15 32      D8 PL   M   J   ABD   14.5  17
## 6_15m9  6_15  9      M8 PL   F   A    NE   26.0  16
## 6_16m18 6_16 18     A13 PL   M  SA     A   11.5  14
## 6_16m32 6_16 32      I6 PL   M   J   SCR   13.5  17
## 6_16m36 6_16 36     B19 PL   M   A   SCR   25.0  17
## 6_16m37 6_16 37     A12 PL   M   J     A    7.0  12
## 6_17m2  6_17  2      E3 PL   M   A   SCR   18.0  14
## 6_17m32 6_17 32      J6 PL   M  SA   SCR   13.0  17
## 6_1m10   6_1 10     B18 PL   F   J    NT   15.0  14
## 6_1m2    6_1  2      D3 PL   M  SA   ABD   16.0  15
## 6_29m48 6_29 48      P7 PL   F   J    NT    9.0  11
## 6_29m9  6_29  9      P6 PL   F   A    NE   27.0  15
## 6_2m10   6_2 10     D17 PL   F   J    NT   16.5  16
## 6_2m14   6_2 14      B6 PL   M   J   ABD   12.0  15
## 6_30m2  6_30  2      B3 PL   M   A   SCR   19.0  15
## 6_30m44 6_30 44     J16 PL   M  SA   SCR   17.0  17
## 7_13m1  7_13  1    AA13 PL   F   A    NE   23.5  14
## 7_13m37 7_13 37     AA6 PL   F   A    NE   15.0  15
## 7_13m54 7_13 54      N3 PL   F  SA    NT   13.0  14
## 7_13m55 7_13 55     J15 PL   F  SA    NT   14.0  14
## 7_13m57 7_13 57     L20 PL   F  SA    NE   15.5  15
## 7_13m61 7_13 61     CC6 PL   M   A   SCR   17.0  18
## 7_13m69 7_13 69     H20 PL   M  SA   SCR   14.5  12
## 7_14m1  7_14  1    CC13 PL   F   A    NE   21.0  15
## 7_14m2  7_14  2     CC6 PL   M   A   SCR   18.5  13
## 7_14m54 7_14 54      P1 PL   F   J    NE   13.5  15
## 7_14m55 7_14 55     L15 PL   F  SA    NT   13.5  14
## 7_14m56 7_14 56     N20 PL   M   A   SCR   18.0  15
## 7_14m57 7_14 57     L19 PL   F  SA    NE   15.0  15
## 7_14m61 7_14 61     CC5 PL   M   A   SCR   19.0  14
## 7_14m69 7_14 69     H20 PL   M  SA   ABD   14.0  12
## 7_14m71 7_14 71     D20 PL   F   J    NT   12.0  14
## 7_14m80 7_14 80      N1 PL   M   J   SCR   13.0  15
## 7_2m27   7_2 27     P11 PL   M  SA   ABD   15.0  16
## 7_2m53   7_2 53     J17 PL   M  SA   SCR   17.0  14
## 7_2m54   7_2 54      H4 PL   F   J    NT    9.0  12
## 7_2m55   7_2 55     P13 PL   F   J    NT   10.0  13
## 7_2m56   7_2 56      N4 PL   M   A   SCR   16.0  16
## 7_2m57   7_2 57     N20 PL   F   J    NT   12.0  15
## 7_3m2    7_3  2      A3 PL   M   A   SCR   19.0  17
## 7_3m20   7_3 20     M17 PL   M   A   SCR   17.0  18
## 7_3m37   7_3 37     CC6 PL   F  SA     N   13.0  14
## 7_3m44   7_3 44     N16 PL   M  SA   SCR   16.0  16
## 7_3m57   7_3 57     L19 PL   F   J    NT   13.0  15
## 7_3m60   7_3 60     P11 PL   M   J     A    9.0  14
```

```r
#getting summary of the Sex variable
PLmousesex<-summary(nPL$Sex)
#saving the summary of PL mouse Sex variable as a vector
femalePL<-PLmousesex["F"]
#checking work
num<-print(unname(femalePL))
```

```
## [1] 24
```

```r
num
```

```
## [1] 24
```
Answer: There are 24 female PL mice


* Alphabetize `wild.metadata.txt` by the ear tag number (only show the first 5 rows of the table) 

```r
wild.metadata <- read.table(file="wild.metadata.txt", header=T)
sortbyet<-wild.metadata[order(metadata$ET),]
sortbyet[1:5,]
```

```
##     Group Date ET Station SP Sex Age Repro Weight Ear
## 3  5_26m1 5_26  1     A12 PL   F   A    NE   19.5  14
## 9  6_14m1 6_14  1    AA13 PL   F   A    NE   22.0  14
## 55 7_13m1 7_13  1    AA13 PL   F   A    NE   23.5  14
## 67 7_14m1 7_14  1    CC13 PL   F   A    NE   21.0  15
## 6  5_31m2 5_31  2     CC4 PL   M  SA   ABD   15.0  14
```

* Sort the table by the weight of each animal

```r
#sorting table by weight
byweighttable<-metadata[order(metadata$Weight),]
byweighttable
```

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

```r
#there are multiple weights per animal(EarTag)
#sorting by ET and then by weight
byweight<-metadata[order(metadata$ET,metadata$Weight),]
byweight
```

```
##         Date ET Station  SP Sex Age Repro Weight Ear
## 5_26m1  5_26  1     A12  PL   F   A    NE   19.5  14
## 7_14m1  7_14  1    CC13  PL   F   A    NE   21.0  15
## 6_14m1  6_14  1    AA13  PL   F   A    NE   22.0  14
## 7_13m1  7_13  1    AA13  PL   F   A    NE   23.5  14
## 5_31m2  5_31  2     CC4  PL   M  SA   ABD   15.0  14
## 6_1m2    6_1  2      D3  PL   M  SA   ABD   16.0  15
## 6_15m2  6_15  2      B2  PL   M   A   SCR   17.0  14
## 6_17m2  6_17  2      E3  PL   M   A   SCR   18.0  14
## 7_14m2  7_14  2     CC6  PL   M   A   SCR   18.5  13
## 6_30m2  6_30  2      B3  PL   M   A   SCR   19.0  15
## 7_3m2    7_3  2      A3  PL   M   A   SCR   19.0  17
## 5_25m3  5_25  3    BB18  PL   M   J   ABD    7.5  13
## 5_25m4  5_25  4     K19  PL   M   A   SCR   16.0  15
## 5_31m4  5_31  4     L18  PL   M   A   SCR   18.0  14
## 6_17m7  6_17  7     I12 PMG   F   A    NE   21.0  17
## 6_5m7    6_5  7     I11 PMG   F  SA    NT   22.0  16
## 6_29m7  6_29  7      F8 PMG   F   A    NE   23.0  17
## 5_26m9  5_26  9      M9  PL   F   A    NE   25.0  13
## 6_15m9  6_15  9      M8  PL   F   A    NE   26.0  16
## 6_29m9  6_29  9      P6  PL   F   A    NE   27.0  15
## 5_31m9  5_31  9      L7  PL   F   A    NE   30.0  15
## 6_1m10   6_1 10     B18  PL   F   J    NT   15.0  14
## 6_2m10   6_2 10     D17  PL   F   J    NT   16.5  16
## 5_31m11 5_31 11      F2 PMG   F   J    NT   16.0  18
## 6_15m11 6_15 11      E2 PMG   F   A    NE   22.5  16
## 6_1m12   6_1 12     H18 PMG   M   A   SCR   16.0  14
## 6_2m12   6_2 12     F19 PMG   M   A   SCR   18.0  17
## 6_5m13   6_5 13      N2 PMG   F   J    NT   18.0  17
## 6_2m14   6_2 14      B6  PL   M   J   ABD   12.0  15
## 6_2m15   6_2 15     N19 PMG   F   J    NT   13.0  17
## 6_15m16 6_15 16     L11 PMG   M   A   SCR   16.0  17
## 6_5m16   6_5 16     H20 PMG   M   A   SCR   16.0  16
## 6_16m18 6_16 18     A13  PL   M  SA     A   11.5  14
## 6_5m19   6_5 19     L11 PMG   M   J   SCR   13.0  18
## 6_14m23 6_14 20    AA18  PL   M   A   SCR   17.0  16
## 6_15m20 6_15 20     M16  PL   M   A   SCR   17.0  16
## 7_3m20   7_3 20     M17  PL   M   A   SCR   17.0  18
## 6_5m21   6_5 21     D13 PMG   F   J    NT   10.5  18
## 7_14m21 7_14 21    AA10 PMG   F   A    NE   17.5  18
## 7_2m21   7_2 21      B8 PMG   F   A    NT   19.0  18
## 6_29m24 6_29 24     N20 PMG   F  SA    NE   17.0  15
## 6_30m24 6_30 24     N20 PMG   F   A    NE   17.0  15
## 6_15m24 6_15 24     M18 PMG   F  SA    NT   18.0  17
## 7_14m24 7_14 24     N19 PMG   F   A    NE   24.0  15
## 7_2m25   7_2 25     P17 PMG   F   A    NE   16.0  15
## 7_14m25 7_14 25     P16 PMG   F  SA    NE   18.0  16
## 7_13m25 7_13 25     P15 PMG   F   A    NE   18.5  15
## 6_29m25 6_29 25     P15 PMG   F   A    NE   23.0  16
## 6_15m27 6_15 27     J10  PL   M  SA   SCR   12.0  16
## 7_2m27   7_2 27     P11  PL   M  SA   ABD   15.0  16
## 6_15m28 6_15 28     CC5  PL   M   A   SCR   17.5  14
## 6_17m32 6_17 32      J6  PL   M  SA   SCR   13.0  17
## 6_16m32 6_16 32      I6  PL   M   J   SCR   13.5  17
## 6_15m32 6_15 32      D8  PL   M   J   ABD   14.5  17
## 6_15m33 6_15 33      A2 PMG   M   A   SCR   18.0  17
## 6_16m33 6_16 33      B2 PMG   M   A   SCR   18.0  15
## 6_30m33 6_30 33      F1 PMG   M   A   SCR   19.0  16
## 7_14m33 7_14 33      P2 PMG   M   A   SCR   20.0  15
## 6_29m34 6_29 34      P5 PMG   M  SA   SCR   15.0  16
## 6_30m34 6_30 34      P6 PMG   M  SA   SCR   15.0  15
## 7_13m34 7_13 34      D7 PMG   F  SA    NT   15.0  14
## 7_3m34   7_3 34      P6 PMG   M  SA   SCR   15.0  17
## 7_14m34 7_14 34      H6 PMG   M   A   SCR   17.5  16
## 7_14m35 7_14 35      J1 PMG   F   A    NE   23.0  17
## 6_16m36 6_16 36     B19  PL   M   A   SCR   25.0  17
## 6_16m37 6_16 37     A12  PL   M   J     A    7.0  12
## 7_3m37   7_3 37     CC6  PL   F  SA     N   13.0  14
## 7_13m37 7_13 37     AA6  PL   F   A    NE   15.0  15
## 6_16m38 6_16 38     CC3 PMG   F   J    NT   17.0  18
## 7_2m38   7_2 38    AA20 PMG   F   A    NE   17.0  16
## 7_3m38   7_3 38     CC3 PMG   F  SA    NT   17.0  19
## 6_29m38 6_29 38     CC2 PMG   F   A    NE   18.0  17
## 7_14m38 7_14 38     CC2 PMG   F   A    NE   21.0  19
## 7_13m38 7_13 38     CC2 PMG   F   A    NT   22.5  18
## 6_30m43 6_30 43    CC13 PMG   F   J     N   16.0  15
## 7_3m43   7_3 43    CC13 PMG   F  SA    NT   16.0  16
## 7_3m44   7_3 44     N16  PL   M  SA   SCR   16.0  16
## 6_30m44 6_30 44     J16  PL   M  SA   SCR   17.0  17
## 7_2m46   7_2 46      P2 PMG   F  SA    NT   15.0  15
## 7_13m46 7_13 46      N4 PMG   F   A    NT   21.0  16
## 6_29m48 6_29 48      P7  PL   F   J    NT    9.0  11
## 7_3m51   7_3 51     B18 PMG   F   J    NT   11.0  15
## 7_2m51   7_2 51     B18 PMG   F   J     N   12.0  16
## 7_14m51 7_14 51     B16 PMG   F  SA    NT   13.5  17
## 7_13m51 7_13 51     B16 PMG   F   J    NT   14.0  17
## 7_2m52   7_2 52     L16 PMG   M   A   SCR   18.0  17
## 7_2m53   7_2 53     J17  PL   M  SA   SCR   17.0  14
## 7_2m54   7_2 54      H4  PL   F   J    NT    9.0  12
## 7_13m54 7_13 54      N3  PL   F  SA    NT   13.0  14
## 7_14m54 7_14 54      P1  PL   F   J    NE   13.5  15
## 7_2m55   7_2 55     P13  PL   F   J    NT   10.0  13
## 7_14m55 7_14 55     L15  PL   F  SA    NT   13.5  14
## 7_13m55 7_13 55     J15  PL   F  SA    NT   14.0  14
## 7_2m56   7_2 56      N4  PL   M   A   SCR   16.0  16
## 7_14m56 7_14 56     N20  PL   M   A   SCR   18.0  15
## 7_2m57   7_2 57     N20  PL   F   J    NT   12.0  15
## 7_3m57   7_3 57     L19  PL   F   J    NT   13.0  15
## 7_14m57 7_14 57     L19  PL   F  SA    NE   15.0  15
## 7_13m57 7_13 57     L20  PL   F  SA    NE   15.5  15
## 7_14m59 7_14 59     CC3 PMG   M  SA   SCR   16.0  17
## 7_3m60   7_3 60     P11  PL   M   J     A    9.0  14
## 7_13m61 7_13 61     CC6  PL   M   A   SCR   17.0  18
## 7_14m61 7_14 61     CC5  PL   M   A   SCR   19.0  14
## 7_14m64 7_14 64      B4 PMG   M   J   SCR   13.0  16
## 7_14m69 7_14 69     H20  PL   M  SA   ABD   14.0  12
## 7_13m69 7_13 69     H20  PL   M  SA   SCR   14.5  12
## 7_14m71 7_14 71     D20  PL   F   J    NT   12.0  14
## 7_14m74 7_14 74     N17 PMG   F   J    NT    7.0  14
## 7_14m77 7_14 77     F17 PMG   M   J   ABD    9.5  15
## 7_14m79 7_14 79     J20 PMG   F   J    NT    9.0  12
## 7_14m80 7_14 80      N1  PL   M   J   SCR   13.0  15
```
* The `Station` column indicates where the mice were sampled. Where were the most mice captured? 
* How many mice were captured there?

```r
summary(metadata$Station)
```

```
##  A12  A13   A2   A3 AA10 AA13 AA18 AA20  AA6  B16  B18  B19   B2   B3   B4 
##    2    1    1    1    1    2    1    1    1    2    3    1    2    1    1 
##   B6   B8 BB18 CC13  CC2  CC3  CC4  CC5  CC6  D13  D17  D20   D3   D7   D8 
##    1    1    1    3    3    3    1    2    3    1    1    1    1    1    1 
##   E2   E3   F1  F17  F19   F2   F8  H18  H20   H4   H6  I11  I12   I6   J1 
##    1    1    1    1    1    1    1    1    3    1    1    1    1    1    1 
##  J10  J15  J16  J17  J20   J6  K19  L11  L15  L16  L18  L19  L20   L7  M16 
##    1    1    1    1    1    1    1    2    1    1    1    2    1    1    1 
##  M17  M18   M8   M9   N1  N16  N17  N19   N2  N20   N3   N4   P1  P11  P13 
##    1    1    1    1    1    1    1    2    1    4    1    2    1    2    1 
##  P15  P16  P17   P2   P5   P6   P7 
##    2    1    1    2    1    3    1
```
Answer: N20, 4 mice.


2.  Describe what each of the following commands does in a text block above the code, be specific. Put the code into the appropriate knitr code chunk. If something throws an error or looks weird, fix it.

count from 1 to 100 by 3's.
```
seq(1,100,3)
```
repeat vector containing a b, 10 times.
```
rep(c("a","b"),10)
```
give 10 numbers from 0 to 1 (from the uniform dist.) and put them in order
```
r <- runif(10); order(r)
```
Maybe this should be %*% instead of %? This is for matrix multiplication, so multiplying matrix with 100 by matrix with 3. 
```
100 %*% 3
```
Weight needs to have a capital W for the variable name. 
metadata[metadata$Weight==12 & metadata$SP=="PMG",]
```
metadata[metadata$weight==16 && metadata$SP=="PMG",]
```


3.	Calculate the mode for the weight of the mice in `wild.metadata.txt`
Answer: the weight is bimodal with 16 and 17 both occuring 12 times.

```r
#make variable containing a table with the weights as the lables and number of observations for each label in a vector.
weightfreq<- table(as.vector(metadata$Weight))
#check work
weightfreq
```

```
## 
##    7  7.5    9  9.5   10 10.5   11 11.5   12   13 13.5   14 14.5   15 15.5 
##    2    1    4    1    1    1    1    1    5    8    4    3    2   10    1 
##   16 16.5   17 17.5   18 18.5   19 19.5   20   21   22 22.5   23 23.5   24 
##   12    1   12    3   11    2    5    1    1    4    2    2    3    1    1 
##   25   26   27   30 
##    2    1    1    1
```

```r
#ask for the names with the maximum frequency in the weightfreq vector.
names (weightfreq) [weightfreq == max(weightfreq)]
```

```
## [1] "16" "17"
```

4.	Usign R commands, write the table to a new text file, but exclude the `Ear` and `Repro` columns.

```r
#make subset table without Ear and Repro
smallermetadata<- subset(metadata,select= c(-Ear, - Repro))
#check work
smallermetadata
```

```
##         Date ET Station  SP Sex Age Weight
## 5_25m3  5_25  3    BB18  PL   M   J    7.5
## 5_25m4  5_25  4     K19  PL   M   A   16.0
## 5_26m1  5_26  1     A12  PL   F   A   19.5
## 5_26m9  5_26  9      M9  PL   F   A   25.0
## 5_31m11 5_31 11      F2 PMG   F   J   16.0
## 5_31m2  5_31  2     CC4  PL   M  SA   15.0
## 5_31m4  5_31  4     L18  PL   M   A   18.0
## 5_31m9  5_31  9      L7  PL   F   A   30.0
## 6_14m1  6_14  1    AA13  PL   F   A   22.0
## 6_14m23 6_14 20    AA18  PL   M   A   17.0
## 6_15m11 6_15 11      E2 PMG   F   A   22.5
## 6_15m16 6_15 16     L11 PMG   M   A   16.0
## 6_15m20 6_15 20     M16  PL   M   A   17.0
## 6_15m24 6_15 24     M18 PMG   F  SA   18.0
## 6_15m27 6_15 27     J10  PL   M  SA   12.0
## 6_15m28 6_15 28     CC5  PL   M   A   17.5
## 6_15m2  6_15  2      B2  PL   M   A   17.0
## 6_15m32 6_15 32      D8  PL   M   J   14.5
## 6_15m33 6_15 33      A2 PMG   M   A   18.0
## 6_15m9  6_15  9      M8  PL   F   A   26.0
## 6_16m18 6_16 18     A13  PL   M  SA   11.5
## 6_16m32 6_16 32      I6  PL   M   J   13.5
## 6_16m33 6_16 33      B2 PMG   M   A   18.0
## 6_16m36 6_16 36     B19  PL   M   A   25.0
## 6_16m37 6_16 37     A12  PL   M   J    7.0
## 6_16m38 6_16 38     CC3 PMG   F   J   17.0
## 6_17m2  6_17  2      E3  PL   M   A   18.0
## 6_17m32 6_17 32      J6  PL   M  SA   13.0
## 6_17m7  6_17  7     I12 PMG   F   A   21.0
## 6_1m10   6_1 10     B18  PL   F   J   15.0
## 6_1m12   6_1 12     H18 PMG   M   A   16.0
## 6_1m2    6_1  2      D3  PL   M  SA   16.0
## 6_29m24 6_29 24     N20 PMG   F  SA   17.0
## 6_29m25 6_29 25     P15 PMG   F   A   23.0
## 6_29m34 6_29 34      P5 PMG   M  SA   15.0
## 6_29m38 6_29 38     CC2 PMG   F   A   18.0
## 6_29m48 6_29 48      P7  PL   F   J    9.0
## 6_29m7  6_29  7      F8 PMG   F   A   23.0
## 6_29m9  6_29  9      P6  PL   F   A   27.0
## 6_2m10   6_2 10     D17  PL   F   J   16.5
## 6_2m12   6_2 12     F19 PMG   M   A   18.0
## 6_2m14   6_2 14      B6  PL   M   J   12.0
## 6_2m15   6_2 15     N19 PMG   F   J   13.0
## 6_30m24 6_30 24     N20 PMG   F   A   17.0
## 6_30m2  6_30  2      B3  PL   M   A   19.0
## 6_30m33 6_30 33      F1 PMG   M   A   19.0
## 6_30m34 6_30 34      P6 PMG   M  SA   15.0
## 6_30m43 6_30 43    CC13 PMG   F   J   16.0
## 6_30m44 6_30 44     J16  PL   M  SA   17.0
## 6_5m13   6_5 13      N2 PMG   F   J   18.0
## 6_5m16   6_5 16     H20 PMG   M   A   16.0
## 6_5m19   6_5 19     L11 PMG   M   J   13.0
## 6_5m21   6_5 21     D13 PMG   F   J   10.5
## 6_5m7    6_5  7     I11 PMG   F  SA   22.0
## 7_13m1  7_13  1    AA13  PL   F   A   23.5
## 7_13m25 7_13 25     P15 PMG   F   A   18.5
## 7_13m34 7_13 34      D7 PMG   F  SA   15.0
## 7_13m37 7_13 37     AA6  PL   F   A   15.0
## 7_13m38 7_13 38     CC2 PMG   F   A   22.5
## 7_13m46 7_13 46      N4 PMG   F   A   21.0
## 7_13m51 7_13 51     B16 PMG   F   J   14.0
## 7_13m54 7_13 54      N3  PL   F  SA   13.0
## 7_13m55 7_13 55     J15  PL   F  SA   14.0
## 7_13m57 7_13 57     L20  PL   F  SA   15.5
## 7_13m61 7_13 61     CC6  PL   M   A   17.0
## 7_13m69 7_13 69     H20  PL   M  SA   14.5
## 7_14m1  7_14  1    CC13  PL   F   A   21.0
## 7_14m2  7_14  2     CC6  PL   M   A   18.5
## 7_14m21 7_14 21    AA10 PMG   F   A   17.5
## 7_14m24 7_14 24     N19 PMG   F   A   24.0
## 7_14m25 7_14 25     P16 PMG   F  SA   18.0
## 7_14m33 7_14 33      P2 PMG   M   A   20.0
## 7_14m34 7_14 34      H6 PMG   M   A   17.5
## 7_14m35 7_14 35      J1 PMG   F   A   23.0
## 7_14m38 7_14 38     CC2 PMG   F   A   21.0
## 7_14m51 7_14 51     B16 PMG   F  SA   13.5
## 7_14m54 7_14 54      P1  PL   F   J   13.5
## 7_14m55 7_14 55     L15  PL   F  SA   13.5
## 7_14m56 7_14 56     N20  PL   M   A   18.0
## 7_14m57 7_14 57     L19  PL   F  SA   15.0
## 7_14m59 7_14 59     CC3 PMG   M  SA   16.0
## 7_14m61 7_14 61     CC5  PL   M   A   19.0
## 7_14m64 7_14 64      B4 PMG   M   J   13.0
## 7_14m69 7_14 69     H20  PL   M  SA   14.0
## 7_14m71 7_14 71     D20  PL   F   J   12.0
## 7_14m74 7_14 74     N17 PMG   F   J    7.0
## 7_14m77 7_14 77     F17 PMG   M   J    9.5
## 7_14m79 7_14 79     J20 PMG   F   J    9.0
## 7_14m80 7_14 80      N1  PL   M   J   13.0
## 7_2m21   7_2 21      B8 PMG   F   A   19.0
## 7_2m25   7_2 25     P17 PMG   F   A   16.0
## 7_2m27   7_2 27     P11  PL   M  SA   15.0
## 7_2m38   7_2 38    AA20 PMG   F   A   17.0
## 7_2m46   7_2 46      P2 PMG   F  SA   15.0
## 7_2m51   7_2 51     B18 PMG   F   J   12.0
## 7_2m52   7_2 52     L16 PMG   M   A   18.0
## 7_2m53   7_2 53     J17  PL   M  SA   17.0
## 7_2m54   7_2 54      H4  PL   F   J    9.0
## 7_2m55   7_2 55     P13  PL   F   J   10.0
## 7_2m56   7_2 56      N4  PL   M   A   16.0
## 7_2m57   7_2 57     N20  PL   F   J   12.0
## 7_3m2    7_3  2      A3  PL   M   A   19.0
## 7_3m20   7_3 20     M17  PL   M   A   17.0
## 7_3m34   7_3 34      P6 PMG   M  SA   15.0
## 7_3m37   7_3 37     CC6  PL   F  SA   13.0
## 7_3m38   7_3 38     CC3 PMG   F  SA   17.0
## 7_3m43   7_3 43    CC13 PMG   F  SA   16.0
## 7_3m44   7_3 44     N16  PL   M  SA   16.0
## 7_3m51   7_3 51     B18 PMG   F   J   11.0
## 7_3m57   7_3 57     L19  PL   F   J   13.0
## 7_3m60   7_3 60     P11  PL   M   J    9.0
```

```r
#write table to text file
write.table(smallermetadata,"smallermetadata.txt")
```

