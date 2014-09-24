# Assignment 2
Amanda Elmore  
September 23, 2014  

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
nsamples <- nrow(metadata)
```

**Answer:** There are 111 samples in the `wild.metadata.txt` file.
  
  
  * How many columns are in the table? What are their names?


```r
nvariables <- ncol(metadata) #get number of columns
colnames <- colnames(metadata) #get column names
```

**Answer:** There are 9 columns in the file and their names are Date, ET, Station, SP, Sex, Age, Repro, Weight, Ear.
  
  * How many mice weighed 15 or more grams?

```r
big_samples <- subset(metadata, Weight>=15) #parse data frame to include only heavy samples
big_nsamples <- nrow(big_samples) #count number of samples over 15
big_samples$ET <- factor(big_samples$ET) #make ET a factor 
big_mice <- length(unique(big_samples$ET)) #count the number of unique mice over 15 grams
```

**Answer:** There are 31 unique mice over 77 samples that weight 15 or more grams.
  
  * What is the median weight for the mice sampled?

```r
median_weight <- median(metadata$Weight)
```

**Answer:** The median weight of all samples is 16.
  
  * How many PMG mice were there?

```r
PMG_mice <- subset(metadata, metadata$SP=='PMG') #parse data frame to include only PMG mice
PMG_num <- length(unique(PMG_mice$ET))
```

**Answer:** There are 23 PMG mice.
  
  * How many female PL mice were there?

```r
female_PL <- subset(metadata, metadata$Sex=='F' & metadata$SP=='PL')  #parse data table to be only female PL mice
femalePL_unique <- length(unique(female_PL$ET)) #have to do this to avoid repeat samples from same mouse
```

**Answer:** The number of female PL mice in the dataset is 9.

  * Alphabetize `wild.metadata.txt` by the ear tag number (only show the first 5 rows of the table)
  

```r
sortedET <- metadata[order(metadata$ET),] #sort and save dataframe to new varible
sortedET[1:5,]
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
sorted_weight <- metadata[order(metadata$ET, metadata$Weight),] #the animals are sorted and each animal is sorted by weight
sorted_weight[1:5,]
```

```
##        Date ET Station SP Sex Age Repro Weight Ear
## 5_26m1 5_26  1     A12 PL   F   A    NE   19.5  14
## 7_14m1 7_14  1    CC13 PL   F   A    NE   21.0  15
## 6_14m1 6_14  1    AA13 PL   F   A    NE   22.0  14
## 7_13m1 7_13  1    AA13 PL   F   A    NE   23.5  14
## 5_31m2 5_31  2     CC4 PL   M  SA   ABD   15.0  14
```

  * The `Station` column indicates where the mice were sampled. Where were the most mice captured? How many mice were captured there?

```r
counts <- summary(metadata$Station)
sortedcounts<- sort(counts, decreasing=T)
max_number <- sortedcounts[1]
max_name <- names(sortedcounts[1])
```
  
**Answer:** The most mice were captured at N20 Station and there were 4 mice captured there.

2.	Describe what each of the following commands does in a text block above the code, be specific. Put the code into the appropriate knitr code chunk. If something throws an error or looks weird, fix it.


Vector with every third number from 1 to 100 
```
seq(1,100,3)

```

Vector with repeating letters a and b 10 times, alternating.
```
rep(c("a","b"),10)
```

r is a vector of 10 numbers from 0 to 1 following a uniform distribution. order(r) will sort the numbers and print the index values of the sorted numbers.
```
r <- runif(10); order(r)
```

A single % sign can't be used for mathematical operations in R. Possibly you meant to use %% which is the modulus operator. 100 %% 3 will output the remainder of 3 into 100, which is 1.
```
100 %% 3
```

This statement will print a parsed data frame 'metadata' to include only observations in which the weight is exactly 16 and the SP is PMG. There is a typo - weight should be capitalized. Also, the && boolean operator is meant for vectors and will not evaluate this data frame correctly. Use a single &.
```
metadata[metadata$Weight==16 & metadata$SP=="PMG",]
```


3.	Calculate the mode for the weight of the mice in `wild.metadata.txt`

```r
metadata$Weight<- factor(metadata$Weight)
counts <- summary(metadata$Weight)
maximum <- max(counts)
mode <- names(counts[maximum])
```
**Answer:** The mode for the weight of mice is 14 grams.

4.	Usign R commands, write the table to a new text file, but exclude the `Ear` and `Repro` columns.

