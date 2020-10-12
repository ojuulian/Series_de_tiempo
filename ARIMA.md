---
title: "ARIMA"
output: html_document
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = TRUE)
```

## Simulación ARIMA 

Se desea simular un proceso $ARIMA(p=1,d=1,q=1)$ con $d=1$, al igual que proceso $ARIMA(p=1,d=1,q=1)$ con drift. Inicialmente vamos a simular el proceso
$$(1-B)(1-\phi B)X_{t}=(1+\theta B)Z_{t}$$
```{r}
Tlength=200
a0=3
a1=-0.5
tiempo=seq(1:Tlength)
xt=a1*tiempo
tendencia=a0+a1*tiempo
drift=a1*rep(1,Tlength)
###Si se desea simular un arima con drfit se debe asignar el valor de d=0 en arima.sim.
arimaej=arima.sim(list(order = c(1,1,1), ar = 0.7,ma=0.6), n = Tlength)
plot(arimaej)
acf(arimaej,lag.max = 60)
pacf(arimaej)

drift=as.ts(cumsum(arimaej+a0))
plot(drift)

```

Ahora procederemos a simular 
$$(1-B)(1-\phi B)X_{t}+ a_{0}=(1+\theta B)Z_{t}$$
```{r}
Tlength=200
a0=3
a1=-0.5
tiempo=seq(1:Tlength)
xt=a1*tiempo
tendencia=a0+a1*tiempo
drift=a1*rep(1,Tlength)
###Si se desea simular un arima con drfit se debe asignar el valor de d=0 en arima.sim.
arimaej=arima.sim(list(order = c(1,0,1), ar = 0.7,ma=0.6), n = Tlength)


drift=as.ts(cumsum(arimaej+a0))
plot(drift)
acf(drift,lag.max = 60)
pacf(drift)

```



