-   <a href="#statistical-analysis"
    id="toc-statistical-analysis">Statistical Analysis</a>
    -   <a href="#model-structure" id="toc-model-structure">Model Structure</a>
        -   <a href="#brief-pain-inventory" id="toc-brief-pain-inventory">Brief Pain
            Inventory</a>
        -   <a href="#depression-anxiety-stress-scale"
            id="toc-depression-anxiety-stress-scale">Depression, Anxiety, Stress
            Scale</a>
        -   <a href="#pain-catastrophizing-scale"
            id="toc-pain-catastrophizing-scale">Pain Catastrophizing Scale</a>
    -   <a href="#evaluation-of-measurement-invariance-across-nationalities"
        id="toc-evaluation-of-measurement-invariance-across-nationalities">Evaluation
        of Measurement Invariance across Nationalities</a>
        -   <a href="#brief-pain-inventory-1" id="toc-brief-pain-inventory-1">Brief
            Pain Inventory</a>
            -   <a href="#configural-invariance"
                id="toc-configural-invariance">Configural Invariance</a>
            -   <a href="#model-fit-estimates-for-configural-invariance"
                id="toc-model-fit-estimates-for-configural-invariance">Model Fit
                Estimates for Configural Invariance</a>
            -   <a href="#test-for-metric-invariance"
                id="toc-test-for-metric-invariance">Test for Metric Invariance</a>
            -   <a href="#summary" id="toc-summary">Summary</a>
        -   <a href="#depression-anxiety-stress-scale-1"
            id="toc-depression-anxiety-stress-scale-1">Depression, Anxiety, Stress
            Scale</a>
            -   <a href="#configural-invariance-1"
                id="toc-configural-invariance-1">Configural Invariance</a>
            -   <a href="#model-fit-for-new-zealand"
                id="toc-model-fit-for-new-zealand">Model Fit for New Zealand</a>
            -   <a href="#summary-1" id="toc-summary-1">Summary</a>
        -   <a href="#pain-catastrophizing-scale-1"
            id="toc-pain-catastrophizing-scale-1">Pain Catastrophizing Scale</a>
            -   <a href="#configural-invariance-2"
                id="toc-configural-invariance-2">Configural Invariance</a>
            -   <a href="#configural-invariance-magnification-variance0"
                id="toc-configural-invariance-magnification-variance0">Configural
                Invariance (Magnification Variance=0)</a>
            -   <a href="#model-fit-estimates-for-configural-invariance-1"
                id="toc-model-fit-estimates-for-configural-invariance-1">Model Fit
                Estimates for Configural Invariance</a>
            -   <a href="#test-for-metric-invariance-1"
                id="toc-test-for-metric-invariance-1">Test for Metric Invariance</a>
            -   <a href="#factor-loadings-from-configural-model"
                id="toc-factor-loadings-from-configural-model">Factor Loadings from
                Configural Model</a>
            -   <a href="#summary-2" id="toc-summary-2">Summary</a>
-   <a href="#appendix-a-complete-output-from-models"
    id="toc-appendix-a-complete-output-from-models">Appendix A: Complete
    Output from Models</a>
    -   <a href="#configural-model-for-bpi"
        id="toc-configural-model-for-bpi">Configural Model for BPI</a>
    -   <a href="#dass-model-for-new-zealand"
        id="toc-dass-model-for-new-zealand">DASS Model for New Zealand</a>
    -   <a href="#configural-model-for-pcs"
        id="toc-configural-model-for-pcs">Configural Model for PCS</a>
-   <a href="#references" id="toc-references">References</a>

# Statistical Analysis

The aim of this analysis is to evaluate measurement invariance in the
Brief Pain Inventory scale (BPI), Depression, Anxiety, Stress Scale
(DASS-21) and Pain Catastrophizing Scale (PCS) across two nationalities
(New Zealand, Mongolia). Measurement invariance is assessed at two
sequential levels: configural and metric (Van de Schoot, Lugtig, & Hox,
2012). Configural invariance is assumed if the same model structure is
successfully fitted across the nationalities. If the same model
structure can not be fitted successfully across the two nationalities,
the model structure is fitted in each nationality separately to test
whether the proposed theoretical structure can be confirmed in each
nationality or not? Metric invariance is assumed if the same model
structure with same factor loadings is successfully fitted across the
nationalities. Metric invariance is interpreted to imply same meaning
across nationalities for the latent constructs.
All the models are fitted using the maximum likelihood method in R (R
Foundation for Statistical Computing, Vienna, Austria) version 3.5.1 (R
Core Team, 2018) using package lavaan version 0.6-4 (Rosseel, 2012). A
model’s goodness-of-the-fit is evaluated with comparative fit index
(CFI) and root mean square error of approximation (RMSEA). For CFI,
values greater than 0.9 and 0.95 are interpreted as adequate and good
fit (Van de Schoot et al., 2012). For RMSEA, values less than 0.08 and
0.05 are interpreted as adequate and good fit (Van de Schoot et al.,
2012). However, these cut-offs are only treated as indicative of good
fit and not as golden rules (Lai & Green, 2016). Each level of
invariance is evaluated with a Chi-squared test for the null hypothesis
that the less constrained model does not fit the data better than the
more constrained model. For example, to evaluate metric invariance, the
fit of the model with same structure across nationalities is compared to
the fit of the model with same structure and factor loadings across
nationalities. In this comparison, configural model is less constrained
as it has more free parameters. The model with same structure and factor
loadings across the groups is more constrained as it has less number of
free parameters due to the fact that the factor loadings are held
constant across nationalities. Statistical significance is assumed below
0.05.

## Model Structure

### Brief Pain Inventory

The model structure fitted to the data is given below in formula syntax
(Rosseel, 2012) and is adopted from the past work of Cleeland, Ladinsky,
Serlin, & Thuy (1988) on BPI.

``` r
structureBPI <-'Intensity        =~ worst + least + average + now
                Interference     =~ activity + mood + walking + work + relations + sleep + enjoyment'
```

### Depression, Anxiety, Stress Scale

The model structure stated below for DASS is based on the work of Norton
(2007).

``` r
structureDASS <-'Depression      =~ DASS3 + DASS5 + DASS10 + DASS13 + DASS16 + DASS17 + DASS21
                 Anxiety         =~ DASS2 + DASS4 + DASS7  + DASS9  + DASS15 + DASS19 + DASS20
                 Stress          =~ DASS1 + DASS6 + DASS8  + DASS11 + DASS12 + DASS14 + DASS18'
```

### Pain Catastrophizing Scale

Following model structure for PCS is based on the work of Joyce, Harris,
& Ellis (2004).

``` r
structurePCS <- 'Rumination      =~ PCS8 + PCS9 + PCS10 + PCS11
                 Magnification   =~ PCS6 + PCS7 + PCS13
                 Helplessness    =~ PCS1 + PCS2 + PCS3 + PCS4 + PCS5 + PCS12
                 Catastrophizing =~ Rumination + Magnification + Helplessness'
```

## Evaluation of Measurement Invariance across Nationalities

### Brief Pain Inventory

#### Configural Invariance

``` r
cfaFit.CI <- cfa(model = structureBPI, data = dataSourceBPI, group = "country")
```

#### Model Fit Estimates for Configural Invariance

CFI = 0.879 and RMSEA = 0.142 90% CI \[0.126, 0.158\] both suggest a
poor model fit.

| Model       | Parameters       | Values                |
|:------------|:-----------------|:----------------------|
| New Zealand | CFI              | 0.886                 |
| New Zealand | RMSEA \[90% CI\] | 0.146 \[0.123 0.169\] |
| Mongolia    | CFI              | 0.87                  |
| Mongolia    | RMSEA \[90% CI\] | 0.138 \[0.115 0.161\] |
| Configural  | CFI              | 0.879                 |
| Configural  | RMSEA \[90% CI\] | 0.142 \[0.126 0.158\] |

#### Test for Metric Invariance

The test statistics (Chi-squared difference \[9\] = 56.751, p \< 0.0001)
reject the null hypothesis that the configural model is not an
improvement over the model with loadings constrained across
nationalities. Thus, the two models which allow same or different factor
loadings across the nationalities (New Zealand, Mongolia) result in
different fits. This result implies that the factor loadings across the
two nationalities are not same.

``` r
cfaFit.MI <- cfa(model = structureBPI,
                 data = dataSourceBPI, group = "country",
                 group.equal = "loadings")
```

|           |  Df |      AIC |      BIC |    Chisq | Chisq diff | Df diff | Pr(\>Chisq) |
|:----------|----:|---------:|---------:|---------:|:-----------|:--------|:------------|
| cfaFit.CI |  86 | 12646.38 | 12893.30 | 327.6645 |            |         |             |
| cfaFit.MI |  95 | 12685.13 | 12899.37 | 384.4159 | 56.7514    | 9       | 0           |

#### Summary

The model with two factor configuration for BPI seems implausible in
both New Zealand (CFI = 0.886 and RMSEA = 0.146 90% CI \[0.123, 0.169\])
and Mongolia (CFI = 0.870 and RMSEA = 0.138 90% CI \[0.115, 0.161\]).
The model fit across the two nationalities is also poor (CFI = 0.879 and
RMSEA = 0.142 90% CI \[0.126, 0.158\]). Moreover, there is evidence
(Chi-squared difference \[9\] = 56.751, p \< 0.0001) to suggest that
these factors do not have same meaning across the two nationalities.

### Depression, Anxiety, Stress Scale

#### Configural Invariance

``` r
cfaFit.CI <- cfa(model = structureDASS, data = dataSourceDASS, group = "country")
```

    ## Warning in lav_object_post_check(object): lavaan WARNING: covariance matrix of latent variables
    ##                 is not positive definite in group 2;
    ##                 use lavInspect(fit, "cov.lv") to investigate.

##### Issue of Non-positive Definite Covariance Matrix

The covariance matrix estimated for Mongolia is not positive definite.
Positive definite covariance matrix is a requirement for valid model
estimation. The reasons underlying this problem are revealed with a
comparative analysis of the estimated correlation matrices.

Estimated correlation matrix for Mongolia

|            | Depression |   Anxiety |    Stress |
|:-----------|-----------:|----------:|----------:|
| Depression |  1.0000000 | 0.9377136 | 1.0145449 |
| Anxiety    |  0.9377136 | 1.0000000 | 0.9737992 |
| Stress     |  1.0145449 | 0.9737992 | 1.0000000 |

Estimated correlation matrix for New Zealand

|            | Depression |   Anxiety |    Stress |
|:-----------|-----------:|----------:|----------:|
| Depression |  1.0000000 | 0.6512748 | 0.8785345 |
| Anxiety    |  0.6512748 | 1.0000000 | 0.7517604 |
| Stress     |  0.8785345 | 0.7517604 | 1.0000000 |

A comparison of the above two matrices reveal that the factors are
highly correlated (\> 0.9) in the model estimated for Mongolia. This
result casts doubt on the hypothesis that the DASS scale is measuring
three constructs, as specified in the model structure, in the case of
Mongolia.

#### Model Fit for New Zealand

``` r
cfaFit.NZ <- cfa(model = structureDASS, data = subset(dataSourceDASS, country == "New Zealand"))
```

CFI = 0.897 and RMSEA = 0.086 90% CI \[0.073 0.098\] both suggest a poor
model fit, indicating absence of evidence for the three factor DASS
structure in the case of New Zealand.

| Parameters       | Values                |
|:-----------------|:----------------------|
| CFI              | 0.897                 |
| RMSEA \[90% CI\] | 0.086 \[0.073 0.098\] |

#### Summary

The model with three factor configuration for DASS appears unconvincing
across the two nationalities. This assertion is supported by the fact
that the model has failed to fit the data from Mongolia as the factors
are highly correlated (r \> 0.9) to each other. The model fit for New
Zealand has also exhibited poor goodness-of-the-fit measures (CFI =
0.897 and RMSEA = 0.086 90% CI \[0.073 0.098\]). The metric invariance
can not be tested as the same model structure did not fit the data from
the two nationalities.

### Pain Catastrophizing Scale

#### Configural Invariance

``` r
cfaFit.CI <- cfa(model = structurePCS, data = dataSourcePCS, group = "country")
```

    ## Warning in lav_object_post_check(object): lavaan WARNING: some estimated lv
    ## variances are negative

##### Issue of Negative Variance Estimate

The variance estimated for magnification in the model for is negative
(-0.046, SE 0.042). This indicates occurrence of a Heywood case (Chen,
Bollen, Paxton, Curran, & Kirby, 2001). This may be caused by a sampling
fluctuation or misspecification of the model structure.

| Model Term      | Variance (Mongolia) | SE (Mongolia) | Variance (NZ) | SE (NZ) |
|:----------------|--------------------:|--------------:|--------------:|--------:|
| PCS8            |               1.057 |         0.134 |         0.939 |   0.117 |
| PCS9            |               0.422 |         0.065 |         0.359 |   0.058 |
| PCS10           |               0.405 |         0.061 |         0.307 |   0.050 |
| PCS11           |               0.542 |         0.077 |         0.460 |   0.066 |
| PCS6            |               0.620 |         0.085 |         0.722 |   0.110 |
| PCS7            |               0.723 |         0.091 |         1.035 |   0.132 |
| PCS13           |               0.714 |         0.099 |         1.152 |   0.149 |
| PCS1            |               0.599 |         0.077 |         0.648 |   0.088 |
| PCS2            |               0.527 |         0.073 |         0.940 |   0.118 |
| PCS3            |               0.365 |         0.053 |         0.566 |   0.080 |
| PCS4            |               0.629 |         0.086 |         0.493 |   0.071 |
| PCS5            |               0.573 |         0.077 |         0.770 |   0.101 |
| PCS12           |               0.632 |         0.081 |         0.969 |   0.121 |
| Rumination      |               0.064 |         0.034 |         0.123 |   0.046 |
| Magnification   |              -0.046 |         0.042 |         0.001 |   0.074 |
| Helplessness    |               0.049 |         0.023 |         0.166 |   0.055 |
| Catastrophizing |               0.711 |         0.175 |         0.793 |   0.177 |

To ascertain that it is not caused by a sampling fluctuation, a
one-sided null hypothesis test for variance estimate equal to 0 is
performed with the alternative hypothesis that the estimate is negative.
The test is based on the z-score obtained as a ratio of the variance
estimate and its standard error (Chen et al., 2001). The test result (z
= -1.095, p(\<z) = 0.137) indicates that there is not enough evidence to
reject the null that the estimate is 0. Thus, as suggested by Chen et
al. (2001), the variance for magnification in the model for Mongolia is
fixed at 0. Moreover, the variance estimate for magnification in the NZ
model (0.001, SE 0.074, z=0.014, p(\<z) = 0.505) is also set to 0 to fit
the same model structure across the nationalities.

#### Configural Invariance (Magnification Variance=0)

``` r
structurePCS <- 'Rumination      =~ PCS8 + PCS9 + PCS10 + PCS11
                 Magnification   =~ PCS6 + PCS7 + PCS13
                 Helplessness    =~ PCS1 + PCS2 + PCS3 + PCS4 + PCS5 + PCS12
                 Catastrophizing =~ Rumination + Magnification + Helplessness
                 Magnification   ~~ 0*Magnification'
cfaFit.CI <- cfa(model = structurePCS, data = dataSourcePCS, group = "country")
```

#### Model Fit Estimates for Configural Invariance

CFI = 0.909 and RMSEA = 0.113 90% CI \[0.1, 0.127\] suggest a
discrepancy between the model fit estimates as CFI \> 0.9 indicates
adequate fit and RMSEA \> 0.08 indicates poor fit. As suggested by Lai &
Green (2016), this does not necessarily imply a bad fit due to model
misspecification. Thus, to further investigate the measurement
invariance across nationalities, we perform tests for metric invariance.

| Model       | Parameters       | Values                |
|:------------|:-----------------|:----------------------|
| New Zealand | CFI              | 0.906                 |
| New Zealand | RMSEA \[90% CI\] | 0.117 \[0.098 0.136\] |
| Mongolia    | CFI              | 0.913                 |
| Mongolia    | RMSEA \[90% CI\] | 0.11 \[0.09 0.13\]    |
| Configural  | CFI              | 0.909                 |
| Configural  | RMSEA \[90% CI\] | 0.113 \[0.1 0.127\]   |

#### Test for Metric Invariance

The test statistics (Chi-squared difference \[12\] = 11.230, p = 0.509)
support the null hypothesis that the configural model is not an
improvement over the model with loadings constrained across
nationalities. Thus, the two models which allow same or different factor
loadings across the nationalities (New Zealand, Mongolia) result in the
same fit. This result implies that the factor loadings across the two
nationalities are same.

``` r
cfaFit.MI <- cfa(model = structurePCS,
                 data = dataSourcePCS, group = "country",
                 group.equal = "loadings")
```

|           |  Df |      AIC |      BIC |    Chisq | Chisq diff | Df diff | Pr(\>Chisq) |
|:----------|----:|---------:|---------:|---------:|:-----------|:--------|:------------|
| cfaFit.CI | 126 | 10132.81 | 10433.18 | 359.6905 |            |         |             |
| cfaFit.MI | 138 | 10120.04 | 10376.45 | 370.9209 | 11.2303    | 12      | 0.5093      |

#### Factor Loadings from Configural Model

| Factor          | Item          | Loading (NZ) | Loading (Mongolia) |
|:----------------|:--------------|-------------:|-------------------:|
| Rumination      | PCS8          |        0.703 |              0.651 |
| Rumination      | PCS9          |        0.891 |              0.852 |
| Rumination      | PCS10         |        0.893 |              0.845 |
| Rumination      | PCS11         |        0.852 |              0.812 |
| Magnification   | PCS6          |        0.790 |              0.754 |
| Magnification   | PCS7          |        0.657 |              0.641 |
| Magnification   | PCS13         |        0.680 |              0.763 |
| Helplessness    | PCS1          |        0.789 |              0.692 |
| Helplessness    | PCS2          |        0.670 |              0.798 |
| Helplessness    | PCS3          |        0.819 |              0.827 |
| Helplessness    | PCS4          |        0.832 |              0.786 |
| Helplessness    | PCS5          |        0.757 |              0.756 |
| Helplessness    | PCS12         |        0.657 |              0.694 |
| Catastrophizing | Rumination    |        0.930 |              0.961 |
| Catastrophizing | Magnification |        1.000 |              1.000 |
| Catastrophizing | Helplessness  |        0.919 |              0.957 |

#### Summary

The model with three factor configuration for PCS across the two
nationalities seems to have some weak evidence (CFI = 0.909 and RMSEA =
0.113 90% CI \[0.1, 0.127\]). There is also evidence (Chi-squared
difference \[12\] = 11.230, p = 0.509) to support the hypothesis that
the three factors hold same meaning across the two nationalities.

# Appendix A: Complete Output from Models

## Configural Model for BPI

    ## lavaan 0.6-12 ended normally after 78 iterations
    ## 
    ##   Estimator                                         ML
    ##   Optimization method                           NLMINB
    ##   Number of model parameters                        68
    ## 
    ##   Number of observations per group:               Used       Total
    ##     New Zealand                                    139         159
    ##     Mongolia                                       140         142
    ## 
    ## Model Test User Model:
    ##                                                       
    ##   Test statistic                               327.665
    ##   Degrees of freedom                                86
    ##   P-value (Chi-square)                           0.000
    ##   Test statistic for each group:
    ##     New Zealand                                169.964
    ##     Mongolia                                   157.701
    ## 
    ## Model Test Baseline Model:
    ## 
    ##   Test statistic                              2102.419
    ##   Degrees of freedom                               110
    ##   P-value                                        0.000
    ## 
    ## User Model versus Baseline Model:
    ## 
    ##   Comparative Fit Index (CFI)                    0.879
    ##   Tucker-Lewis Index (TLI)                       0.845
    ## 
    ## Loglikelihood and Information Criteria:
    ## 
    ##   Loglikelihood user model (H0)              -6255.191
    ##   Loglikelihood unrestricted model (H1)      -6091.358
    ##                                                       
    ##   Akaike (AIC)                               12646.381
    ##   Bayesian (BIC)                             12893.304
    ##   Sample-size adjusted Bayesian (BIC)        12677.682
    ## 
    ## Root Mean Square Error of Approximation:
    ## 
    ##   RMSEA                                          0.142
    ##   90 Percent confidence interval - lower         0.126
    ##   90 Percent confidence interval - upper         0.158
    ##   P-value RMSEA <= 0.05                          0.000
    ## 
    ## Standardized Root Mean Square Residual:
    ## 
    ##   SRMR                                           0.069
    ## 
    ## Parameter Estimates:
    ## 
    ##   Standard errors                             Standard
    ##   Information                                 Expected
    ##   Information saturated (h1) model          Structured
    ## 
    ## 
    ## Group 1 [New Zealand]:
    ## 
    ## Latent Variables:
    ##                    Estimate  Std.Err  z-value  P(>|z|)   Std.lv  Std.all
    ##   Intensity =~                                                          
    ##     worst             1.000                               1.342    0.713
    ##     least             1.491    0.155    9.632    0.000    2.002    0.845
    ##     average           1.358    0.130   10.474    0.000    1.823    0.929
    ##     now               1.566    0.158    9.945    0.000    2.103    0.873
    ##   Interference =~                                                       
    ##     activity          1.000                               2.185    0.866
    ##     mood              0.926    0.085   10.905    0.000    2.024    0.764
    ##     walking           0.994    0.120    8.312    0.000    2.173    0.633
    ##     work              0.987    0.073   13.455    0.000    2.157    0.866
    ##     relations         1.019    0.094   10.825    0.000    2.226    0.761
    ##     sleep             0.843    0.103    8.190    0.000    1.843    0.626
    ##     enjoyment         0.933    0.077   12.075    0.000    2.039    0.814
    ## 
    ## Covariances:
    ##                    Estimate  Std.Err  z-value  P(>|z|)   Std.lv  Std.all
    ##   Intensity ~~                                                          
    ##     Interference      1.759    0.350    5.024    0.000    0.600    0.600
    ## 
    ## Intercepts:
    ##                    Estimate  Std.Err  z-value  P(>|z|)   Std.lv  Std.all
    ##    .worst             7.799    0.160   48.853    0.000    7.799    4.144
    ##    .least             3.899    0.201   19.399    0.000    3.899    1.645
    ##    .average           5.835    0.166   35.056    0.000    5.835    2.973
    ##    .now               5.633    0.204   27.575    0.000    5.633    2.339
    ##    .activity          6.914    0.214   32.304    0.000    6.914    2.740
    ##    .mood              6.906    0.225   30.732    0.000    6.906    2.607
    ##    .walking           5.137    0.291   17.640    0.000    5.137    1.496
    ##    .work              6.906    0.211   32.702    0.000    6.906    2.774
    ##    .relations         5.705    0.248   22.979    0.000    5.705    1.949
    ##    .sleep             6.813    0.250   27.279    0.000    6.813    2.314
    ##    .enjoyment         7.396    0.213   34.788    0.000    7.396    2.951
    ##     Intensity         0.000                               0.000    0.000
    ##     Interference      0.000                               0.000    0.000
    ## 
    ## Variances:
    ##                    Estimate  Std.Err  z-value  P(>|z|)   Std.lv  Std.all
    ##    .worst             1.740    0.227    7.678    0.000    1.740    0.491
    ##    .least             1.608    0.241    6.666    0.000    1.608    0.286
    ##    .average           0.529    0.126    4.209    0.000    0.529    0.137
    ##    .now               1.379    0.225    6.121    0.000    1.379    0.238
    ##    .activity          1.591    0.253    6.293    0.000    1.591    0.250
    ##    .mood              2.922    0.395    7.392    0.000    2.922    0.416
    ##    .walking           7.065    0.895    7.890    0.000    7.065    0.599
    ##    .work              1.549    0.246    6.293    0.000    1.549    0.250
    ##    .relations         3.612    0.487    7.413    0.000    3.612    0.422
    ##    .sleep             5.273    0.667    7.906    0.000    5.273    0.608
    ##    .enjoyment         2.124    0.303    7.012    0.000    2.124    0.338
    ##     Intensity         1.802    0.380    4.736    0.000    1.000    1.000
    ##     Interference      4.776    0.758    6.302    0.000    1.000    1.000
    ## 
    ## R-Square:
    ##                    Estimate
    ##     worst             0.509
    ##     least             0.714
    ##     average           0.863
    ##     now               0.762
    ##     activity          0.750
    ##     mood              0.584
    ##     walking           0.401
    ##     work              0.750
    ##     relations         0.578
    ##     sleep             0.392
    ##     enjoyment         0.662
    ## 
    ## 
    ## Group 2 [Mongolia]:
    ## 
    ## Latent Variables:
    ##                    Estimate  Std.Err  z-value  P(>|z|)   Std.lv  Std.all
    ##   Intensity =~                                                          
    ##     worst             1.000                               1.874    0.790
    ##     least             0.490    0.074    6.668    0.000    0.918    0.544
    ##     average           0.858    0.076   11.318    0.000    1.608    0.971
    ##     now               0.665    0.094    7.065    0.000    1.246    0.572
    ##   Interference =~                                                       
    ##     activity          1.000                               1.993    0.773
    ##     mood              0.886    0.106    8.396    0.000    1.765    0.689
    ##     walking           1.026    0.126    8.165    0.000    2.045    0.673
    ##     work              1.162    0.105   11.093    0.000    2.316    0.873
    ##     relations         0.937    0.113    8.304    0.000    1.867    0.682
    ##     sleep             1.099    0.119    9.254    0.000    2.190    0.749
    ##     enjoyment         1.214    0.119   10.169    0.000    2.419    0.811
    ## 
    ## Covariances:
    ##                    Estimate  Std.Err  z-value  P(>|z|)   Std.lv  Std.all
    ##   Intensity ~~                                                          
    ##     Interference      2.089    0.440    4.747    0.000    0.559    0.559
    ## 
    ## Intercepts:
    ##                    Estimate  Std.Err  z-value  P(>|z|)   Std.lv  Std.all
    ##    .worst             4.936    0.200   24.641    0.000    4.936    2.083
    ##    .least             1.764    0.143   12.362    0.000    1.764    1.045
    ##    .average           3.357    0.140   23.980    0.000    3.357    2.027
    ##    .now               2.800    0.184   15.208    0.000    2.800    1.285
    ##    .activity          4.257    0.218   19.536    0.000    4.257    1.651
    ##    .mood              3.507    0.217   16.197    0.000    3.507    1.369
    ##    .walking           4.671    0.257   18.175    0.000    4.671    1.536
    ##    .work              4.093    0.224   18.250    0.000    4.093    1.542
    ##    .relations         3.350    0.231   14.488    0.000    3.350    1.225
    ##    .sleep             3.793    0.247   15.348    0.000    3.793    1.297
    ##    .enjoyment         3.671    0.252   14.556    0.000    3.671    1.230
    ##     Intensity         0.000                               0.000    0.000
    ##     Interference      0.000                               0.000    0.000
    ## 
    ## Variances:
    ##                    Estimate  Std.Err  z-value  P(>|z|)   Std.lv  Std.all
    ##    .worst             2.107    0.325    6.480    0.000    2.107    0.375
    ##    .least             2.008    0.248    8.099    0.000    2.008    0.704
    ##    .average           0.157    0.149    1.057    0.291    0.157    0.057
    ##    .now               3.192    0.397    8.041    0.000    3.192    0.673
    ##    .activity          2.676    0.371    7.206    0.000    2.676    0.402
    ##    .mood              3.447    0.450    7.665    0.000    3.447    0.525
    ##    .walking           5.065    0.656    7.726    0.000    5.065    0.548
    ##    .work              1.680    0.286    5.863    0.000    1.680    0.239
    ##    .relations         3.998    0.520    7.690    0.000    3.998    0.534
    ##    .sleep             3.753    0.509    7.370    0.000    3.753    0.439
    ##    .enjoyment         3.053    0.445    6.861    0.000    3.053    0.343
    ##     Intensity         3.510    0.655    5.355    0.000    1.000    1.000
    ##     Interference      3.973    0.751    5.286    0.000    1.000    1.000
    ## 
    ## R-Square:
    ##                    Estimate
    ##     worst             0.625
    ##     least             0.296
    ##     average           0.943
    ##     now               0.327
    ##     activity          0.598
    ##     mood              0.475
    ##     walking           0.452
    ##     work              0.761
    ##     relations         0.466
    ##     sleep             0.561
    ##     enjoyment         0.657

## DASS Model for New Zealand

    ## lavaan 0.6-12 ended normally after 51 iterations
    ## 
    ##   Estimator                                         ML
    ##   Optimization method                           NLMINB
    ##   Number of model parameters                        45
    ## 
    ##                                                   Used       Total
    ##   Number of observations                           139         159
    ## 
    ## Model Test User Model:
    ##                                                       
    ##   Test statistic                               375.019
    ##   Degrees of freedom                               186
    ##   P-value (Chi-square)                           0.000
    ## 
    ## Model Test Baseline Model:
    ## 
    ##   Test statistic                              2045.571
    ##   Degrees of freedom                               210
    ##   P-value                                        0.000
    ## 
    ## User Model versus Baseline Model:
    ## 
    ##   Comparative Fit Index (CFI)                    0.897
    ##   Tucker-Lewis Index (TLI)                       0.884
    ## 
    ## Loglikelihood and Information Criteria:
    ## 
    ##   Loglikelihood user model (H0)              -3353.081
    ##   Loglikelihood unrestricted model (H1)      -3165.571
    ##                                                       
    ##   Akaike (AIC)                                6796.161
    ##   Bayesian (BIC)                              6928.212
    ##   Sample-size adjusted Bayesian (BIC)         6785.843
    ## 
    ## Root Mean Square Error of Approximation:
    ## 
    ##   RMSEA                                          0.086
    ##   90 Percent confidence interval - lower         0.073
    ##   90 Percent confidence interval - upper         0.098
    ##   P-value RMSEA <= 0.05                          0.000
    ## 
    ## Standardized Root Mean Square Residual:
    ## 
    ##   SRMR                                           0.069
    ## 
    ## Parameter Estimates:
    ## 
    ##   Standard errors                             Standard
    ##   Information                                 Expected
    ##   Information saturated (h1) model          Structured
    ## 
    ## Latent Variables:
    ##                    Estimate  Std.Err  z-value  P(>|z|)   Std.lv  Std.all
    ##   Depression =~                                                         
    ##     DASS3             1.000                               0.703    0.741
    ##     DASS5             1.037    0.124    8.353    0.000    0.728    0.702
    ##     DASS10            1.322    0.125   10.585    0.000    0.929    0.870
    ##     DASS13            1.157    0.116    9.968    0.000    0.813    0.824
    ##     DASS16            1.258    0.119   10.535    0.000    0.884    0.866
    ##     DASS17            1.214    0.127    9.526    0.000    0.853    0.791
    ##     DASS21            1.126    0.127    8.884    0.000    0.791    0.743
    ##   Anxiety =~                                                            
    ##     DASS2             1.000                               0.382    0.334
    ##     DASS4             1.531    0.419    3.655    0.000    0.585    0.645
    ##     DASS7             1.560    0.452    3.455    0.001    0.597    0.532
    ##     DASS9             2.233    0.587    3.801    0.000    0.854    0.769
    ##     DASS15            2.164    0.556    3.889    0.000    0.828    0.884
    ##     DASS19            1.444    0.409    3.534    0.000    0.552    0.571
    ##     DASS20            2.084    0.543    3.840    0.000    0.797    0.814
    ##   Stress =~                                                             
    ##     DASS1             1.000                               0.749    0.702
    ##     DASS6             0.961    0.113    8.477    0.000    0.720    0.762
    ##     DASS8             1.017    0.131    7.756    0.000    0.762    0.695
    ##     DASS11            1.095    0.122    8.983    0.000    0.820    0.809
    ##     DASS12            0.961    0.117    8.210    0.000    0.720    0.737
    ##     DASS14            0.856    0.115    7.472    0.000    0.642    0.668
    ##     DASS18            0.950    0.114    8.355    0.000    0.712    0.750
    ## 
    ## Covariances:
    ##                    Estimate  Std.Err  z-value  P(>|z|)   Std.lv  Std.all
    ##   Depression ~~                                                         
    ##     Anxiety           0.175    0.054    3.228    0.001    0.651    0.651
    ##     Stress            0.462    0.082    5.641    0.000    0.879    0.879
    ##   Anxiety ~~                                                            
    ##     Stress            0.215    0.066    3.280    0.001    0.752    0.752
    ## 
    ## Variances:
    ##                    Estimate  Std.Err  z-value  P(>|z|)   Std.lv  Std.all
    ##    .DASS3             0.407    0.053    7.684    0.000    0.407    0.452
    ##    .DASS5             0.547    0.070    7.816    0.000    0.547    0.508
    ##    .DASS10            0.277    0.042    6.647    0.000    0.277    0.243
    ##    .DASS13            0.312    0.043    7.191    0.000    0.312    0.321
    ##    .DASS16            0.260    0.039    6.706    0.000    0.260    0.249
    ##    .DASS17            0.435    0.058    7.434    0.000    0.435    0.374
    ##    .DASS21            0.509    0.066    7.676    0.000    0.509    0.449
    ##    .DASS2             1.169    0.142    8.230    0.000    1.169    0.889
    ##    .DASS4             0.482    0.062    7.721    0.000    0.482    0.585
    ##    .DASS7             0.903    0.113    7.997    0.000    0.903    0.717
    ##    .DASS9             0.505    0.071    7.062    0.000    0.505    0.409
    ##    .DASS15            0.191    0.037    5.178    0.000    0.191    0.218
    ##    .DASS19            0.631    0.080    7.919    0.000    0.631    0.674
    ##    .DASS20            0.324    0.049    6.588    0.000    0.324    0.338
    ##    .DASS1             0.579    0.076    7.663    0.000    0.579    0.508
    ##    .DASS6             0.375    0.051    7.371    0.000    0.375    0.420
    ##    .DASS8             0.623    0.081    7.689    0.000    0.623    0.518
    ##    .DASS11            0.354    0.051    7.002    0.000    0.354    0.345
    ##    .DASS12            0.436    0.058    7.509    0.000    0.436    0.457
    ##    .DASS14            0.510    0.066    7.776    0.000    0.510    0.553
    ##    .DASS18            0.393    0.053    7.438    0.000    0.393    0.437
    ##     Depression        0.494    0.099    5.012    0.000    1.000    1.000
    ##     Anxiety           0.146    0.076    1.930    0.054    1.000    1.000
    ##     Stress            0.561    0.122    4.618    0.000    1.000    1.000
    ## 
    ## R-Square:
    ##                    Estimate
    ##     DASS3             0.548
    ##     DASS5             0.492
    ##     DASS10            0.757
    ##     DASS13            0.679
    ##     DASS16            0.751
    ##     DASS17            0.626
    ##     DASS21            0.551
    ##     DASS2             0.111
    ##     DASS4             0.415
    ##     DASS7             0.283
    ##     DASS9             0.591
    ##     DASS15            0.782
    ##     DASS19            0.326
    ##     DASS20            0.662
    ##     DASS1             0.492
    ##     DASS6             0.580
    ##     DASS8             0.482
    ##     DASS11            0.655
    ##     DASS12            0.543
    ##     DASS14            0.447
    ##     DASS18            0.563

## Configural Model for PCS

    ## lavaan 0.6-12 ended normally after 47 iterations
    ## 
    ##   Estimator                                         ML
    ##   Optimization method                           NLMINB
    ##   Number of model parameters                        82
    ## 
    ##   Number of observations per group:               Used       Total
    ##     New Zealand                                    148         159
    ##     Mongolia                                       140         142
    ## 
    ## Model Test User Model:
    ##                                                       
    ##   Test statistic                               359.691
    ##   Degrees of freedom                               126
    ##   P-value (Chi-square)                           0.000
    ##   Test statistic for each group:
    ##     New Zealand                                190.564
    ##     Mongolia                                   169.127
    ## 
    ## Model Test Baseline Model:
    ## 
    ##   Test statistic                              2728.962
    ##   Degrees of freedom                               156
    ##   P-value                                        0.000
    ## 
    ## User Model versus Baseline Model:
    ## 
    ##   Comparative Fit Index (CFI)                    0.909
    ##   Tucker-Lewis Index (TLI)                       0.888
    ## 
    ## Loglikelihood and Information Criteria:
    ## 
    ##   Loglikelihood user model (H0)              -4984.406
    ##   Loglikelihood unrestricted model (H1)      -4804.561
    ##                                                       
    ##   Akaike (AIC)                               10132.813
    ##   Bayesian (BIC)                             10433.175
    ##   Sample-size adjusted Bayesian (BIC)        10173.142
    ## 
    ## Root Mean Square Error of Approximation:
    ## 
    ##   RMSEA                                          0.113
    ##   90 Percent confidence interval - lower         0.100
    ##   90 Percent confidence interval - upper         0.127
    ##   P-value RMSEA <= 0.05                          0.000
    ## 
    ## Standardized Root Mean Square Residual:
    ## 
    ##   SRMR                                           0.052
    ## 
    ## Parameter Estimates:
    ## 
    ##   Standard errors                             Standard
    ##   Information                                 Expected
    ##   Information saturated (h1) model          Structured
    ## 
    ## 
    ## Group 1 [New Zealand]:
    ## 
    ## Latent Variables:
    ##                      Estimate  Std.Err  z-value  P(>|z|)   Std.lv  Std.all
    ##   Rumination =~                                                           
    ##     PCS8                1.000                               0.957    0.703
    ##     PCS9                1.227    0.120   10.267    0.000    1.175    0.891
    ##     PCS10               1.150    0.112   10.290    0.000    1.100    0.893
    ##     PCS11               1.154    0.117    9.851    0.000    1.104    0.852
    ##   Magnification =~                                                        
    ##     PCS6                1.000                               1.096    0.790
    ##     PCS7                0.809    0.098    8.290    0.000    0.887    0.657
    ##     PCS13               0.908    0.105    8.632    0.000    0.995    0.680
    ##   Helplessness =~                                                         
    ##     PCS1                1.000                               1.035    0.789
    ##     PCS2                0.846    0.099    8.548    0.000    0.875    0.670
    ##     PCS3                1.036    0.095   10.955    0.000    1.073    0.819
    ##     PCS4                1.016    0.091   11.181    0.000    1.052    0.832
    ##     PCS5                0.982    0.099    9.922    0.000    1.017    0.757
    ##     PCS12               0.828    0.099    8.344    0.000    0.857    0.657
    ##   Catastrophizing =~                                                      
    ##     Rumination          1.000                               0.930    0.930
    ##     Magnification       1.231    0.145    8.509    0.000    1.000    1.000
    ##     Helplessness        1.068    0.134    7.995    0.000    0.919    0.919
    ## 
    ## Intercepts:
    ##                    Estimate  Std.Err  z-value  P(>|z|)   Std.lv  Std.all
    ##    .PCS8              2.372    0.112   21.183    0.000    2.372    1.741
    ##    .PCS9              2.196    0.108   20.260    0.000    2.196    1.665
    ##    .PCS10             2.189    0.101   21.614    0.000    2.189    1.777
    ##    .PCS11             2.554    0.107   23.976    0.000    2.554    1.971
    ##    .PCS6              2.378    0.114   20.858    0.000    2.378    1.714
    ##    .PCS7              1.311    0.111   11.813    0.000    1.311    0.971
    ##    .PCS13             1.784    0.120   14.826    0.000    1.784    1.219
    ##    .PCS1              2.709    0.108   25.136    0.000    2.709    2.066
    ##    .PCS2              1.554    0.107   14.472    0.000    1.554    1.190
    ##    .PCS3              2.419    0.108   22.462    0.000    2.419    1.846
    ##    .PCS4              2.169    0.104   20.861    0.000    2.169    1.715
    ##    .PCS5              2.020    0.110   18.301    0.000    2.020    1.504
    ##    .PCS12             2.284    0.107   21.289    0.000    2.284    1.750
    ##    .Rumination        0.000                               0.000    0.000
    ##    .Magnification     0.000                               0.000    0.000
    ##    .Helplessness      0.000                               0.000    0.000
    ##     Catastrophizng    0.000                               0.000    0.000
    ## 
    ## Variances:
    ##                    Estimate  Std.Err  z-value  P(>|z|)   Std.lv  Std.all
    ##    .Magnification     0.000                               0.000    0.000
    ##    .PCS8              0.939    0.117    8.013    0.000    0.939    0.506
    ##    .PCS9              0.359    0.058    6.207    0.000    0.359    0.206
    ##    .PCS10             0.307    0.050    6.149    0.000    0.307    0.202
    ##    .PCS11             0.460    0.066    6.967    0.000    0.460    0.274
    ##    .PCS6              0.723    0.101    7.156    0.000    0.723    0.375
    ##    .PCS7              1.036    0.130    7.958    0.000    1.036    0.568
    ##    .PCS13             1.152    0.146    7.872    0.000    1.152    0.538
    ##    .PCS1              0.648    0.088    7.368    0.000    0.648    0.377
    ##    .PCS2              0.940    0.118    7.999    0.000    0.940    0.551
    ##    .PCS3              0.566    0.080    7.080    0.000    0.566    0.330
    ##    .PCS4              0.493    0.071    6.919    0.000    0.493    0.308
    ##    .PCS5              0.770    0.101    7.602    0.000    0.770    0.427
    ##    .PCS12             0.969    0.121    8.042    0.000    0.969    0.569
    ##    .Rumination        0.123    0.045    2.744    0.006    0.134    0.134
    ##    .Helplessness      0.167    0.054    3.062    0.002    0.155    0.155
    ##     Catastrophizng    0.793    0.176    4.494    0.000    1.000    1.000
    ## 
    ## R-Square:
    ##                    Estimate
    ##     Magnification     1.000
    ##     PCS8              0.494
    ##     PCS9              0.794
    ##     PCS10             0.798
    ##     PCS11             0.726
    ##     PCS6              0.625
    ##     PCS7              0.432
    ##     PCS13             0.462
    ##     PCS1              0.623
    ##     PCS2              0.449
    ##     PCS3              0.670
    ##     PCS4              0.692
    ##     PCS5              0.573
    ##     PCS12             0.431
    ##     Rumination        0.866
    ##     Helplessness      0.845
    ## 
    ## 
    ## Group 2 [Mongolia]:
    ## 
    ## Latent Variables:
    ##                      Estimate  Std.Err  z-value  P(>|z|)   Std.lv  Std.all
    ##   Rumination =~                                                           
    ##     PCS8                1.000                               0.881    0.651
    ##     PCS9                1.206    0.141    8.560    0.000    1.063    0.852
    ##     PCS10               1.145    0.135    8.505    0.000    1.009    0.845
    ##     PCS11               1.157    0.140    8.248    0.000    1.020    0.812
    ##   Magnification =~                                                        
    ##     PCS6                1.000                               0.887    0.754
    ##     PCS7                0.787    0.103    7.635    0.000    0.698    0.641
    ##     PCS13               1.101    0.119    9.275    0.000    0.976    0.763
    ##   Helplessness =~                                                         
    ##     PCS1                1.000                               0.740    0.692
    ##     PCS2                1.293    0.147    8.776    0.000    0.957    0.798
    ##     PCS3                1.205    0.133    9.067    0.000    0.892    0.827
    ##     PCS4                1.359    0.157    8.660    0.000    1.006    0.786
    ##     PCS5                1.186    0.142    8.347    0.000    0.878    0.756
    ##     PCS12               1.035    0.134    7.699    0.000    0.766    0.694
    ##   Catastrophizing =~                                                      
    ##     Rumination          1.000                               0.961    0.961
    ##     Magnification       1.047    0.139    7.547    0.000    1.000    1.000
    ##     Helplessness        0.836    0.122    6.859    0.000    0.957    0.957
    ## 
    ## Intercepts:
    ##                    Estimate  Std.Err  z-value  P(>|z|)   Std.lv  Std.all
    ##    .PCS8              1.936    0.114   16.924    0.000    1.936    1.430
    ##    .PCS9              1.193    0.105   11.316    0.000    1.193    0.956
    ##    .PCS10             1.400    0.101   13.873    0.000    1.400    1.172
    ##    .PCS11             1.550    0.106   14.609    0.000    1.550    1.235
    ##    .PCS6              1.343    0.099   13.514    0.000    1.343    1.142
    ##    .PCS7              1.221    0.092   13.267    0.000    1.221    1.121
    ##    .PCS13             1.393    0.108   12.875    0.000    1.393    1.088
    ##    .PCS1              1.886    0.090   20.860    0.000    1.886    1.763
    ##    .PCS2              1.300    0.101   12.825    0.000    1.300    1.084
    ##    .PCS3              1.121    0.091   12.300    0.000    1.121    1.040
    ##    .PCS4              1.207    0.108   11.168    0.000    1.207    0.944
    ##    .PCS5              0.964    0.098    9.824    0.000    0.964    0.830
    ##    .PCS12             1.100    0.093   11.790    0.000    1.100    0.996
    ##    .Rumination        0.000                               0.000    0.000
    ##    .Magnification     0.000                               0.000    0.000
    ##    .Helplessness      0.000                               0.000    0.000
    ##     Catastrophizng    0.000                               0.000    0.000
    ## 
    ## Variances:
    ##                    Estimate  Std.Err  z-value  P(>|z|)   Std.lv  Std.all
    ##    .Magnification     0.000                               0.000    0.000
    ##    .PCS8              1.055    0.134    7.864    0.000    1.055    0.576
    ##    .PCS9              0.425    0.066    6.483    0.000    0.425    0.273
    ##    .PCS10             0.408    0.062    6.601    0.000    0.408    0.286
    ##    .PCS11             0.536    0.076    7.012    0.000    0.536    0.340
    ##    .PCS6              0.596    0.080    7.462    0.000    0.596    0.431
    ##    .PCS7              0.700    0.089    7.896    0.000    0.700    0.590
    ##    .PCS13             0.685    0.092    7.410    0.000    0.685    0.418
    ##    .PCS1              0.597    0.077    7.773    0.000    0.597    0.521
    ##    .PCS2              0.523    0.072    7.221    0.000    0.523    0.364
    ##    .PCS3              0.369    0.053    6.947    0.000    0.369    0.317
    ##    .PCS4              0.624    0.085    7.308    0.000    0.624    0.382
    ##    .PCS5              0.578    0.077    7.499    0.000    0.578    0.429
    ##    .PCS12             0.633    0.081    7.767    0.000    0.633    0.519
    ##    .Rumination        0.059    0.034    1.730    0.084    0.076    0.076
    ##    .Helplessness      0.046    0.023    1.950    0.051    0.084    0.084
    ##     Catastrophizng    0.717    0.176    4.072    0.000    1.000    1.000
    ## 
    ## R-Square:
    ##                    Estimate
    ##     Magnification     1.000
    ##     PCS8              0.424
    ##     PCS9              0.727
    ##     PCS10             0.714
    ##     PCS11             0.660
    ##     PCS6              0.569
    ##     PCS7              0.410
    ##     PCS13             0.582
    ##     PCS1              0.479
    ##     PCS2              0.636
    ##     PCS3              0.683
    ##     PCS4              0.618
    ##     PCS5              0.571
    ##     PCS12             0.481
    ##     Rumination        0.924
    ##     Helplessness      0.916

# References

<div id="refs" class="references csl-bib-body hanging-indent"
line-spacing="2">

<div id="ref-chen2001improper" class="csl-entry">

Chen, F., Bollen, K. A., Paxton, P., Curran, P. J., & Kirby, J. B.
(2001). Improper solutions in structural equation models: Causes,
consequences, and strategies. *Sociological Methods & Research*,
*29*(4), 468–508. <https://doi.org/10.1177/0049124101029004003>

</div>

<div id="ref-cleeland1988multidimensional" class="csl-entry">

Cleeland, C. S., Ladinsky, J. L., Serlin, R. C., & Thuy, N. C. (1988).
Multidimensional measurement of cancer pain: Comparisons of US and
vietnamese patients. *Journal of Pain and Symptom Management*, *3*(1),
23–27.

</div>

<div id="ref-joyce2004testing" class="csl-entry">

Joyce, L., Harris, C. A., & Ellis, J. A. (2004). Testing factorial
validity and gender invariance of the pain catastrophizing scale.
*Journal of Behavioral Medicine*, *27*(4), 361–372.
<https://doi.org/10.1023/b:jobm.0000042410.34535.64>

</div>

<div id="ref-lai2016problem" class="csl-entry">

Lai, K., & Green, S. B. (2016). The problem with having two watches:
Assessment of fit when RMSEA and CFI disagree. *Multivariate Behavioral
Research*, *51*(2-3), 220–239.
<https://doi.org/10.1080/00273171.2015.1134306>

</div>

<div id="ref-norton2007depression" class="csl-entry">

Norton, P. J. (2007). Depression anxiety and stress scales (DASS-21):
Psychometric analysis across four racial groups. *Anxiety, Stress, and
Coping*, *20*(3), 253–265. <https://doi.org/10.1080/10615800701309279>

</div>

<div id="ref-forR" class="csl-entry">

R Core Team. (2018). *R: A language and environment for statistical
computing*. Retrieved from <https://www.R-project.org/>

</div>

<div id="ref-forLavaan" class="csl-entry">

Rosseel, Y. (2012). <span class="nocase">lavaan</span>: An R package for
structural equation modeling. *Journal of Statistical Software*,
*48*(2), 1–36. <https://doi.org/10.18637/jss.v048.i02>

</div>

<div id="ref-van2012checklist" class="csl-entry">

Van de Schoot, R., Lugtig, P., & Hox, J. (2012). A checklist for testing
measurement invariance. *European Journal of Developmental Psychology*,
*9*(4), 486–492. <https://doi.org/10.1080/17405629.2012.686740>

</div>

</div>
