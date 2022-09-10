---
title: "Confirmatory Factor Analysis for Pain Scales"
author: "Usman Rashid"
date: "05/10/2019"
output:
  md_document:
    variant: gfm
    toc: yes
    toc_depth: '4'
  pdf_document:
    toc: true
    toc_depth: 4
    number_sections: true
bibliography: bibliography.bib
csl: apa.csl
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
rm(list = ls())

# function for is nan
is.nan.data.frame <- function(x)
  do.call(cbind, lapply(x, is.nan))
```

```{r data_setup, echo=FALSE, include=FALSE}

# Packages Used:
require(ggplot2)
require(lme4)
require(car)
require(MASS)
require(sjstats)
require(fBasics)
require(ggpubr)
require(reshape2)
require(phia)
require(emmeans)
require(multcomp)
require(jtools)
require(rsq)
require(r2glmm)
require(sjPlot)
require(MuMIn)
require(effects)
require(optimx)
require(margins)
require(cAIC4)
require(ggsignif)
require(dplyr)
require(forcats)
require(splines)
require(ggsci)
require(corrplot)
require(lavaan)
require(lemon)
#require(semTools)

knit_print.data.frame <- lemon_print

def.chunk.hook  <- knitr::knit_hooks$get("chunk")
knitr::knit_hooks$set(chunk = function(x, options) {
  x <- def.chunk.hook(x, options)
  ifelse(options$size != "normalsize", paste0("\\", options$size,"\n\n", x, "\n\n \\normalsize"), x)
})

# Load data
dataSource <- read.csv("DataTable.csv")
dataSource[is.nan(dataSource)] <- NA
# Country names
dataSource$country <- factor(dataSource$country, levels = c(0, 1), labels = c("Mongolia", "New Zealand"))


dataSourcePCS <- dataSource[, c("country", "name", "nameid",
                                "PCS1", "PCS2", "PCS3", "PCS4", "PCS5",
                                "PCS6", "PCS7",
                                "PCS8", "PCS9", "PCS10", "PCS11",
                                "PCS12", "PCS13")]

dataSourcePCS$partId <- seq(1, 301)
dataSourcePCS$name <- NULL
dataSourcePCS$nameid <- NULL

dataSourcePCS <- dataSourcePCS[, c(15, seq(1,14))]

dataSourcePCS$country <- fct_relevel(dataSourcePCS$country, "New Zealand", "Mongolia")

dataSourcePCS$partId <- as.factor(dataSourcePCS$partId)

dataSourceDASS <- dataSource[, c("country", "name", "nameid",
                                "DASS1", "DASS2", "DASS3", "DASS4", "DASS5",
                                "DASS6", "DASS7", "DASS8", "DASS9", "DASS10",
                                "DASS11", "DASS12", "DASS13", "DASS14", "DASS15",
                                "DASS16", "DASS17", "DASS18", "DASS19", "DASS20",
                                "DASS21")]

dataSourceDASS$partId <- seq(1, 301)
dataSourceDASS$name <- NULL
dataSourceDASS$nameid <- NULL

dataSourceDASS <- dataSourceDASS[, c(23, seq(1,22))]

dataSourceDASS$country <- fct_relevel(dataSourceDASS$country, "NZ", "Mongolia")

dataSourceDASS$partId <- as.factor(dataSourceDASS$partId)

dataSourceDASS.long     <- melt(dataSourceDASS, id = c("country", "partId"), 
                         variable.name = "Question", value.name = "Response")
dataSourceDASS.long$Response <- as.factor(dataSourceDASS.long$Response)
dataSourceDASS.long$Response <- fct_explicit_na(dataSourceDASS.long$Response, na_level = "Missing")

#PBI data
dataSourceBPI <- dataSource[, c("country", "name", "nameid",
                                "worst", "least", "average", "now",
                                "activity", "mood",
                                "walking", "work", "relations", "sleep",
                                "enjoyment")]
dataSourceBPI$partId <- seq(1, 301)
dataSourceBPI$name <- NULL
dataSourceBPI$nameid <- NULL

dataSourceBPI <- dataSourceBPI[, c(13, seq(1,12))]

dataSourceBPI$country <- fct_relevel(dataSourceBPI$country, "New Zealand", "Mongolia")

dataSourceBPI$partId <- as.factor(dataSourceBPI$partId)

dataSourceBPI[dataSourceBPI == 999] = NA
```
\newpage
# Statistical Analysis
The aim of this analysis is to evaluate measurement invariance in the Brief Pain Inventory scale (BPI),  Depression, Anxiety, Stress Scale (DASS-21) and Pain Catastrophizing Scale (PCS) across two nationalities (New Zealand, Mongolia). Measurement invariance is assessed at two sequential levels: configural and metric [@van2012checklist]. Configural invariance is assumed if the same model structure is successfully fitted across the nationalities. If the same model structure can not be fitted successfully across the two nationalities, the model structure is fitted in each nationality separately to test whether the proposed theoretical structure can be confirmed in each nationality or not? Metric invariance is assumed if the same model structure with same factor loadings is successfully fitted across the nationalities. Metric invariance is interpreted to imply same meaning across nationalities for the latent constructs.
\par
All the models are fitted using the maximum likelihood method in R (R Foundation for Statistical Computing, Vienna, Austria) version 3.5.1 [@forR] using package lavaan version 0.6-4 [@forLavaan]. A model's goodness-of-the-fit is evaluated with comparative fit index (CFI) and root mean square error of approximation (RMSEA). For CFI, values greater than 0.9 and 0.95 are interpreted as adequate and good fit [@van2012checklist]. For RMSEA, values less than 0.08 and 0.05 are interpreted as adequate and good fit [@van2012checklist]. However, these cut-offs are only treated as indicative of good fit and not as golden rules [@lai2016problem]. Each level of invariance is evaluated with a Chi-squared test for the null hypothesis that the less constrained model does not fit the data better than the more constrained model. For example, to evaluate metric invariance, the fit of the model with same structure across nationalities is compared to the fit of the model with same structure and factor loadings across nationalities. In this comparison, configural model is less constrained as it has more free parameters. The model with same structure and factor loadings across the groups is more constrained as it has less number of free parameters due to the fact that the factor loadings are held constant across nationalities. Statistical significance is assumed below 0.05.

## Model Structure

### Brief Pain Inventory
The model structure fitted to the data is given below in \emph{lavaan} formula syntax [@forLavaan] and is adopted from the past work of @cleeland1988multidimensional on BPI.
```{r mdl_struct_pbi, echo=TRUE}
structureBPI <-'Intensity        =~ worst + least + average + now
                Interference     =~ activity + mood + walking + work + relations + sleep + enjoyment'
```

### Depression, Anxiety, Stress Scale
The model structure stated below for DASS is based on the work of @norton2007depression.
```{r mdl_struct_dass, echo=TRUE}
structureDASS <-'Depression      =~ DASS3 + DASS5 + DASS10 + DASS13 + DASS16 + DASS17 + DASS21
                 Anxiety         =~ DASS2 + DASS4 + DASS7  + DASS9  + DASS15 + DASS19 + DASS20
                 Stress          =~ DASS1 + DASS6 + DASS8  + DASS11 + DASS12 + DASS14 + DASS18'
```

### Pain Catastrophizing Scale
Following model structure for PCS is based on the work of @joyce2004testing.
```{r mdl_struct_pcs, echo=TRUE}
structurePCS <- 'Rumination      =~ PCS8 + PCS9 + PCS10 + PCS11
                 Magnification   =~ PCS6 + PCS7 + PCS13
                 Helplessness    =~ PCS1 + PCS2 + PCS3 + PCS4 + PCS5 + PCS12
                 Catastrophizing =~ Rumination + Magnification + Helplessness'
```

\newpage

## Evaluation of Measurement Invariance across Nationalities
### Brief Pain Inventory
#### Configural Invariance
```{r cfa_fit_config_pop_bpi, echo=TRUE}
cfaFit.CI <- cfa(model = structureBPI, data = dataSourceBPI, group = "country")
```

```{r mdl_summary_bpi, echo=FALSE, eval=TRUE, include=FALSE}
cfaFit.CI.BPI <- cfaFit.CI
a<-summary(cfaFit.CI, fit.measures = TRUE, standardize = TRUE, rsquare = TRUE)
params<-a$fit
```

#### Model Fit Estimates for Configural Invariance
CFI = 0.879 and RMSEA = 0.142 90% CI [0.126, 0.158] both suggest a poor model fit.

```{r mdl_summary_print_bpi, echo=FALSE}
param_name <- c("CFI", "RMSEA [90% CI]")
ci <- paste(as.character(round(as.numeric(params['rmsea']), 3)), " [", as.character(round(as.numeric(params['rmsea.ci.lower']), 3)), " ", as.character(round(as.numeric(params['rmsea.ci.upper']), 3)), "]", sep="")
param_values <- c(as.character(round(as.numeric(params['cfi']), 3)), ci)

d <- data.frame(param_name, param_values)
names(d) <- c("Parameters", "Values")
```

```{r mdl_summary_print_bpi_nz_mn, echo=FALSE, eval=TRUE, include=FALSE}
cfaFit.CI.NZ <- cfa(model = structureBPI, data = subset(dataSourceBPI, country == "New Zealand"))
cfaFit.CI.Mn <- cfa(model = structureBPI, data = subset(dataSourceBPI, country == "Mongolia"))

a<-summary(cfaFit.CI.NZ, fit.measures = TRUE, standardize = TRUE, rsquare = TRUE)
params<-a$fit

param_name <- c("CFI", "RMSEA [90% CI]")
ci <- paste(as.character(round(as.numeric(params['rmsea']), 3)), " [", as.character(round(as.numeric(params['rmsea.ci.lower']), 3)), " ", as.character(round(as.numeric(params['rmsea.ci.upper']), 3)), "]", sep="")
param_values <- c(as.character(round(as.numeric(params['cfi']), 3)), ci)

d.nz <- data.frame(param_name, param_values)
names(d.nz) <- c("Parameters", "Values")

a<-summary(cfaFit.CI.Mn, fit.measures = TRUE, standardize = TRUE, rsquare = TRUE)
params<-a$fit

param_name <- c("CFI", "RMSEA [90% CI]")
ci <- paste(as.character(round(as.numeric(params['rmsea']), 3)), " [", as.character(round(as.numeric(params['rmsea.ci.lower']), 3)), " ", as.character(round(as.numeric(params['rmsea.ci.upper']), 3)), "]", sep="")
param_values <- c(as.character(round(as.numeric(params['cfi']), 3)), ci)

d.mn <- data.frame(param_name, param_values)
names(d.mn) <- c("Parameters", "Values")
```

```{r bpi_fits_print, echo=FALSE, render=lemon_print}
d.nz$Model <- "New Zealand"
d.mn$Model <- "Mongolia"
d$Model <- "Configural"

pd <- rbind(d.nz, d.mn, d)

pd <- pd[, c(3, 1, 2)]

head(pd, n = 10)
```

#### Test for Metric Invariance
The test statistics (Chi-squared difference [9] = 56.751, p < 0.0001) reject the null hypothesis that the configural model is not an improvement over the model with loadings constrained across nationalities. Thus, the two models which allow same or different factor loadings across the nationalities (New Zealand, Mongolia) result in different fits. This result implies that the factor loadings across the two nationalities are not same.
```{r test_me_invar_bpi, echo=TRUE}
cfaFit.MI <- cfa(model = structureBPI,
                 data = dataSourceBPI, group = "country",
                 group.equal = "loadings")
```

```{r test_me_invar_results_bpi, echo=FALSE, render=lemon_print}
anovaResults<-as.data.frame(anova(cfaFit.MI, cfaFit.CI))
anovaResults <- round(anovaResults, 4)

anovaResults[is.na(anovaResults)] <- ""
head(anovaResults)
```

#### Summary
The model with two factor configuration for BPI seems implausible in both New Zealand (CFI = 0.886 and RMSEA = 0.146 90% CI [0.123, 0.169]) and Mongolia (CFI = 0.870 and RMSEA = 0.138 90% CI [0.115, 0.161]). The model fit across the two nationalities is also poor (CFI = 0.879 and RMSEA = 0.142 90% CI [0.126, 0.158]). Moreover, there is evidence (Chi-squared difference [9] = 56.751, p < 0.0001) to suggest that these factors do not have same meaning across the two nationalities.

\newpage

### Depression, Anxiety, Stress Scale
#### Configural Invariance
```{r cfa_fit_config_pop_dass, echo=TRUE}
cfaFit.CI <- cfa(model = structureDASS, data = dataSourceDASS, group = "country")
```

##### Issue of Non-positive Definite Covariance Matrix
The covariance matrix estimated for Mongolia is not positive definite. Positive definite covariance matrix is a requirement for valid model estimation. The reasons underlying this problem are revealed with a comparative analysis of the estimated correlation matrices.

```{r cov_mat_model, echo=FALSE}
covMat <- lavInspect(cfaFit.CI, "cor.lv")

covMat.Mongolia <- as.data.frame(covMat$Mongolia)
covMat.NZ <- as.data.frame(covMat$`New Zealand`)
```

Estimated correlation matrix for Mongolia

```{r cov_mat_model_mongolia, echo=FALSE, render=lemon_print}
head(covMat.Mongolia)
```

Estimated correlation matrix for New Zealand

```{r cov_mat_model_nz, echo=FALSE, render=lemon_print}
head(covMat.NZ)
```

A comparison of the above two matrices reveal that the factors are highly correlated (> 0.9) in the model estimated for Mongolia. This result casts doubt on the hypothesis that the DASS scale is measuring three constructs, as specified in the model structure, in the case of Mongolia.

#### Model Fit for New Zealand
```{r cfa_fit_config_pop_dass_nz, echo=TRUE}
cfaFit.NZ <- cfa(model = structureDASS, data = subset(dataSourceDASS, country == "New Zealand"))
```

```{r mdl_summary_dass_nz, echo=FALSE, eval=TRUE, include=FALSE}
a<-summary(cfaFit.NZ, fit.measures = TRUE, standardize = TRUE, rsquare = TRUE)
params<-a$fit
```

CFI = 0.897 and RMSEA = 0.086 90% CI [0.073 0.098] both suggest a poor model fit, indicating absence of evidence for the three factor DASS structure in the case of New Zealand.

```{r mdl_summary_print_dass, echo=FALSE, render=lemon_print}
param_name <- c("CFI", "RMSEA [90% CI]")
ci <- paste(as.character(round(as.numeric(params['rmsea']), 3)), " [", as.character(round(as.numeric(params['rmsea.ci.lower']), 3)), " ", as.character(round(as.numeric(params['rmsea.ci.upper']), 3)), "]", sep="")
param_values <- c(as.character(round(as.numeric(params['cfi']), 3)), ci)

d <- data.frame(param_name, param_values)
names(d) <- c("Parameters", "Values")

head(d)
```

#### Summary
The model with three factor configuration for DASS appears unconvincing across the two nationalities. This assertion is supported by the fact that the model has failed to fit the data from Mongolia as the factors are highly correlated (r > 0.9) to each other. The model fit for New Zealand has also exhibited poor goodness-of-the-fit measures (CFI = 0.897 and RMSEA = 0.086 90% CI [0.073 0.098]). The metric invariance can not be tested as the same model structure did not fit the data from the two nationalities.

\newpage

### Pain Catastrophizing Scale
#### Configural Invariance
```{r cfa_fit_config_pop_pcs, echo=TRUE}
cfaFit.CI <- cfa(model = structurePCS, data = dataSourcePCS, group = "country")
```
##### Issue of Negative Variance Estimate
The variance estimated for magnification in the model for \emph{Mongolia} is negative (-0.046, SE 0.042). This indicates occurrence of a Heywood case [@chen2001improper]. This may be caused by a sampling fluctuation or misspecification of the model structure.
```{r neg_vars_pcs, echo=FALSE, include=FALSE}
a <- summary(cfaFit.CI)
```

```{r neg_vars_table_pcs, echo=FALSE, render=lemon_print}
a <- a$pe
a <- subset(a, op == "~~")

a <- a[, c(1, 5, 7, 8)]

a$Nationality <- factor(a$group, levels = c(1, 2), labels = c("NZ", "Mongolia"))

a$group <- NULL
a_m <- subset(a, Nationality == "Mongolia")
a_nz <- subset(a, Nationality == "NZ")

a_m$Nationality <- NULL
a_nz$Nationality <- NULL
a_nz$lhs <- NULL

names(a_m) <- c("Model Term", "Variance (Mongolia)", "SE (Mongolia)")
names(a_nz) <- c("Variance (NZ)", "SE (NZ)")

t <- cbind(a_m, a_nz)

t$`Variance (Mongolia)` <- round(t$`Variance (Mongolia)`, 3)
t$`SE (Mongolia)` <- round(t$`SE (Mongolia)`, 3)
t$`Variance (NZ)` <- round(t$`Variance (NZ)`, 3)
t$`SE (NZ)` <- round(t$`SE (NZ)`, 3)

rownames(t) <- NULL

head(t, n=20L, addrownums = FALSE)
```

To ascertain that it is not caused by a sampling fluctuation, a one-sided null hypothesis test for variance estimate equal to 0 is performed with the alternative hypothesis that the estimate is negative. The test is based on the z-score obtained as a ratio of the variance estimate and its standard error [@chen2001improper]. The test result (z = -1.095, p(<z) = 0.137) indicates that there is not enough evidence to reject the null that the estimate is 0. Thus, as suggested by @chen2001improper, the variance for magnification in the model for Mongolia is fixed at 0. Moreover, the variance estimate for magnification in the NZ model (0.001, SE 0.074, z=0.014, p(<z) = 0.505) is also set to 0 to fit the same model structure across the nationalities.

#### Configural Invariance (Magnification Variance=0)
```{r cfa_fit_config_pop_zero_var_pcs, echo=TRUE}
structurePCS <- 'Rumination      =~ PCS8 + PCS9 + PCS10 + PCS11
                 Magnification   =~ PCS6 + PCS7 + PCS13
                 Helplessness    =~ PCS1 + PCS2 + PCS3 + PCS4 + PCS5 + PCS12
                 Catastrophizing =~ Rumination + Magnification + Helplessness
                 Magnification   ~~ 0*Magnification'
cfaFit.CI <- cfa(model = structurePCS, data = dataSourcePCS, group = "country")
```

```{r mdl_summary_pcs, echo=FALSE, eval=TRUE, include=FALSE}
cfaFit.CI.PCS <- cfaFit.CI
a<-summary(cfaFit.CI, fit.measures = TRUE, standardize = TRUE, rsquare = TRUE)
a.super <- a
params<-a$fit
```

\newpage

#### Model Fit Estimates for Configural Invariance
CFI = 0.909 and RMSEA = 0.113 90% CI [0.1, 0.127] suggest a discrepancy between the model fit estimates as CFI > 0.9 indicates adequate fit and RMSEA > 0.08 indicates poor fit. As suggested by @lai2016problem, this does not necessarily imply a bad fit due to model misspecification. Thus, to further investigate the measurement invariance across nationalities, we perform tests for metric invariance.

```{r mdl_summary_print_pcs, echo=FALSE}
param_name <- c("CFI", "RMSEA [90% CI]")
ci <- paste(as.character(round(as.numeric(params['rmsea']), 3)), " [", as.character(round(as.numeric(params['rmsea.ci.lower']), 3)), " ", as.character(round(as.numeric(params['rmsea.ci.upper']), 3)), "]", sep="")
param_values <- c(as.character(round(as.numeric(params['cfi']), 3)), ci)

d <- data.frame(param_name, param_values)
names(d) <- c("Parameters", "Values")
```

```{r mdl_summary_print_pcs_nz_mn, echo=FALSE, eval=TRUE, include=FALSE}
cfaFit.CI.NZ <- cfa(model = structurePCS, data = subset(dataSourcePCS, country == "New Zealand"))
cfaFit.CI.Mn <- cfa(model = structurePCS, data = subset(dataSourcePCS, country == "Mongolia"))

a<-summary(cfaFit.CI.NZ, fit.measures = TRUE, standardize = TRUE, rsquare = TRUE)
params<-a$fit

param_name <- c("CFI", "RMSEA [90% CI]")
ci <- paste(as.character(round(as.numeric(params['rmsea']), 3)), " [", as.character(round(as.numeric(params['rmsea.ci.lower']), 3)), " ", as.character(round(as.numeric(params['rmsea.ci.upper']), 3)), "]", sep="")
param_values <- c(as.character(round(as.numeric(params['cfi']), 3)), ci)

d.nz <- data.frame(param_name, param_values)
names(d.nz) <- c("Parameters", "Values")

a<-summary(cfaFit.CI.Mn, fit.measures = TRUE, standardize = TRUE, rsquare = TRUE)
params<-a$fit

param_name <- c("CFI", "RMSEA [90% CI]")
ci <- paste(as.character(round(as.numeric(params['rmsea']), 3)), " [", as.character(round(as.numeric(params['rmsea.ci.lower']), 3)), " ", as.character(round(as.numeric(params['rmsea.ci.upper']), 3)), "]", sep="")
param_values <- c(as.character(round(as.numeric(params['cfi']), 3)), ci)

d.mn <- data.frame(param_name, param_values)
names(d.mn) <- c("Parameters", "Values")
```

```{r pcs_fits_print, echo=FALSE, render=lemon_print}
d.nz$Model <- "New Zealand"
d.mn$Model <- "Mongolia"
d$Model <- "Configural"

pd <- rbind(d.nz, d.mn, d)

pd <- pd[, c(3, 1, 2)]

head(pd, n = 10)
```

#### Test for Metric Invariance
The test statistics (Chi-squared difference [12] = 11.230, p = 0.509) support the null hypothesis that the configural model is not an improvement over the model with loadings constrained across nationalities. Thus, the two models which allow same or different factor loadings across the nationalities (New Zealand, Mongolia) result in the same fit. This result implies that the factor loadings across the two nationalities are same.
```{r test_me_invar_pcs, echo=TRUE}
cfaFit.MI <- cfa(model = structurePCS,
                 data = dataSourcePCS, group = "country",
                 group.equal = "loadings")
```
```{r test_me_invar_results_pcs, echo=FALSE, render=lemon_print}
anovaResults<-as.data.frame(anova(cfaFit.MI, cfaFit.CI))
anovaResults <- round(anovaResults, 4)

anovaResults[is.na(anovaResults)] <- ""
head(anovaResults)
```

#### Factor Loadings from Configural Model
```{r fct_load_config_mdl_pcs, echo=FALSE, render=lemon_print}
b<-a.super$pe
params_loads<-subset(b, op == "=~")
params_loads$Nationality <- factor(params_loads$group, levels = c(1, 2), labels = c("New Zealand", "Mongolia"))

params_loads$lhs <- as.factor(params_loads$lhs)
params_loads$rhs <- as.factor(params_loads$rhs)

params_loads[, c(2, seq(4, 11), 13)] <- NULL

params_loads <- params_loads[, c(4, 1, 2, 3)]
names(params_loads) <- c("Nationality", "Factor", "Item", "Loading")
params_loads[,4] <- round(params_loads[,4], 3)

params_loads.NZ <- subset(params_loads, Nationality == "New Zealand")
params_loads.NZ$Nationality <- NULL
params_loads.NZ$`Loading (NZ)` <- params_loads.NZ$Loading
params_loads.NZ$Loading <- NULL

params_loads.Mong <- subset(params_loads, Nationality != "New Zealand")
params_loads.Mong$Nationality <- NULL
params_loads.Mong$`Loading (Mongolia)` <- params_loads.Mong$Loading
params_loads.Mong$Loading <- NULL
params_loads.Mong$Factor <-  NULL
params_loads.Mong$Item <-  NULL

params_loads <- cbind(params_loads.NZ, params_loads.Mong)
head(params_loads, n = 100)
```

\newpage

#### Summary
The model with three factor configuration for PCS across the two nationalities seems to have some weak evidence (CFI = 0.909 and RMSEA = 0.113 90% CI [0.1, 0.127]). There is also evidence (Chi-squared difference [12] = 11.230, p = 0.509) to support the hypothesis that the three factors hold same meaning across the two nationalities.

\newpage

# Appendix A: Complete Output from Models
## Configural Model for BPI
```{r complete_mdl_bpi, echo=FALSE}
summary(cfaFit.CI.BPI, fit.measures = TRUE, standardize = TRUE, rsquare = TRUE)
```
## DASS Model for New Zealand
```{r complete_mdl_dass, echo=FALSE}
summary(cfaFit.NZ, fit.measures = TRUE, standardize = TRUE, rsquare = TRUE)
```
## Configural Model for PCS
```{r complete_mdl_pcs, echo=FALSE}
summary(cfaFit.CI.PCS, fit.measures = TRUE, standardize = TRUE, rsquare = TRUE)
```

\newpage

# References