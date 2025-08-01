# WUP_linearmodel
---
title: "WUP_Linearmodel"
name: "Jennifer Espinoza"
date: "Summer 2025"
output: html_document
---

```{r include=FALSE,echo=FALSE}
require(knitr)
require(tidyverse)
require(tigerstats)
Data <- read.csv(file="https://onlinestatbook.com/case_studies_rvls/physical_strength/data.txt", sep="", header=TRUE)
```

```{r}
simp <- lm(SIMS~ARM,data=Data)
plot(SIMS~ARM,data=Data)
abline(simp)
summary.lm(simp)
```

```{r}
target<-data.frame(ARM=88, GRIP=94)
```

```{r}
predict(simp,target,interval=c("prediction"))
```

```{r}
newGRIP <- lm(SIMS~GRIP,data=Data)
plot(SIMS~GRIP,data=Data)
abline(newGRIP)
summary.lm(newGRIP)
```
```{r}
predict(newGRIP,target,interval=c("prediction"))
```

```{r}
ARMGRIP_2 <- lm(SIMS~ARM + GRIP,data=Data)
summary.lm(ARMGRIP_2)
```

```{r}
predict(ARMGRIP_2,target,interval=c("prediction"))
```

Now we are going to compare models simp and newGrip using the anova command.

```{r}
anova(simp,ARMGRIP_2)
```

This test is telling us that their is an error that occurs from the with just ARM and it added up to 217.88. The errors in the model with both ARM and GRIP added up to 188.43 showing that there is less errors in the model with both elements rather then the one with just ARM.

```{r}
anova(newGRIP,ARMGRIP_2)
```

What this shows is that the sum of errors for the model with just GRIP adds up to 243.07. The sum of errors for the model of both ARM and GRIP adds up 188.43. The difference is greater than before being that it is a 54.64 difference.

```{r}
anova(newGRIP,simp)
```

While we do not get a p-value from anova since the models aren't nesting, we see that model for ARM has a smaller sum of errors than the model for GRIP.
