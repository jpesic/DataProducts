---
title: "Week 3 Project"
author: "jpesic"
date: "February 14, 2018"
output:
 # slidy_presentation: default
  ioslides_presentation: default
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = FALSE)
```


```{r plot, echo=FALSE, warning=FALSE,message=FALSE}
suppressPackageStartupMessages({library(plotly)})
require(readr)
require(lubridate)
transactions <- read_csv("transactions.csv")
transactions$Date<-mdy(transactions$Date)
transactions$Date_Day<-wday((transactions$Date), label=TRUE)
transactions$Date_Month<-month((transactions$Date), label=TRUE)

```
## Amazon Spending since 2010


```{r plot_1, echo=FALSE, message=FALSE, warning=FALSE}
transactions<-transactions[order(transactions$Date, decreasing = FALSE),]
transactions$Cum_Amount<-cumsum(transactions$Amount)
p1<-plot_ly (transactions, x =~Date, y = ~Cum_Amount, type='scatter', color = ~Date_Day)
p1

```

## Amazon Spending since 2010 (cont)


```{r plot_2, echo=FALSE, message=FALSE, warning=FALSE}
p3<-plot_ly (transactions, x =~year(Date), y = ~Date_Month, type='scatter', size=~Amount, color = ~Date_Day)
p3

```


