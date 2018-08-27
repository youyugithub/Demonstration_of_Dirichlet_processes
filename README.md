# Demonstration_of_Dirichlet_processes
Demonstration of Dirichlet processes

###

```
########################################
## demonstration of Dirichlet process ##
########################################

## Let N(2,4) be the generic distribution
## a draw from DP(22,N(2,4)) is a distribution, (a cdf/pdf)
## To sample from the distribution we define weights by simulating from beta distribution
## 100 draws: gray, mean: black

plot(c(-4,8),c(0,1),"n")
for(ll in 1:100){
  random_normal<-rnorm(1000,2,2)
  random_beta<-rbeta(1000,1,22)
  weights<-random_beta*c(1,cumprod(1-random_beta)[-1000])
  
  idx<-order(random_normal)
  sfun<-stepfun(random_normal[idx],c(0,cumsum(weights[idx])))
  plot(sfun,col="gray",add=TRUE)
}
tempx<-seq(-4,8,0.01)
lines(tempx,pnorm(tempx,2,2),"l")
```


```
##########################
## sample from marginal ##
##########################

## Method 1

# Let pi be DP(22,N(2,4))
# sample F~pi
# then draw X1,...,Xn from F
# Marginal means F|pi


## Method 2

# 
#
#

###########################
## sample from posterior ##
###########################

## pi|X1,...,Xn


```
