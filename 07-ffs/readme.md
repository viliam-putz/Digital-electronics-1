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
## 3. Flip-flops
### VHDL code listing of the processes p_d_ff_arst, p_d_ff_rst, p_jk_ff_rst, p_t_ff_rst
#### p_d_ff_arst
```vhdl
p_d_ff_arst : process (clk, arst)             
    begin                                         
        if (arst = '1') then                      
            q     <= '0';                         
            q_bar <= '1';                                    
        elsif  rising_edge(clk) then                    
            q     <= d;                               
            q_bar <= not d;                       
        end if;                                   
    end process p_d_ff_arst; 
```
#### p_d_ff_rst
```vhdl
p_d_ff_rst : process (clk)             
    begin
        if rising_edge(clk) then
            if (rst = '1') then
                q     <= '0';
                q_bar <= '1';
            else
                q     <= d;
                q_bar <= not d;
            end if; 
        end if;
    end process p_d_ff_rst;
```
#### p_jk_ff_rst
```vhdl
p_jk_ff_rst : process (clk)             
    begin                                         
      if rising_edge(clk) then 
          if (rst = '1') then
              s_q <= '0';
          else
              if    (j = '0' and k = '0') then
                  s_q <= s_q;                  
              elsif (j = '0' and k = '1') then
                  s_q <= '0';                 
              elsif (j = '1' and k = '0') then
                  s_q <= '1';                 
              elsif (j = '1' and k = '1') then                   
                  s_q <= not s_q;                    
              end if; 
            end if;                   
        end if;                                   
    end process p_jk_ff_rst;       
```
#### p_t_ff_rst
```vhdl
p_t_ff_rst : process (clk)
    begin
        if rising_edge(clk) then
            if (rst = '1') then
                s_q     <= '0';
                s_q_bar <= '1';
            else
                if (t = '0') then
                    s_q     <= s_q;
                    s_q_bar <= s_q_bar;
                else
                    s_q     <= not s_q;
                    s_q_bar <= not s_q_bar;
                end if;    
            end if;
        end if;
    end process p_t_ff_rst;
```
### Listing of VHDL clock, reset and stimulus processes from the testbench files
#### Listing of VHDL clock, reset and stimulus process - tb_d_ff_arst
```vhdl
p_clk_gen : process
        begin
            while now < 750 ns loop         -- 75 periods of 100MHz clock
                s_clk_100MHz <= '0';
                wait for c_CLK_100MHz_PERIOD / 2;
                s_clk_100MHz <= '1';
                wait for c_CLK_100MHz_PERIOD / 2;
            end loop;
            wait;
        end process p_clk_gen;
    ------------------------------------------
    --Reset generation process
    ------------------------------------------    
     p_reset_gen : process
        begin
            s_arst <=  '0';
        wait for 20 ns;
        s_arst <=  '1';
        wait for 20 ns;        
        s_arst <=  '0';
        wait for 20 ns;
        s_arst <=  '1';
        wait for 20 ns;       
        s_arst <=  '0';   
        wait;
        end process p_reset_gen;
    ------------------------------------------
    --Data generation process
    ------------------------------------------ 
    p_stimulus : process
    begin
        report "Stimulus process started" severity note;
        s_d     <= '0';
        wait for 10 ns;
        s_d     <= '1';
        wait for 10 ns;
        s_d     <= '0';
        wait for 10 ns;
        s_d     <= '1';        
        assert(s_q =  '1' and s_q_bar = '0')
        report "s_q = 1, s_q_bar = 0" severity error;       
        wait for 10 ns;
        s_d     <= '0';
        wait for 10 ns;
        s_d     <= '1';
        wait for 10 ns;
        s_d     <= '0';      
        assert(s_q =  '0' and s_q_bar = '1')
        report "s_q = 0, s_q_bar = 1" severity error;      
        wait for 10 ns;
        s_d     <= '1';
        wait for 10 ns;
        s_d     <= '0';
        report "Stimulus process finished" severity note;
        wait;
    end process p_stimulus;
```
#### Listing of VHDL clock, reset and stimulus process - tb_d_ff_rst
```vhdl
p_clk_gen : process
        begin
            while now < 750 ns loop         -- 75 periods of 100MHz clock
                s_clk_100MHz <= '0';
                wait for c_CLK_100MHz_PERIOD / 2;
                s_clk_100MHz <= '1';
                wait for c_CLK_100MHz_PERIOD / 2;
            end loop;
            wait;
        end process p_clk_gen;        
    ------------------------------------------
    --Reset generation process
    ------------------------------------------    
     p_reset_gen : process
        begin
            s_rst <=  '0';
        wait for 20 ns;
        s_rst <=  '1';
        wait for 20 ns;        
        s_rst <=  '0';
        wait for 20 ns;
        s_rst <=  '1';
        wait for 20 ns;        
        s_rst <=  '0';
        wait;
        end process p_reset_gen;      
    ------------------------------------------
    --Data generation process
    ------------------------------------------ 
    p_stimulus : process
    begin
        report "Stimulus process started" severity note;
        s_d     <= '0';
        wait for 10 ns;
        s_d     <= '1';
        wait for 10 ns;
        s_d     <= '0';
        wait for 10 ns;
        s_d     <= '1';      
        assert(s_q =  '1' and s_q_bar = '0')
        report "s_q = 1, s_q_bar = 0" severity error;       
        wait for 10 ns;
        s_d     <= '0';
        wait for 10 ns;
        s_d     <= '1';
        wait for 10 ns;
        s_d     <= '0';       
        assert(s_q =  '0' and s_q_bar = '1')
        report "s_q = 0, s_q_bar = 1" severity error;       
        wait for 10 ns;
        s_d     <= '1';
        wait for 10 ns;
        s_d     <= '0';
        report "Stimulus process finished" severity note;
    wait;
    end process p_stimulus;
```

#### Listing of VHDL clock, reset and stimulus process - tb_jk_ff_rst
```vhdl
p_clk_gen : process
    begin
        while now < 750 ns loop         -- 75 periods of 100MHz clock
            s_clk_100MHz <= '0';
            wait for c_CLK_100MHz_PERIOD / 2;
            s_clk_100MHz <= '1';
            wait for c_CLK_100MHz_PERIOD / 2;
        end loop;
        wait;
    end process p_clk_gen;
    ------------------------------------------
    --Reset generation process
    ------------------------------------------     
     p_reset_gen : process
        begin
            s_rst <=  '0';
        wait for 40 ns;        
        s_rst <=  '1';
        wait for 40 ns;        
        s_rst <=  '0';   
            wait;
        end process p_reset_gen;
    ------------------------------------------
    --Data generation process
    ------------------------------------------    
    p_stimulus : process
    begin
        report "Stimulus process started" severity note;     
        s_j     <= '0';
        s_k     <= '0';
        wait for 10 ns;
        s_j     <= '0';
        s_k     <= '1';
        wait for 10 ns;
        s_j     <= '1';
        s_k     <= '0';
        wait for 10 ns;
        s_j     <= '1';
        s_k     <= '1';
        wait for 10 ns;      
        assert(s_q =  '1' and s_q_bar = '0')
        report "s_q = 1, s_q_bar = 0" severity error;        
        s_j     <= '0';
        s_k     <= '0';
        wait for 10 ns;
        s_j     <= '0';
        s_k     <= '1';
        wait for 10 ns;
        s_j     <= '1';
        s_k     <= '0';
        wait for 10 ns;
        s_j     <= '1';
        s_k     <= '1';        
        assert(s_q =  '1' and s_q_bar = '0')
        report "s_q = 1, s_q_bar = 0" severity error;
        wait for 10 ns;
        s_j     <= '0';
        s_k     <= '0';
        report "Stimulus process finished" severity note;
        wait;
    end process p_stimulus;
```

#### Listing of VHDL clock, reset and stimulus process - tb_t_ff_rst
```vhdl
p_clk_gen : process
    begin
        while now < 750 ns loop         -- 75 periods of 100MHz clock
            s_clk_100MHz <= '0';
            wait for c_CLK_100MHz_PERIOD / 2;
            s_clk_100MHz <= '1';
            wait for c_CLK_100MHz_PERIOD / 2;
        end loop;
        wait;
    end process p_clk_gen;    
    ------------------------------------------
    --Reset generation process
    ------------------------------------------    
     p_reset_gen : process
        begin
            s_rst <=  '1';
        wait for 10 ns;
        s_rst <=  '0';
        wait for 20 ns;
        s_rst <=  '1';
        wait for 20 ns;
        s_rst <=  '0';
        wait;
        end process p_reset_gen; 
    ------------------------------------------
    --Data generation process
    ------------------------------------------ 
    p_stimulus : process
    begin
        report "Stimulus process started" severity note;
        s_t     <= '0';
        wait for 20 ns;
        s_t     <= '1';
        wait for 10 ns;
        s_t     <= '0';
        wait for 10 ns;
        s_t     <= '1';
        assert(s_q =  '1' and s_q_bar = '0')
        report "s_q = 1, s_q_bar = 0" severity error;    
        wait for 10 ns;
        s_t     <= '1';
        wait for 10 ns;
        s_t     <= '0';
        wait for 10 ns;
        s_t     <= '1';
        assert(s_q =  '0' and s_q_bar = '1')
        report "s_q = 0, s_q_bar = 1" severity error;
        wait for 10 ns;        
        s_t     <= '0';
        report "Stimulus process finished" severity note;
        wait;
    end process p_stimulus; 
```
### Screenshots with simulated time waveforms
#### d_ff_arst
![](https://github.com/viliam-putz/Digital-electronics-1/blob/main/07-ffs/screen2.png)
#### d_ff_rst
![](https://github.com/viliam-putz/Digital-electronics-1/blob/main/07-ffs/screen3.png)
#### jk_ff_rst
![](https://github.com/viliam-putz/Digital-electronics-1/blob/main/07-ffs/screen4.png)
#### t_ff_rst
![](https://github.com/viliam-putz/Digital-electronics-1/blob/main/07-ffs/screen5.png)
