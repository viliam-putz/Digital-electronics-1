# Assignment 8
## 1. Preparation tasks
### Completed state table
| **Input P** | `0` | `0` | `1` | `1` | `0` | `1` | `0` | `1` | `1` | `1` | `1` | `0` | `0` | `1` | `1` | `1` |
| :-- | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| **Clock** | ![rising](eq_uparrow.png) | ![rising](eq_uparrow.png) | ![rising](eq_uparrow.png) | ![rising](eq_uparrow.png) | ![rising](eq_uparrow.png) | ![rising](eq_uparrow.png) | ![rising](eq_uparrow.png) | ![rising](eq_uparrow.png) | ![rising](eq_uparrow.png) | ![rising](eq_uparrow.png) | ![rising](eq_uparrow.png) | ![rising](eq_uparrow.png) | ![rising](eq_uparrow.png) | ![rising](eq_uparrow.png) | ![rising](eq_uparrow.png) | ![rising](eq_uparrow.png) |
| **State** | A | A | B | C | C | D | A | B | C | D | B | B | B | C | D | B |
| **Output R** | `0` | `0` | `0` | `0` | `0` | `1` | `0` | `0` | `0` | `1` | `0` | `0` | `0` | `0` | `1` | `0` |
### Figure with connection of RGB LEDs on Nexys A7 board and completed table with color settings
![figure](n4r-1.png)
## 2. Traffic light controller
### State diagram
![statediagram](state.png)
