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
suppressPackageStartupMessages(library("pRolocdata"))
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
that can be summerised by 2 or 3 tabular data structures (from an R
point of view, 1 [expression `matrix`](./exprs.csv) and 1 or 2
`data.frames` describing the [features](./fdata.csv) and
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
fData(hyperLOPIT2015)[1:6, 1:3] ## a data.frame
```

```
##           entry.name
## Q9JHU4   DYHC1_MOUSE
## Q9QXS1-3  PLEC_MOUSE
## Q9ERU9    RBP2_MOUSE
## P26039    TLN1_MOUSE
## Q8BTM8    FLNA_MOUSE
## A2ARV4    LRP2_MOUSE
##                                                                                                                         protein.description
## Q9JHU4                                              Cytoplasmic dynein 1 heavy chain 1 OS=Mus musculus GN=Dync1h1 PE=1 SV=2 - [DYHC1_MOUSE]
## Q9QXS1-3 Isoform PLEC-1 of Plectin OS=Mus musculus GN=Plec - [PLEC_MOUSE]|Isoform PLEC-1A of Plectin OS=Mus musculus GN=Plec - [PLEC_MOUSE]
## Q9ERU9                                                     E3 SUMO-protein ligase RanBP2 OS=Mus musculus GN=Ranbp2 PE=1 SV=2 - [RBP2_MOUSE]
## P26039                                                                             Talin-1 OS=Mus musculus GN=Tln1 PE=1 SV=2 - [TLN1_MOUSE]
## Q8BTM8                                                                           Filamin-A OS=Mus musculus GN=Flna PE=1 SV=5 - [FLNA_MOUSE]
## A2ARV4                                  Low-density lipoprotein receptor-related protein 2 OS=Mus musculus GN=Lrp2 PE=1 SV=1 - [LRP2_MOUSE]
##          peptides.rep1
## Q9JHU4             175
## Q9QXS1-3           123
## Q9ERU9             101
## P26039             101
## Q8BTM8              95
## A2ARV4              85
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

#### Session information


```r
sessionInfo()
```

```
## R Under development (unstable) (2015-12-17 r69781)
## Platform: x86_64-pc-linux-gnu (64-bit)
## Running under: Ubuntu 14.04.3 LTS
## 
## locale:
##  [1] LC_CTYPE=en_GB.UTF-8       LC_NUMERIC=C              
##  [3] LC_TIME=en_GB.UTF-8        LC_COLLATE=en_GB.UTF-8    
##  [5] LC_MONETARY=en_GB.UTF-8    LC_MESSAGES=en_GB.UTF-8   
##  [7] LC_PAPER=en_GB.UTF-8       LC_NAME=C                 
##  [9] LC_ADDRESS=C               LC_TELEPHONE=C            
## [11] LC_MEASUREMENT=en_GB.UTF-8 LC_IDENTIFICATION=C       
## 
## attached base packages:
## [1] parallel  methods   stats     graphics  grDevices utils     datasets 
## [8] base     
## 
## other attached packages:
## [1] pRolocdata_1.9.1    MSnbase_1.19.7      ProtGenerics_1.3.3 
## [4] BiocParallel_1.5.11 mzR_2.5.2           Rcpp_0.12.2        
## [7] Biobase_2.31.3      BiocGenerics_0.17.2
## 
## loaded via a namespace (and not attached):
##  [1] knitr_1.11            magrittr_1.5          IRanges_2.5.18       
##  [4] zlibbioc_1.17.0       doParallel_1.0.10     munsell_0.4.2        
##  [7] colorspace_1.2-6      impute_1.45.0         lattice_0.20-33      
## [10] foreach_1.4.3         stringr_1.0.0         plyr_1.8.3           
## [13] tools_3.3.0           mzID_1.9.0            grid_3.3.0           
## [16] gtable_0.1.2          affy_1.49.0           iterators_1.0.8      
## [19] digest_0.6.8          preprocessCore_1.33.0 affyio_1.41.0        
## [22] reshape2_1.4.1        ggplot2_2.0.0         formatR_1.2.1        
## [25] S4Vectors_0.9.15      codetools_0.2-14      MALDIquant_1.14      
## [28] evaluate_0.8          limma_3.27.6          stringi_1.0-1        
## [31] BiocInstaller_1.21.2  pcaMethods_1.61.0     scales_0.3.0         
## [34] XML_3.98-1.3          stats4_3.3.0          vsn_3.39.0
```
