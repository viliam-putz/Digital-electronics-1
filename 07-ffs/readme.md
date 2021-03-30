# Assignment 7
## 1. Preparation tasks
### Characteristic equations and completed tables for D, JK, T flip-flops
![](https://github.com/viliam-putz/Digital-electronics-1/blob/main/07-ffs/eq1.png)

![](https://github.com/viliam-putz/Digital-electronics-1/blob/main/07-ffs/eq2.png)

![](https://github.com/viliam-putz/Digital-electronics-1/blob/main/07-ffs/eq3.png)

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
   
## 2. D latch
### VHDL code listing of the process p_d_latch
```vhdl
 p_d_latch : process (d, arst, en)                                                        
    begin                                                                                    
        if (arst = '1') then                                                                 
            q     <= '0';                                                                    
            q_bar <= '1';                                                                               
        elsif (en = '1') then                                                               
            q     <= d;                                                                          
            q_bar <= not d;                                                                          
        end if;                                                                              
    end process p_d_latch;      
```
### Listing of VHDL reset and stimulus processes from the testbench tb_d_latch.vhd file
```vhdl
------------------------------------------
    --Reset generation process
    ------------------------------------------
    p_reset_gen : process
    begin
        s_arst <=  '0';
        wait for 40 ns;
        s_arst <=  '1';
        wait for 40 ns;
        s_arst <=  '0';
        wait for 40 ns;
        s_arst <=  '1';
        wait for 40 ns;
    end process p_reset_gen;
    ------------------------------------------
    --Data generation process
    ------------------------------------------
    p_stimulus  : process
    begin
        report "Stimulus process started" severity note;
        s_en    <= '0';
        s_d     <= '0';
        wait for 10 ns;
        s_en    <= '0';
        s_d     <= '1';
        wait for 10 ns;
        s_en    <= '1';
        s_d     <= '0';
        wait for 10 ns;
        s_en    <= '1';
        s_d     <= '1'; 
        assert(s_q =  '1' and s_q_bar = '0')
        report "s_q = 1, s_q_bar = 0" severity error;       
        wait for 10 ns;
        s_en    <= '0';
        s_d     <= '0';
        wait for 10 ns;
        s_en    <= '0';
        s_d     <= '1';
        wait for 10 ns;
        s_en    <= '1';
        s_d     <= '0';        
        wait for 10 ns;
        s_en    <= '1';
        s_d     <= '1';
        wait for 10 ns;
        s_en    <= '0';
        s_d     <= '0';
        wait for 13 ns;
        s_en    <= '0';
        s_d     <= '1';
        wait for 10 ns;
        s_en    <= '1';
        s_d     <= '0';
        wait for 10 ns;
        s_en    <= '1';
        s_d     <= '1';        
        wait for 10 ns;
        s_en    <= '0';
        s_d     <= '0';
        wait for 10 ns;
        s_en    <= '0';
        s_d     <= '1';
        wait for 10 ns;
        s_en    <= '1';
        s_d     <= '0';        
        wait for 10 ns;
        s_en    <= '1';
        s_d     <= '1';
        assert(s_q =  '1' and s_q_bar = '0')
        report "s_q = 1, s_q_bar = 0" severity error;
        wait for 10 ns;
        s_en    <= '0';
        s_d     <= '0';
        wait for 10 ns;
        
        report "Stimulus process finished" severity note;
    wait;
    end process p_stimulus;
```
### Screenshot with simulated time waveforms; always display all inputs and outputs
![](https://github.com/viliam-putz/Digital-electronics-1/blob/main/07-ffs/screen1.png)
