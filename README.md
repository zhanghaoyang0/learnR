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
table(df[,2])/nrow(df) # nrow is the total number of rows in the dataframe
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
mean(score) # ncol is the total number of columns in the dataframe
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
## Target
1. Test if the score in male and female is different.
2. Test if the education level (4th col) in male and female is different.
3. Use for loop to measure the distribution of variable in 2-10 column (i.e., sex to drink or not), one by one.

## Reference answer
### Read data, rename columns, make score to numeric:
```  
library(dplyr)
library(readxl)
df = read_excel("冠心病患者运动康复依从性及影响因素调查问卷.xlsx")
df = df%>%rename(edu='3、文化程度', sex='1、您的性别：', score='总分')
df = df%>%mutate(score=as.numeric(score))
``` 
### Test if the score in male and female is different:
```  
t.test(df[df$sex=='男', 'score'], df[df$sex=='女', 'score'])
# t = -1.1689, df = 112.99, p-value = 0.2449
``` 
### Test if the education level (4th col) in male and female is different:
```  
tab = table(df$sex, df$edu)
tab 
chisq.test(tab)
# X-squared = 3.2186, df = 4, p-value = 0.5219
``` 
### Distribution of variable in 2-10 column:
```  
for (i in names(df)[2:10]){
    print(table(df[,i]))
}
# 女 男 
# 65 50 
# ＜50   ≧80 50-59 60-79 
#   48     3    38    26 
# 其他       初中       大学       小学 高中及中专 
#  2         39         16         23         35 
# ...
``` 

# Homework 3 (20221223)
## Target
1. Measure the association between score (67th col), and sex (2nd col) to "53、当一个人心脏有问题时，他/她应该避免进行体力活动/锻炼"(66th col), one by one, with regression.  
For example, in your first regression, your y is score, your x is sex. In your second regression, your y is score, your x is age... 
2. Measure the association between "12、是否接受冠心病相关的健康教育" (13th col), and sex (2nd col) to "53、当一个人心脏有问题时，他/她应该避免进行体力活动/锻炼"(66th col), one by one, with regression. Note that you should use logistic regression for binary outcome.
3. Go through this [*paper*](https://pubmed.ncbi.nlm.nih.gov/29201888/)



