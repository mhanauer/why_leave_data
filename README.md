---
  title: "Why leave Descriptives"
output: html_document
---
Load in data
```{r}
setwd("S:/Indiana Research & Evaluation/Matthew Hanauer/why_leave_project")
why_leave_data = read.csv("why_leave_data.csv", header = TRUE)
```
Grab first and last column
Then lower case last variable
Then seperate by comma
Then figure out how to count them (grab n's from different columns)
```{r}

describe.factor(why_leave_data$State)
why_leave_dat = why_leave_data[,c(3,5)]
why_leave_dat
why_leave_dat = t(data.frame(describe.factor(why_leave_dat$Overall.theme)))
themes = rownames(why_leave_dat) 
why_leave_dat = data.frame(why_leave_dat)
why_leave_dat$themes = themes
rownames(why_leave_dat) = NULL
why_leave_dat
### Poor management row 1, 16, 18, 19, 20 
poor_management = why_leave_dat[c(1,16,18,19, 20),]
poor_management_des = round(apply(poor_management[,1:2], 2, sum),2)
poor_management_des
### 2, 3,8, 10, 11,14
outside_centerstone = why_leave_dat[c(2, 3,8, 10, 11,14),]
outside_centerstone_des = round(apply(outside_centerstone[,1:2], 2, sum),2)
### Lack of pay 5, 6, 12:19
lack_pay = why_leave_dat[c(5, 6, 12:17, 19),]
lack_pay_des = round(apply(lack_pay[,1:2], 2, sum),2)
lack_pay_des

### Opportunities for advancement 7, 11,12, 17
opp_advance = why_leave_dat[c(6, 11,12,18),]
opp_advance_des = round(apply(opp_advance[,1:2], 2, sum),2)
opp_advance_des

theme_results = data.frame(poor_management_des, outside_centerstone_des , lack_pay_des, opp_advance_des)
theme_results = t(theme_results)
themes = rownames(theme_results)
theme_results = data.frame(themes, theme_results)
theme_results
write.csv(theme_results, "theme_results.csv", row.names = FALSE)
```



