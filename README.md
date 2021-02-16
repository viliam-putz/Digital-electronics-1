# Digital electronics assignment 1

## 1. My repository link:
https://github.com/viliam-putz/Digital-electronics-1

## 2. Verification of De Morgan's laws

### VHDL code:
```
f_o  <= ((not b_i) and a_i) or ((not c_i) and (not b_i));
fnand_o <= not (not (not b_i and a_i) and not(not c_i and not b_i));
fnor_o <= not (b_i or (not a_i)) or (not (c_i or b_i));
```
### Screenshot with simulated time waveforms:
![](https://github.com/viliam-putz/Digital-electronics-1/blob/main/de1%20uloha1-1.png)

### Table:

| **c** | **b** |**a** | **f(c,b,a)** | ***f(c,b,a)NAND*** | ***f(c,b,a)NOR*** |
| :-: | :-: | :-: | :-: | :-: | :-: |
|0|0|0|1|1|1|
|0|0|1|1|1|1|
|0|1|0|0|0|0|
|0|1|1|0|0|0|
|1|0|0|0|0|0|
|1|0|1|1|1|1|
|1|1|0|0|0|0|
|1|1|1|0|0|0|

### EDA playground link:
https://www.edaplayground.com/x/wFJq

## 2. Verification of Distributive laws

### VHDL code:
```
fx1_o  <=   x_i and (not x_i);
fx2_o  <=   x_i or (not x_i);
fx3_o  <=   x_i or x_i or x_i;
fx4_o  <=   x_i and x_i and x_i;
```

### Screenshot with simulated time waveforms:
![](https://github.com/viliam-putz/Digital-electronics-1/blob/main/de1%20uloha1-2.png)

### EDA playground link
https://www.edaplayground.com/x/qrWy
