# Assignment 2
Isaiah Song  
September 26, 2014  

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
numSamples<-nrow(metadata) #Number of rows
```

There are as many samples as there are rows, equaling 111.
  
  * How many columns are in the table? What are their names?
  

```r
numColumns<-ncol(metadata) #Number of columns
namColumns<-colnames(metadata) #Names of columns
```

There are 9 columns and their names are: Date, ET, Station, SP, Sex, Age, Repro, Weight, Ear.

  * How many samples came from mice that weighed 15 or more grams?
  

```r
wtGr15<-metadata[metadata$Weight>=15,] #Output of samples weighing 15 grams or greater
samGr15<-nrow(wtGr15) #Number of rows
```

The number of samples that came from mice that weighed 15 or more grams is 77.
  
  * What is the median weight of the samples?
  

```r
medWt<-median(metadata$Weight) #Median of sample weights
```

The median weight is 16.

  * How many PMG samples were there?
  

```r
PMG<-metadata[metadata$SP=="PMG",] #Output of samples of PMG
numPMG<-nrow(PMG) #Number of rows
```

There were 53 PMG samples.

  * How many female PL samples were there?
  

```r
PL_F<-metadata[metadata$SP=="PL"&metadata$Sex=="F",] #Output of samples of female PL
numPL_F<-nrow(PL_F) #Number of rows
```

There were 24 female PL samples.

  * Alphabetize `wild.metadata.txt` by the ear tag number (only show the first 5 rows of the table) 
  

```r
metadata.sortET<-metadata[order(metadata$ET),] #Sort by ET order
metadata.sortET[1:5,] #Display first 5 rows
```

```
##        Date ET Station SP Sex Age Repro Weight Ear
## 5_26m1 5_26  1     A12 PL   F   A    NE   19.5  14
## 6_14m1 6_14  1    AA13 PL   F   A    NE   22.0  14
## 7_13m1 7_13  1    AA13 PL   F   A    NE   23.5  14
## 7_14m1 7_14  1    CC13 PL   F   A    NE   21.0  15
## 5_31m2 5_31  2     CC4 PL   M  SA   ABD   15.0  14
```

  * Sort the table by the weight of the mice that each sample came from  
  

```r
metadata.sortWt<-metadata[order(metadata$Weight),] #Sort by weight
metadata.sortWt[1:5,] #Display first 5 rows
```

```
##         Date ET Station  SP Sex Age Repro Weight Ear
## 6_16m37 6_16 37     A12  PL   M   J     A    7.0  12
## 7_14m74 7_14 74     N17 PMG   F   J    NT    7.0  14
## 5_25m3  5_25  3    BB18  PL   M   J   ABD    7.5  13
## 6_29m48 6_29 48      P7  PL   F   J    NT    9.0  11
## 7_14m79 7_14 79     J20 PMG   F   J    NT    9.0  12
```

  * The `Station` column indicates where the mice were sampled. Where were the most mice captured? 
  

```r
summStation<-summary(metadata$Station) #Show number of mice sampled in each station
maxStation<-names(summStation[summStation==max(summStation)]) #Get name of station with largest number of mice sampled
```

The most mice were captured in N20.

  * How many mice were captured there?


```r
sortStation<-sort(summStation, decreasing=TRUE) #Sort by decreasing number of mice sampled
capMice<-as.integer(sortStation[1]) #Output first entry (station of highest number of mice sampled) as integer
```

There were 4 mice captured at N20.

2.	Describe what each of the following commands does in a text block above the code, be specific. Put the code into the appropriate knitr code chunk. If something throws an error or looks weird, fix it.


Gives a sequence of numbers from 1 to 100 rising in increments of 3.
```
seq(1,100,3)
```

Repeats a vector sequence ("a" and "b") a total of 10 times
```
rep(c("a","b"),10)
```

Gives a series of 10 numbers in uniform distribution from 0 to 1 and sorts them in order
```
r <- runif(10); order(r)
```

This code gives an error; may possibly be fixed by changing to "100 %% 3", which gives the remainder when dividing the first number by the second number
```
100 % 3
```

Outputs samples in the metadata that correspond to a weight of 16 and SP value of "PMG";  Also, "weight" must be capitalized as that is how the variable is assigned and && must be changed to &
```
metadata[metadata$weight==16 && metadata$SP=="PMG",]
```


3.	Calculate the mode for the weights in `wild.metadata.txt`


```r
tabWeight<-table(metadata$Weight) #Convert into a table
modeWt<-names(tabWeight[tabWeight==max(tabWeight)]) #Get the weights that have the highest number of occurrences
```

The mode for the weights is 16, 17

4.	Usign R commands, write the table to a new text file, but exclude the `Ear` and `Repro` columns.


```r
newmetadata<-metadata[,-7] #Excludes column 7 ("Repro")
newmetadata2<-newmetadata[,-8] #Excludes column 8 of new metadata ("Ear")
write.table(newmetadata2, "C:/Users/Isaiah/Desktop/new.wild.metadata.txt") #Writes newmetadata2 to text file on desktop
```
