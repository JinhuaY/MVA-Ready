
[<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/banner.png" alt="Visit QuantNet">](http://quantlet.de/index.php?p=info)

## [<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/qloqo.png" alt="Visit QuantNet">](http://quantlet.de/) **MVAdrafthousing** [<img src="https://github.com/QuantLet/Styleguide-and-Validation-procedure/blob/master/pictures/QN2.png" width="60" alt="Visit QuantNet 2.0">](http://quantlet.de/d3/ia)

```yaml

Name of QuantLet : MVAdrafthousing

Published in : Applied Multivariate Statistical Analysis

Description : Plots the scatterplot matrix for Boston housing data.

Keywords : financial, data visualization, boxplot, scatterplot, plot, graphical representation

See also : MVAdrafthousingt, MVApcphousing

Author : Vladimir Georgescu, Jorge Patron, Song Song, Julia Wandke, Awdesch Melzer

Submitted : Tue, September 09 2014 by Awdesch Melzer

Datafile : bostonh.dat

```

![Picture1](MVAdrafthousing.png)


```r

# clear all variables
rm(list = ls(all = TRUE))
graphics.off()

# load data
data = read.table("bostonh.dat")

K    = as.numeric(data[, 14] > median(data[, 14])) + 1
x    = cbind(data[, -(6:13)], K)
z    = data.frame(x)
z1   = subset(z, z$K == 1)
z2   = subset(z, z$K == 2)
m1   = apply(z1, 2, mean)
m2   = apply(z2, 2, mean)
i    = 0
op   = par(mfrow = c(6, 6), cex = 0.15)

while (i < 6) {
    i = i + 1
    j = 0
    while (j < 6) {
        j = j + 1
        
        if (i == j) {
            boxplot(x[, i] ~ K, at = 1:2, axes = FALSE, lwd = 0.7)
            lines(c(0.6, 1.4), c(m1[i], m1[i]), lty = "dotted", lwd = 1.2, col = "red3")
            lines(c(1.6, 2.4), c(m1[i], m1[i]), lty = "dotted", lwd = 1.2, col = "red3")
        }
        
        if (i > j) {
            yy = cbind(x[, j], x[, i], K)
            plot(yy[, -3], col = as.numeric(K), xlab = "", ylab = "", cex = 4, axes = FALSE)
        }
        
        if (i < j) {
            plot(i, type = "n", axes = FALSE, xlab = "", ylab = "", main = "")
        }
    }
}
title(main = list("Scatterplot matrix for Boston Housing", cex = 8), line = -16, 
    outer = TRUE) 

```
