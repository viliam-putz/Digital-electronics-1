# Assignment 4
## Table with connection of 7-segment displays on Nexys A7 board
| **Segment** | **I/O Port** | **Anode** | **I/O Port** | 
| :-: | :-: |  :-: | :-: |
| CA | T10 | AN0 | J17 | 
| CB | R10 | AN1 | J18 |
| CC | K16 | AN2 | T9 |
| CD | K13 | AN3 | J14 |
| CE | P15 | AN4 | P14 |
| CF | T11 | AN5 | T14 |
| CG | L18 | AN6 | K2 |
| DP | H15 | AN7 | U13  |


### Decoder truth table for common anode 7-segment display.

| **Hex** | **Inputs** | **A** | **B** | **C** | **D** | **E** | **F** | **G** | **Outputs** |
| :-: | :-:  |  :-:  |  :-:  |  :-:  |  :-:  |  :-:  |  :-:  |  :-:  |  :-:  |
| 0 | 0000 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0000001 | 
| 1 | 0001 | 1 | 0 | 0 | 1 | 1 | 1 | 1 | 1001111 |
| 2 | 0010 | 0 | 0 | 1 | 0 | 0 | 1 | 0 | 0010010 |
| 3 | 0011 | 0 | 0 | 0 | 0 | 1 | 1 | 0 | 0000110 |
| 4 | 0100 | 1 | 0 | 0 | 1 | 1 | 0 | 0 | 1001100 |
| 5 | 0101 | 0 | 1 | 0 | 0 | 1 | 0 | 0 | 0100100 |
| 6 | 0110 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0100000 |
| 7 | 0111 | 0 | 0 | 0 | 1 | 1 | 1 | 1 | 0001111 |
| 8 | 1000 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0000000 |
| 9 | 1001 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0000100 |
| A | 1010 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0001000 |
| b | 1011 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 1100000 |
| C | 1100 | 0 | 1 | 1 | 0 | 0 | 0 | 1 | 0110001 |
| d | 1101 | 1 | 0 | 0 | 0 | 0 | 1 | 0 | 1000010 |
| E | 1110 | 0 | 1 | 1 | 0 | 0 | 0 | 0 | 0110000 |
| F | 1111 | 0 | 1 | 1 | 1 | 0 | 0 | 0 | 0111000 |

### VHDL architecture from source file hex_7seg.vhd
```vhdl
begin
    
  p_7seg_decoder : process(hex_i)  
    begin                       
        case hex_i is
            when "0000" =>
                seg_o <= "0000001";
            when "0001" =>
                seg_o <= "1001111";
            when "0010" =>
                seg_o <= "0010010";
            when "0011" =>
                seg_o <= "0000110";
            when "0100" =>
                seg_o <= "1001100";
            when "0101" =>
                seg_o <= "0100100";   
            when "0110" =>
                seg_o <= "0100000";  
            when "0111" =>
                seg_o <= "0001111";
            when "1000" =>
                seg_o <= "0000000";
            when "1001" =>
                seg_o <= "0000100";
            when "1010" =>
                seg_o <= "0001000";
            when "1011" =>
                seg_o <= "1100000";
            when "1100" =>
                seg_o <= "0110001";
            when "1101" =>
                seg_o <= "1000010";
            when "1110" =>
                seg_o <= "0110000";
            when others =>
                seg_o <= "0111000"; 
        end case;
    end process p_7seg_decoder;

end Behavioral;
```
### VHDL stimulus process from testbench file tb_hex_7seg.vhd
```vhdl
p_stimulus : process
    begin
        -- Report a note at the begining of stimulus process
        report "Stimulus process started" severity note;
               
        
        s_hex  <= "0000"; wait for 100 ns;
        s_hex  <= "0001"; wait for 100 ns;
        s_hex  <= "0010"; wait for 100 ns;
        s_hex  <= "0011"; wait for 100 ns;
        s_hex  <= "0100"; wait for 100 ns;
        s_hex  <= "0101"; wait for 100 ns;  
        s_hex  <= "0110"; wait for 100 ns; 
        s_hex  <= "0111"; wait for 100 ns;  
        s_hex  <= "1000"; wait for 100 ns;
        s_hex  <= "1001"; wait for 100 ns;
        s_hex  <= "1010"; wait for 100 ns;      
        s_hex  <= "1011"; wait for 100 ns;
        s_hex  <= "1100"; wait for 100 ns;   
        s_hex  <= "1101"; wait for 100 ns;  
        s_hex  <= "1110"; wait for 100 ns;
        s_hex  <= "1111"; wait for 100 ns; 
        -- Report a note at the end of stimulus process
        report "Stimulus process finished" severity note;
        wait;
    end process p_stimulus;
```

### Screenshot with simulated time waveforms
![](https://github.com/viliam-putz/Digital-electronics-1/blob/main/04-segment/scr1.png)


### VHDL code from source file top.vhd
```vhdl
hex2seg : entity work.hex_7seg
        port map(
            hex_i    => SW,
            seg_o(6) => CA,
            seg_o(5) => CB,
            seg_o(4) => CC,
            seg_o(3) => CD,
            seg_o(2) => CE,
            seg_o(1) => CF,
            seg_o(0) => CG
        );
```
### LEDs(7:4) truth table
| **Hex** | **Inputs** | **LED4** | **LED5** | **LED6** | **LED7** |
| :-: | :-: | :-: | :-: | :-: | :-: |
| 0   | 0000 | 1 | 0 | 0 | 0 |
| 1   | 0001 | 0 | 0 | 1 | 1 |
| 2 | 0010 | 0 | 0 | 0 | 1 |
| 3 | 0011 | 0 | 0 | 1 | 0 |
| 4 | 0100 | 0 | 0 | 0 | 1 |
| 5 | 0101 | 0 | 0 | 1 | 0 |
| 6 | 0110 | 0 | 0 | 0 | 0 |
| 7 | 0111 | 0 | 0 | 1 | 0 |
| 8 | 1000 | 0 | 0 | 0 | 1 |
| 9 | 1001 | 0 | 0 | 1 | 0 |
| A | 1010 | 0 | 1 | 0 | 0 |
| b | 1011 | 0 | 1 | 1 | 0 |
| C | 1100 | 0 | 1 | 0 | 0 |
| d | 1101 | 0 | 1 | 1 | 0 |
| E | 1110 | 0 | 1 | 0 | 0 |
| F | 1111 | 0 | 1 | 1 | 0 |

### VHDL code for LEDs(7:4)
```vhdl
LED(4) <= '1' when SW = "0000" else '0';
    LED(5) <= '1' when (SW > "1001") else '0';
    LED(6) <= '1' when (SW = "0001" or SW = "0011" or SW = "0101" or 
                        SW = "0111" or SW = "1001" or SW = "1011" or 
                        SW = "1101" or SW = "1111") 
                  else '0';
    LED(7) <= '1' when (SW = "0001" or SW = "0010" or SW = "0100" or 
                        SW = "1000") 
                  else '0';
```
### Screenshot with simulated time waveforms
![](https://github.com/viliam-putz/Digital-electronics-1/blob/main/04-segment/scr2.png)
