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
## Screenshot with simulated time waveforms:
![text](https://github.com/viliam-putz/Digital-electronics-1/blob/main/de1%20uloha1-1.png)

