Introduction to Machine Learning
================
Claire Chapman
10/24/2021

# Clustering methods

## kmeans()

### First lets make up some data to cluster

``` r
tmp <- c(rnorm(30, 3), rnorm(30, -3))
tmp
```

    ##  [1]  2.8002332  3.9701052  3.3369556  3.7836700  3.3211626  1.7456154
    ##  [7]  1.5760392  0.5851125  1.5591935  4.5044798  4.2942720  5.1687247
    ## [13]  2.0413453  0.4290256  2.2369067  2.3911038  3.9713766  2.6288403
    ## [19]  2.8916769  3.3460085  3.8164024  5.2060766  3.7882068  2.0240792
    ## [25]  3.8821791  1.2006701  2.5168669  3.1301394  2.8019074  2.8252322
    ## [31] -3.0526633 -1.4349289 -4.2428629 -2.9537627 -2.9292198 -3.0439476
    ## [37] -4.9264042 -2.4193927 -2.8933739 -3.2491997 -3.6286516 -2.2070870
    ## [43] -2.9886541 -3.8266876 -1.9808742 -2.6341570 -4.1491752 -3.3405212
    ## [49] -1.9008502 -1.9911995 -4.2491301 -3.3314143 -3.5268212 -3.2108528
    ## [55] -3.3877758 -4.1314835 -3.5134551 -3.4035565 -3.4118993 -2.5473170

``` r
data <- cbind(x = tmp, y = rev(tmp))
data
```

    ##                x          y
    ##  [1,]  2.8002332 -2.5473170
    ##  [2,]  3.9701052 -3.4118993
    ##  [3,]  3.3369556 -3.4035565
    ##  [4,]  3.7836700 -3.5134551
    ##  [5,]  3.3211626 -4.1314835
    ##  [6,]  1.7456154 -3.3877758
    ##  [7,]  1.5760392 -3.2108528
    ##  [8,]  0.5851125 -3.5268212
    ##  [9,]  1.5591935 -3.3314143
    ## [10,]  4.5044798 -4.2491301
    ## [11,]  4.2942720 -1.9911995
    ## [12,]  5.1687247 -1.9008502
    ## [13,]  2.0413453 -3.3405212
    ## [14,]  0.4290256 -4.1491752
    ## [15,]  2.2369067 -2.6341570
    ## [16,]  2.3911038 -1.9808742
    ## [17,]  3.9713766 -3.8266876
    ## [18,]  2.6288403 -2.9886541
    ## [19,]  2.8916769 -2.2070870
    ## [20,]  3.3460085 -3.6286516
    ## [21,]  3.8164024 -3.2491997
    ## [22,]  5.2060766 -2.8933739
    ## [23,]  3.7882068 -2.4193927
    ## [24,]  2.0240792 -4.9264042
    ## [25,]  3.8821791 -3.0439476
    ## [26,]  1.2006701 -2.9292198
    ## [27,]  2.5168669 -2.9537627
    ## [28,]  3.1301394 -4.2428629
    ## [29,]  2.8019074 -1.4349289
    ## [30,]  2.8252322 -3.0526633
    ## [31,] -3.0526633  2.8252322
    ## [32,] -1.4349289  2.8019074
    ## [33,] -4.2428629  3.1301394
    ## [34,] -2.9537627  2.5168669
    ## [35,] -2.9292198  1.2006701
    ## [36,] -3.0439476  3.8821791
    ## [37,] -4.9264042  2.0240792
    ## [38,] -2.4193927  3.7882068
    ## [39,] -2.8933739  5.2060766
    ## [40,] -3.2491997  3.8164024
    ## [41,] -3.6286516  3.3460085
    ## [42,] -2.2070870  2.8916769
    ## [43,] -2.9886541  2.6288403
    ## [44,] -3.8266876  3.9713766
    ## [45,] -1.9808742  2.3911038
    ## [46,] -2.6341570  2.2369067
    ## [47,] -4.1491752  0.4290256
    ## [48,] -3.3405212  2.0413453
    ## [49,] -1.9008502  5.1687247
    ## [50,] -1.9911995  4.2942720
    ## [51,] -4.2491301  4.5044798
    ## [52,] -3.3314143  1.5591935
    ## [53,] -3.5268212  0.5851125
    ## [54,] -3.2108528  1.5760392
    ## [55,] -3.3877758  1.7456154
    ## [56,] -4.1314835  3.3211626
    ## [57,] -3.5134551  3.7836700
    ## [58,] -3.4035565  3.3369556
    ## [59,] -3.4118993  3.9701052
    ## [60,] -2.5473170  2.8002332

Using just our eyes, we can assume that we should get two clusters

``` r
plot(data)
```

![](class08_files/figure-gfm/unnamed-chunk-3-1.png)<!-- --> \#\#\# Run
kmeans() The argument **k** tells how many clusters you are asking for.
The argument **nstarts** tells how many iterations

``` r
km <- kmeans(data, centers = 2, nstart = 20)
km
```

    ## K-means clustering with 2 clusters of sizes 30, 30
    ## 
    ## Cluster means:
    ##           x         y
    ## 1  2.925787 -3.150244
    ## 2 -3.150244  2.925787
    ## 
    ## Clustering vector:
    ##  [1] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2
    ## [39] 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2
    ## 
    ## Within cluster sum of squares by cluster:
    ## [1] 61.15161 61.15161
    ##  (between_SS / total_SS =  90.1 %)
    ## 
    ## Available components:
    ## 
    ## [1] "cluster"      "centers"      "totss"        "withinss"     "tot.withinss"
    ## [6] "betweenss"    "size"         "iter"         "ifault"

> Q. How many points are in each cluster?

``` r
km$size
```

    ## [1] 30 30

**Thirty points in each cluster**

> Q. What “component” of your result object details cluster
> assignment/membership?

``` r
km$cluster
```

    ##  [1] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2
    ## [39] 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2

> Q. What “component” of your result object details cluster center?

``` r
km$centers
```

    ##           x         y
    ## 1  2.925787 -3.150244
    ## 2 -3.150244  2.925787

> Q. Plot x colored by the kmeans cluster assignment and add cluster
> centers as blue points

``` r
plot(data, col = km$cluster)
points(km$centers, col = "blue", pch = 15)
```

![](class08_files/figure-gfm/unnamed-chunk-8-1.png)<!-- -->

## Hierarchical Clustering, **hclust()**

A little bit more work required than in kmeans: can’t just use x, need a
distance matrix using function **dist()**

``` r
hc <- hclust(dist(data))
hc
```

    ## 
    ## Call:
    ## hclust(d = dist(data))
    ## 
    ## Cluster method   : complete 
    ## Distance         : euclidean 
    ## Number of objects: 60

This printout wasn’t very helpful, use a plot. Hclust() has its own
useful plot method

``` r
plot(hc)
abline(h = 7, col = "red")
```

![](class08_files/figure-gfm/unnamed-chunk-10-1.png)<!-- --> To find out
membership vector, we need to “cut” the tree. Use **cutree()** function
and tell it the height to cut at

``` r
cutree(hc, h = 7)
```

    ##  [1] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2
    ## [39] 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2

Can also use **cutree()** and state the number of k clusters we want

``` r
grps <- cutree(hc, k = 2)
grps
```

    ##  [1] 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2
    ## [39] 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2 2

``` r
plot(data, col = grps)
```

![](class08_files/figure-gfm/unnamed-chunk-13-1.png)<!-- -->

# Principal Component Analysis (PCA)

A useful analysis method when you have lots of dimensions in your data

## PCA of UK food data

### Read in data

``` r
url <- "https://tinyurl.com/UK-foods"
x <- read.csv(url)
```

> Q1. How many rows and columns are in your new data frame named x? What
> R functions could you use to answer this questions?

``` r
dim(x)
```

    ## [1] 17  5

Why aren’t there only 4 columns (one for each country)?

``` r
head(x)
```

    ##                X England Wales Scotland N.Ireland
    ## 1         Cheese     105   103      103        66
    ## 2  Carcass_meat      245   227      242       267
    ## 3    Other_meat      685   803      750       586
    ## 4           Fish     147   160      122        93
    ## 5 Fats_and_oils      193   235      184       209
    ## 6         Sugars     156   175      147       139

Row names were being assigned to the first column, incorrectly

### Fix data

``` r
rownames(x) <- x[,1]
x <- x[,-1]
head(x)
```

    ##                England Wales Scotland N.Ireland
    ## Cheese             105   103      103        66
    ## Carcass_meat       245   227      242       267
    ## Other_meat         685   803      750       586
    ## Fish               147   160      122        93
    ## Fats_and_oils      193   235      184       209
    ## Sugars             156   175      147       139

The better way to fix this is upon import

``` r
x <- read.csv(url, row.names = 1)
dim(x)
```

    ## [1] 17  4

> Q2. Which approach to solving the ‘row-names problem’ mentioned above
> do you prefer and why? Is one approach more robust than another under
> certain circumstances?

The second method is much better because it makes the correct change,
permanently, to the dataset whereas the first method will keep taking
away the first column.

### Plotting the data

``` r
barplot(as.matrix(x), beside = T, col = rainbow(nrow(x)))
```

![](class08_files/figure-gfm/unnamed-chunk-19-1.png)<!-- --> &gt; Q3:
Changing what optional argument in the above barplot() function results
in the following plot?

The argument “beside” determines if values are stacked on top of each
other or beside each other. Default is beside = F and values are stacked

> Q5: Generating all pairwise plots may help somewhat. Can you make
> sense of the following code and resulting figure? What does it mean if
> a given point lies on the diagonal for a given plot?

``` r
mycols <- rainbow(nrow(x))
pairs(x, col=mycols, pch=16)
```

![](class08_files/figure-gfm/unnamed-chunk-20-1.png)<!-- --> This plot
compares all pairs of countries. Points on the diagonal show that tha
data is the same for the pair of countries. Points that are not on the
diagonal signify differences between the two countries being compared.

> Q6. What is the main differences between N. Ireland and the other
> countries of the UK in terms of this data-set?

The main difference between N. Ireland and the other countries is the
green data point that was consumed at a higher quantity in N.Ireland
than others. The results are still just qualitative though…

## PCA is here to help

Base R function **prcomp()** to find PCA First need to tranpose the
data, this function wants countries in rows and foods in columns

``` r
pca <- prcomp(t(x))
summary(pca)
```

    ## Importance of components:
    ##                             PC1      PC2      PC3       PC4
    ## Standard deviation     324.1502 212.7478 73.87622 4.189e-14
    ## Proportion of Variance   0.6744   0.2905  0.03503 0.000e+00
    ## Cumulative Proportion    0.6744   0.9650  1.00000 1.000e+00

``` r
plot(pca)
```

![](class08_files/figure-gfm/unnamed-chunk-22-1.png)<!-- -->

We want the **score plot** (aka PCA plot), the plot of PC1 vs. PC2 that
we often see

``` r
attributes(pca)
```

    ## $names
    ## [1] "sdev"     "rotation" "center"   "scale"    "x"       
    ## 
    ## $class
    ## [1] "prcomp"

We want pca$x component for this plot

``` r
plot(pca$x[,1:2])
text(pca$x[,1:2], labels = colnames(x))
```

![](class08_files/figure-gfm/unnamed-chunk-24-1.png)<!-- -->

### PCA “loadings”

Loadings tell us how much each variable contributes to each PC

``` r
par(mar = c(10, 3, 0.35, 0))
barplot(pca$rotation[,1], las = 2)
```

![](class08_files/figure-gfm/unnamed-chunk-25-1.png)<!-- --> \#\# One
more PCA for the day

``` r
url2 <- "https://tinyurl.com/expression-CSV"
rna.data <- read.csv(url2, row.names=1)
head(rna.data)
```

    ##        wt1 wt2  wt3  wt4 wt5 ko1 ko2 ko3 ko4 ko5
    ## gene1  439 458  408  429 420  90  88  86  90  93
    ## gene2  219 200  204  210 187 427 423 434 433 426
    ## gene3 1006 989 1030 1017 973 252 237 238 226 210
    ## gene4  783 792  829  856 760 849 856 835 885 894
    ## gene5  181 249  204  244 225 277 305 272 270 279
    ## gene6  460 502  491  491 493 612 594 577 618 638

> Q10 How many genes and samples are in the data set?

``` r
nrow(rna.data)
```

    ## [1] 100

100 genes

``` r
ncol(rna.data)
```

    ## [1] 10

``` r
colnames(rna.data)
```

    ##  [1] "wt1" "wt2" "wt3" "wt4" "wt5" "ko1" "ko2" "ko3" "ko4" "ko5"

10 samples

### PCA

The argument scale normalizes the ranges in observations

``` r
pca.rna <- prcomp(t(rna.data), scale = T)
summary(pca.rna)
```

    ## Importance of components:
    ##                           PC1    PC2     PC3     PC4     PC5     PC6     PC7
    ## Standard deviation     9.6237 1.5198 1.05787 1.05203 0.88062 0.82545 0.80111
    ## Proportion of Variance 0.9262 0.0231 0.01119 0.01107 0.00775 0.00681 0.00642
    ## Cumulative Proportion  0.9262 0.9493 0.96045 0.97152 0.97928 0.98609 0.99251
    ##                            PC8     PC9      PC10
    ## Standard deviation     0.62065 0.60342 3.348e-15
    ## Proportion of Variance 0.00385 0.00364 0.000e+00
    ## Cumulative Proportion  0.99636 1.00000 1.000e+00

``` r
plot(pca.rna)
```

![](class08_files/figure-gfm/unnamed-chunk-30-1.png)<!-- -->

``` r
plot(pca.rna$x[,1:2])
text(pca.rna$x[,1:2], labels = colnames(rna.data))
```

![](class08_files/figure-gfm/unnamed-chunk-31-1.png)<!-- -->

### Quick scree plot

``` r
plot(pca, main = "Quick scree plot")
```

![](class08_files/figure-gfm/unnamed-chunk-32-1.png)<!-- -->

### our own scree plots

Variance captured per PC

``` r
pca.var <- pca.rna$sdev^2
```

Percent variance is often more informative to look at

``` r
pca.var.per <- round(pca.var/sum(pca.var)*100, 1)
pca.var.per
```

    ##  [1] 92.6  2.3  1.1  1.1  0.8  0.7  0.6  0.4  0.4  0.0

``` r
barplot(pca.var.per, main="Scree Plot", 
        names.arg = paste0("PC", 1:10),
        xlab="Principal Component", ylab="Percent Variation")
```

![](class08_files/figure-gfm/unnamed-chunk-35-1.png)<!-- --> Adding
colors

``` r
colvec <- colnames(rna.data)
colvec[grep("wt", colvec)] <- "red"
colvec[grep("ko", colvec)] <- "blue"

plot(pca$x[,1], pca$x[,2], col=colvec, pch=16,
     xlab=paste0("PC1 (", pca.var.per[1], "%)"),
     ylab=paste0("PC2 (", pca.var.per[2], "%)"))

text(pca$x[,1], pca$x[,2], labels = colnames(rna.data), pos=c(rep(4,5), rep(2,5)))
```

![](class08_files/figure-gfm/unnamed-chunk-36-1.png)<!-- -->
