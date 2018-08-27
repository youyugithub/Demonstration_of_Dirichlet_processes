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

# Chinese restaurant process

xvec<-numeric(1000)
xvec[1]<-rnorm(1,2,2)
for(ii in 2:length(xvec)){
  if(runif(1)<(ii-1)/(ii-1+22)){
    xvec[ii]<-sample(xvec[1:(ii-1)],1)
  }else{
    xvec[ii]<-rnorm(1,2,2)
  }
}

hist(xvec)

idx<-order(xvec)
sfun<-stepfun(xvec[idx],seq(0,1,0.001))
plot(sfun,col="gray")
```

```
###########################
## sample from posterior ##
###########################

## pi|X1,...,Xn

# X1,...,Xn ~ F
# F ~ pi = DP(alpha,F0)
# ==> pi|X1,..,Xn ~ DP(alpha+n,Fhat)
#     where Fhat=n/(n+alpha)*Fn+alpha/(n+alpha)*F0
```
