# Assignment 7
## 1. Preparation tasks
### Characteristic equations and completed tables for D, JK, T flip-flops
   | **clk** | **d** | **q(n)** | **q(n+1)** | **Comments** |
   | :-: | :-: | :-: | :-: | :-- |
   | ![](eq_uparrow.png) | 0 | 0 | 0 | No change |
   | ![](eq_uparrow.png) | 0 | 1 | 0 | Change |
   | ![](eq_uparrow.png) | 1 | 1 | 1 | No change |
   | ![](eq_uparrow.png) | 1 | 0 | 1 | Change |

   | **clk** | **j** | **k** | **q(n)** | **q(n+1)** | **Comments** |
   | :-: | :-: | :-: | :-: | :-: | :-- |
   | ![](eq_uparrow.png) | 0 | 0 | 0 | 0 | No change |
   | ![](eq_uparrow.png) | 0 | 0 | 1 | 1 | No change |
   | ![](eq_uparrow.png) | 0 | 1 | 0 | 0 | Reset |
   | ![](eq_uparrow.png) | 0 | 1 | 1 | 0 | Reset |
   | ![](eq_uparrow.png) | 1 | 0 | 0 | 1 | Set |
   | ![](eq_uparrow.png) | 1 | 0 | 1 | 1 | Set |
   | ![](eq_uparrow.png) | 1 | 1 | 0 | 1 | Toggle |
   | ![](eq_uparrow.png) | 1 | 1 | 1 | 0 | Toggle |

   | **clk** | **t** | **q(n)** | **q(n+1)** | **Comments** |
   | :-: | :-: | :-: | :-: | :-- |
   | ![](eq_uparrow.png) | 0 | 0 | 0 | No change |
   | ![](eq_uparrow.png) | 0 | 1 | 1 | No change |
   | ![](eq_uparrow.png) | 1 | 0 | 1 | Invert |
   | ![](eq_uparrow.png) | 1 | 1 | 0 | Invert |