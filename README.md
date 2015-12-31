## The `pRolocdata` `hyperLOPIT` data, as csv files

This data originates from the Bioconductor
[`pRolocdata`](http://bioconductor.org/packages/release/data/experiment/html/pRolocdata.html)
package. It is a recent spatial proteomics dataset, formatted and
analysed using the
[`pRoloc`](http://bioconductor.org/packages/release/bioc/html/pRoloc.html)
software.

#### Installation

To install these software:

```r
source("https://bioconductor.org/biocLite.R")
biocLite("pRoloc")
biocLite("pRolocdata")
```

#### Accessing the data


```r
library("pRolocdata")
```

```
## Loading required package: MSnbase
## Loading required package: methods
## Loading required package: BiocGenerics
## Loading required package: parallel
## 
## Attaching package: 'BiocGenerics'
## 
## The following objects are masked from 'package:parallel':
## 
##     clusterApply, clusterApplyLB, clusterCall, clusterEvalQ,
##     clusterExport, clusterMap, parApply, parCapply, parLapply,
##     parLapplyLB, parRapply, parSapply, parSapplyLB
## 
## The following objects are masked from 'package:stats':
## 
##     IQR, mad, xtabs
## 
## The following objects are masked from 'package:base':
## 
##     anyDuplicated, append, as.data.frame, as.vector, cbind,
##     colnames, do.call, duplicated, eval, evalq, Filter, Find, get,
##     grep, grepl, intersect, is.unsorted, lapply, lengths, Map,
##     mapply, match, mget, order, paste, pmax, pmax.int, pmin,
##     pmin.int, Position, rank, rbind, Reduce, rownames, sapply,
##     setdiff, sort, table, tapply, union, unique, unlist, unsplit
## 
## Loading required package: Biobase
## Welcome to Bioconductor
## 
##     Vignettes contain introductory material; view with
##     'browseVignettes()'. To cite Bioconductor, see
##     'citation("Biobase")', and for packages 'citation("pkgname")'.
## 
## Loading required package: mzR
## Loading required package: Rcpp
## Loading required package: BiocParallel
## Loading required package: ProtGenerics
```

```
## Warning: replacing previous import by 'ggplot2::Position' when loading
## 'MSnbase'
```

```
## Warning: replacing previous import by 'ggplot2::unit' when loading
## 'MSnbase'
```

```
## Warning: replacing previous import by 'ggplot2::arrow' when loading
## 'MSnbase'
```

```
## 
## This is MSnbase version 1.19.7 
##   Read '?MSnbase' and references therein for information
##   about the package and how to get started.
## 
## 
## Attaching package: 'MSnbase'
## 
## The following object is masked from 'package:stats':
## 
##     smooth
## 
## 
## This is pRolocdata version 1.9.1.
## Use 'pRolocdata()' to list available data sets.
```

```r
data(hyperLOPIT2015)
class(hyperLOPIT2015)
```

```
## [1] "MSnSet"
## attr(,"package")
## [1] "MSnbase"
```

```r
hyperLOPIT2015
```

```
## MSnSet (storageMode: lockedEnvironment)
## assayData: 5032 features, 20 samples 
##   element names: exprs 
## protocolData: none
## phenoData
##   sampleNames: X126.rep1 X127N.rep1 ... X131.rep2 (20 total)
##   varLabels: Replicate TMT.Reagent ... Fraction.No (6 total)
##   varMetadata: labelDescription
## featureData
##   featureNames: Q9JHU4 Q9QXS1-3 ... Q9Z2R6 (5032 total)
##   fvarLabels: entry.name protein.description ...
##     cell.surface.proteins (24 total)
##   fvarMetadata: labelDescription
## experimentData: use 'experimentData(object)'
## Annotation:  
## - - - Processing information - - -
## Loaded on Thu Nov  5 18:07:10 2015. 
## Normalised to sum of intensities. 
##  MSnbase version: 1.19.3
```

This `MSnSet` class is specific to quantitative proteomics data, but
that canb be summerised by 2 or 3 tabular data structures (from an R
point of view, 1 [expression `matrix`](./exprs.csv) and 1 or 2
`data.frames` describing the [features](./fdata/csv) and
[samples](./pdata.csv)), which are accessible individually with


```r
exprs(hyperLOPIT2015)[1:6, 1:3] ## a matrix
```

```
##          X126.rep1 X127N.rep1 X127C.rep1
## Q9JHU4       0.028      0.034      0.024
## Q9QXS1-3     0.039      0.134      0.095
## Q9ERU9       0.021      0.013      0.014
## P26039       0.120      0.255      0.148
## Q8BTM8       0.055      0.139      0.078
## A2ARV4       0.000      0.085      0.223
```


```r
fData(LOPIT2015)[1:6, 1:3] ## a data.frame
```

```
## Error in fData(LOPIT2015): error in evaluating the argument 'object' in selecting a method for function 'fData': Error: object 'LOPIT2015' not found
```


```r
pData(hyperLOPIT2015)[1:6, 1:3] ## second data.frame
```

```
##            Replicate TMT.Reagent Acquisiton.Method
## X126.rep1          1        X126               MS3
## X127N.rep1         1       X127N               MS3
## X127C.rep1         1       X127C               MS3
## X128N.rep1         1       X128N               MS3
## X128C.rep1         1       X128C               MS3
## X129N.rep1         1       X129N               MS3
```

#### Producing the csv files


```r
write.csv(exprs(hyperLOPIT2015), file = "exprs.csv")
write.csv(fData(hyperLOPIT2015), file = "fdata.csv")
write.csv(pData(hyperLOPIT2015), file = "pdata.csv")
```
