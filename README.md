# About learnR
Let's learn R step by step, it is easy!

# Requirements
- `R`
- `Rstudio`
 
# Data 
`冠心病患者运动康复依从性及影响因素调查问卷` contributed by Fan Yang, thanks~

# Homework 1 (20221123)
## Target
1. Read that data
2. Measure the proprotion of second column (i.e., sex)
3. Measure the mean and sd of last column (i.e., score)  

## Reference answer
### Read that data:
```  
library(readxl)
file='this/is/your/path/of/the/file/冠心病患者运动康复依从性及影响因素调查问卷'
df = read_excel(file)
``` 
### Measure the proprotion of second column (i.e., sex):  
``` 
table(df[,2])
table(df[,2])/nrow(df) # nrow is the total number of column in the dataframe
```
You will see:  
```
女 男 
65 50 
       女        男 
0.5652174 0.4347826 
```
### Measure the mean and sd of last column (i.e., score):  
```
score = df[,ncol(df)]
mean(score) # ncol is the total number of column in the dataframe
```
You will see:  
```
[1] NA
Warning message:
In mean.default(score) : argument is not numeric or logical: returning NA
```
Why? Because the `score` is character, we should convert it to numberic:
```
score = as.numeric(score)
mean(score)
sd(score)
```
You will see:  
```
> mean(score)
[1] 175.1043
> sd(score)
[1] 17.5186
```
Want a better looking? Try this:
```
paste0(round(mean(score), 1), '±', round(sd(score), 1))
[1] "175.1±17.5"
```

# Homework 2 (20221128)
Prepare for your examination first, then you may go this homework:
1. Test if the score in male and female is different.
2. Test if the education level (4th col) in male and female is different.

