Portfolio Modeling
================

### Loading all required libraries

``` r
library(mosaic)
```

    ## Loading required package: dplyr

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

    ## Loading required package: lattice

    ## Loading required package: ggformula

    ## Loading required package: ggplot2

    ## Loading required package: ggstance

    ## 
    ## Attaching package: 'ggstance'

    ## The following objects are masked from 'package:ggplot2':
    ## 
    ##     geom_errorbarh, GeomErrorbarh

    ## 
    ## New to ggformula?  Try the tutorials: 
    ##  learnr::run_tutorial("introduction", package = "ggformula")
    ##  learnr::run_tutorial("refining", package = "ggformula")

    ## Loading required package: mosaicData

    ## Loading required package: Matrix

    ## Registered S3 method overwritten by 'mosaic':
    ##   method                           from   
    ##   fortify.SpatialPolygonsDataFrame ggplot2

    ## 
    ## The 'mosaic' package masks several functions from core packages in order to add 
    ## additional features.  The original behavior of these functions should not be affected by this.
    ## 
    ## Note: If you use the Matrix package, be sure to load it BEFORE loading mosaic.

    ## 
    ## Attaching package: 'mosaic'

    ## The following object is masked from 'package:Matrix':
    ## 
    ##     mean

    ## The following object is masked from 'package:ggplot2':
    ## 
    ##     stat

    ## The following objects are masked from 'package:dplyr':
    ## 
    ##     count, do, tally

    ## The following objects are masked from 'package:stats':
    ## 
    ##     binom.test, cor, cor.test, cov, fivenum, IQR, median,
    ##     prop.test, quantile, sd, t.test, var

    ## The following objects are masked from 'package:base':
    ## 
    ##     max, mean, min, prod, range, sample, sum

``` r
library(quantmod)
```

    ## Loading required package: xts

    ## Loading required package: zoo

    ## 
    ## Attaching package: 'zoo'

    ## The following objects are masked from 'package:base':
    ## 
    ##     as.Date, as.Date.numeric

    ## Registered S3 method overwritten by 'xts':
    ##   method     from
    ##   as.zoo.xts zoo

    ## 
    ## Attaching package: 'xts'

    ## The following objects are masked from 'package:dplyr':
    ## 
    ##     first, last

    ## Loading required package: TTR

    ## Registered S3 method overwritten by 'quantmod':
    ##   method            from
    ##   as.zoo.data.frame zoo

    ## Version 0.4-0 included new data defaults. See ?getSymbols.

``` r
library(foreach)
```

### 1\. Importing top 3 oil & gas ETF’s - last 5 yrs data - Portfolio 1

### 2\. Importing top 3 Building\&Construction & top 2 Commodities ETF’s - last 5 yrs data - Portfolio 2

### 3\. Import top 7 Diversified Portfolio ETF’s - last 5 yrs data - Portfolio 3

### Creating an all return matrix for all the 3 portfolios

``` r
# Import top 3 oil & gas ETF's - last 5 yrs data
etf1 = c("USO", "UNG", "DBO")

# Import top 3 Building&Construction & top 2 Commodities ETF's - last 5 yrs data
etf2 = c("ITB", "XHB", "PKB","PDBC","DBC")

# Import top 7 Diversified Portfolio ETF's - last 5 yrs data
etf3 = c("AOR", "AOM", "AOA", "MDIV", "AOK", "IYLD", "GAL")

#Getting data for past 5 years
getSymbols(etf1, from = "2014-08-01")
```

    ## 'getSymbols' currently uses auto.assign=TRUE by default, but will
    ## use auto.assign=FALSE in 0.5-0. You will still be able to use
    ## 'loadSymbols' to automatically load data. getOption("getSymbols.env")
    ## and getOption("getSymbols.auto.assign") will still be checked for
    ## alternate defaults.
    ## 
    ## This message is shown once per session and may be disabled by setting 
    ## options("getSymbols.warning4.0"=FALSE). See ?getSymbols for details.

    ## [1] "USO" "UNG" "DBO"

``` r
getSymbols(etf2, from = "2014-08-01")
```

    ## [1] "ITB"  "XHB"  "PKB"  "PDBC" "DBC"

``` r
getSymbols(etf3, from = "2014-08-01")
```

    ## pausing 1 second between requests for more than 5 symbols

    ## pausing 1 second between requests for more than 5 symbols
    ## pausing 1 second between requests for more than 5 symbols

    ## [1] "AOR"  "AOM"  "AOA"  "MDIV" "AOK"  "IYLD" "GAL"

``` r
for(ticker in etf1) {
    expr = paste0(ticker, "a = adjustOHLC(", ticker, ")")
    eval(parse(text=expr))
}

all_returns1 = cbind(   ClCl(USOa),
                                ClCl(UNGa),
                                ClCl(DBOa))

# Creating all return matrix for Portfolio 1
all_returns1 = as.matrix(na.omit(all_returns1))
summary(all_returns1)
```

    ##    ClCl.USOa            ClCl.UNGa           ClCl.DBOa         
    ##  Min.   :-0.0831541   Min.   :-0.756614   Min.   :-0.0870556  
    ##  1st Qu.:-0.0124836   1st Qu.:-0.014726   1st Qu.:-0.0112782  
    ##  Median : 0.0000000   Median :-0.001327   Median : 0.0009008  
    ##  Mean   :-0.0006718   Mean   :-0.001417   Mean   :-0.0006739  
    ##  3rd Qu.: 0.0120148   3rd Qu.: 0.012869   3rd Qu.: 0.0104275  
    ##  Max.   : 0.0924041   Max.   : 0.188993   Max.   : 0.0890411

``` r
for(ticker in etf2) {
    expr = paste0(ticker, "a = adjustOHLC(", ticker, ")")
    eval(parse(text=expr))
}

all_returns2 = cbind(   ClCl(ITBa),
                                ClCl(XHBa),
                                ClCl(PKBa),
                                ClCl(PDBCa),
                                ClCl(DBCa))

# Creating all return matrix for Portfolio 2
all_returns2 = as.matrix(na.omit(all_returns2))
summary(all_returns2)
```

    ##    ClCl.ITBa            ClCl.XHBa            ClCl.PKBa         
    ##  Min.   :-0.0501931   Min.   :-0.0465761   Min.   :-0.0478842  
    ##  1st Qu.:-0.0069519   1st Qu.:-0.0063242   1st Qu.:-0.0065874  
    ##  Median : 0.0007842   Median : 0.0005671   Median : 0.0012653  
    ##  Mean   : 0.0004906   Mean   : 0.0003011   Mean   : 0.0003623  
    ##  3rd Qu.: 0.0084572   3rd Qu.: 0.0073858   3rd Qu.: 0.0074987  
    ##  Max.   : 0.0464876   Max.   : 0.0503418   Max.   : 0.0482122  
    ##    ClCl.PDBCa           ClCl.DBCa         
    ##  Min.   :-0.0493328   Min.   :-0.0457944  
    ##  1st Qu.:-0.0055934   1st Qu.:-0.0059587  
    ##  Median : 0.0000000   Median : 0.0000000  
    ##  Mean   :-0.0002628   Mean   :-0.0002681  
    ##  3rd Qu.: 0.0057211   3rd Qu.: 0.0055285  
    ##  Max.   : 0.0476750   Max.   : 0.0360861

``` r
for(ticker in etf3) {
    expr = paste0(ticker, "a = adjustOHLC(", ticker, ")")
    eval(parse(text=expr))
}

all_returns3 = cbind(   ClCl(AORa),
                                ClCl(AOMa),
                                ClCl(AOAa),
                                ClCl(MDIVa),
                                ClCl(AOKa),
                                ClCl(IYLDa),
                                ClCl(GALa))
# Creating all return matrix for Portfolio 3
all_returns3 = as.matrix(na.omit(all_returns3))
summary(all_returns3)
```

    ##    ClCl.AORa            ClCl.AOMa            ClCl.AOAa         
    ##  Min.   :-0.0314434   Min.   :-0.0200057   Min.   :-0.0437299  
    ##  1st Qu.:-0.0022693   1st Qu.:-0.0019460   1st Qu.:-0.0028090  
    ##  Median : 0.0002522   Median : 0.0002747   Median : 0.0005553  
    ##  Mean   : 0.0002241   Mean   : 0.0001845   Mean   : 0.0002546  
    ##  3rd Qu.: 0.0030203   3rd Qu.: 0.0024090   3rd Qu.: 0.0039476  
    ##  Max.   : 0.0205751   Max.   : 0.0158020   Max.   : 0.0284864  
    ##    ClCl.MDIVa           ClCl.AOKa            ClCl.IYLDa        
    ##  Min.   :-0.0307452   Min.   :-0.0143162   Min.   :-0.0173639  
    ##  1st Qu.:-0.0027070   1st Qu.:-0.0014501   1st Qu.:-0.0018889  
    ##  Median : 0.0000000   Median : 0.0002993   Median : 0.0003998  
    ##  Mean   : 0.0001122   Mean   : 0.0001645   Mean   : 0.0001518  
    ##  3rd Qu.: 0.0033144   3rd Qu.: 0.0018019   3rd Qu.: 0.0024077  
    ##  Max.   : 0.0326959   Max.   : 0.0100794   Max.   : 0.0130293  
    ##    ClCl.GALa         
    ##  Min.   :-0.0313433  
    ##  1st Qu.:-0.0026267  
    ##  Median : 0.0002949  
    ##  Mean   : 0.0001694  
    ##  3rd Qu.: 0.0033749  
    ##  Max.   : 0.0209423

### Calculating VAR for Portfolio 1

#### From the summary of returns, it seems ETF “UNG” has a neagtive mean and median return. Hence assigning weights as (0.4,0.2,0.4) to have lesser weights on “UNG”

``` r
# Monte Carlo Simulation to Calculate VAR for Portfolio 1
initial_wealth = 100000
# 5000 simulations
sim1 = foreach(i=1:5000, .combine='rbind') %do% {
    total_wealth = initial_wealth
    weights = c(0.4, 0.2, 0.4)
    holdings = weights * total_wealth
    n_days = 20
    wealthtracker1 = rep(0, n_days)
    for(today in 1:n_days) {
        return.today = resample(all_returns1, 1, orig.ids=FALSE)
        holdings = holdings + holdings*return.today
        total_wealth = sum(holdings)
        wealthtracker1[today] = total_wealth
        holdings = weights * total_wealth #re-balancing each day
        
    }
    ((wealthtracker1[20]-initial_wealth)*100)/initial_wealth
    
}
sorted_sim_1=sort(sim1)
VAR1=sorted_sim_1[250]
VAR1
```

    ## [1] -14.33251

### Calculating VAR for Portfolio 2

#### From the summary of returns, it seems ETF “PDBC” and “DBC” hvae neagtive mean returns. Hence assigning the weights accordingly as (0.2,0.3,0.3,0.1,0.1) to have lesser weights on “PDBC” and “DBC”

``` r
# Monte Carlo Simulation to Calculate VAR for Portfolio 2
initial_wealth = 100000
#5000 Simulations
sim2 = foreach(i=1:5000, .combine='rbind') %do% {
    total_wealth = initial_wealth
    weights = c(0.2, 0.3, 0.3, 0.1, 0.1)
    holdings = weights * total_wealth
    n_days = 20 #20 trading day
    wealthtracker2 = rep(0, n_days)
    for(today in 1:n_days) {
        return.today = resample(all_returns2, 1, orig.ids=FALSE)
        holdings = holdings + holdings*return.today
        total_wealth = sum(holdings)
        wealthtracker2[today] = total_wealth
        holdings = weights * total_wealth #re-balancing each day
        
    }
    ((wealthtracker2[20]-initial_wealth)*100)/initial_wealth
    
}
sorted_sim_2=sort(sim2)
VAR2=sorted_sim_2[250]
VAR2
```

    ## [1] -6.81134

### Calculating VAR for Portfolio 3

#### From the summary of returns, all ETF’s have comparable returns. Hence assigning almost equal weights to them.

``` r
# Monte Carlo Simulation to Calculate VAR for Portfolio 3
initial_wealth = 100000
#5000 simulations
sim3 = foreach(i=1:5000, .combine='rbind') %do% {
    total_wealth = initial_wealth
    weights = c(0.15, 0.15, 0.15, 0.15,0.15,0.15,0.1)
    holdings = weights * total_wealth
    n_days = 20
    wealthtracker3 = rep(0, n_days)
    for(today in 1:n_days) {
        return.today = resample(all_returns3, 1, orig.ids=FALSE)
        holdings = holdings + holdings*return.today
        total_wealth = sum(holdings)
        wealthtracker3[today] = total_wealth
        holdings = weights * total_wealth #re-balancing each day
        
    }
    ((wealthtracker3[20]-initial_wealth)*100)/initial_wealth
    
}
sorted_sim_3=sort(sim3)
VAR3=sorted_sim_3[250]
VAR3
```

    ## [1] -2.898298

``` r
print("Final Report")
```

    ## [1] "Final Report"

``` r
cat("\nPortfolio 1 containing top 3 oil & gas ETF's - ",etf1, "\n4-week (20 trading day) VAR at the 5% level = ", VAR1,"%")
```

    ## 
    ## Portfolio 1 containing top 3 oil & gas ETF's -  USO UNG DBO 
    ## 4-week (20 trading day) VAR at the 5% level =  -14.33251 %

``` r
cat("\n\nPortfolio 2 containing top 3 Building&Construction & top 2 Commodities ETF's - ",etf2, "\n4-week (20 trading day) VAR at the 5% level = ", VAR2,"%")
```

    ## 
    ## 
    ## Portfolio 2 containing top 3 Building&Construction & top 2 Commodities ETF's -  ITB XHB PKB PDBC DBC 
    ## 4-week (20 trading day) VAR at the 5% level =  -6.81134 %

``` r
cat("\n\nPortfolio 3 containing top 7 Diversified Portfolio ETF's - ",etf3, "\n4-week (20 trading day) VAR at the 5% level = ", VAR3,"%")
```

    ## 
    ## 
    ## Portfolio 3 containing top 7 Diversified Portfolio ETF's -  AOR AOM AOA MDIV AOK IYLD GAL 
    ## 4-week (20 trading day) VAR at the 5% level =  -2.898298 %

### **Final Report**

| Portfolio | ETF List                                          | ETF Category                                     | 4-week VAR |
| --------- | ------------------------------------------------- | ------------------------------------------------ | ---------- |
| 1         | “USO”, “UNG”, “DBO”                               | Top 3 oil & gas                                  | \-14.64 %  |
| 2         | “ITB”, “XHB”, “PKB”,“PDBC”,“DBC”                  | Top 3 Building\&Construction & top 2 Commodities | \-6.68 %   |
| 3         | “AOR”, “AOM”, “AOA”, “MDIV”, “AOK”, “IYLD”, “GAL” | Top 7 Diversified Portfolios                     | \-2.79 %   |
