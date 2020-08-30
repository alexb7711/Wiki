---
title: Plotting Root Locus with Matlab
geometry: margin=1in
---

```
s = tf('s') # makes the transfer function 
G = 1/(s+100) # Transfer function we are concerned with
G = zpk(G) # Factors Denominator 
rlocus(G) # Plots root locus of G
```
