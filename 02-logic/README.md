# Assignment 2

## 2-bit comparator
link to EDA

### 2-bit comparator truth table

| **Dec. equivalent** | **B [1:0]** | **A [1:0]** | **B is greater than A** | **B equals A** | **B is less than A** |
| :-: | :-: | :-: | :-: | :-: | :-: |
| 0 | 0 0 | 0 0 | 0 | 1 | 0 |
| 1 | 0 0 | 0 1 | 0 | 0 | 1 |
| 2 | 0 0 | 1 0 | 0 | 0 | 1 |
| 3 | 0 0 | 1 1 | 0 | 0 | 1 |
| 4 | 0 1 | 0 0 | 1 | 0 | 0 |
| 5 | 0 1 | 0 1 | 0 | 1 | 0 |
| 6 | 0 1 | 1 0 | 0 | 0 | 1 |
| 7 | 0 1 | 1 1 | 0 | 0 | 1 |
| 8 | 1 0 | 0 0 | 1 | 0 | 0 |
| 9 | 1 0 | 0 1 | 1 | 0 | 0 |
| 10 | 1 0 | 1 0 | 0 | 1 | 0 |
| 11 | 1 0 | 1 1 | 0 | 0 | 1 |
| 12 | 1 1 | 0 0 | 1 | 0 | 0 |
| 13 | 1 1 | 0 1 | 1 | 0 | 0 |
| 14 | 1 1 | 1 0 | 1 | 0 | 0 |
| 15 | 1 1 | 1 1 | 0 | 1 | 0 |

### Karnaugh map - B is greater than A

  |  | **00** | **01** | **11** | **10** |
  | :-: | :-: | :-: | :-: | :-: |
  | **00** | 0 | 0 | 0 | 0 |
  | **01** | 1 | 0 | 0 | 0 |
  | **11** | 1 | 1 | 0 | 1 |
  | **10** | 1 | 1 | 0 | 0 |
  
### Karnaugh map - B equals A
  |  | **00** | **01** | **11** | **10** |
  | :-: | :-: | :-: | :-: | :-: |
  | **00** | 1 | 0 | 0 | 0 |
  | **01** | 0 | 1 | 0 | 0 |
  | **11** | 0 | 0 | 1 | 0 |
  | **10** | 0 | 0 | 0 | 1 |

### Karnaugh map - B is less than A
  |  | **00** | **01** | **11** | **10** |
  | :-: | :-: | :-: | :-: | :-: |
  | **00** | 0 | 1 | 1 | 1 |
  | **01** | 0 | 0 | 1 | 1 |
  | **11** | 1 | 1 | 0 | 1 |
  | **10** | 0 | 0 | 1 | 0 |
  
### Equations of simplified SoP form of the "greater than" function and simplified PoS form of the "less than" function:
![](https://github.com/viliam-putz/Digital-electronics-1/blob/main/Equations_SoP_PoS.gif)
  
## 4-bit comparator
link to EDA

## VHDL architecture from design file
```
entity comparator_4bit is
    port(
      a_i           : in  std_logic_vector(4 - 1 downto 0);
      b_i           : in  std_logic_vector(4 - 1 downto 0);


	B_greater_A_o : out std_logic;       -- B is greater than A
        B_equals_A_o  : out std_logic;       -- B equals A
        B_less_A_o    : out std_logic       -- B is less than A
    );
end entity comparator_4bit;


architecture Behavioral of comparator_4bit is
begin

    B_less_A_o    <= '1' when (b_i < a_i) else '0';
    B_greater_A_o <= '1' when (b_i > a_i) else '0';
    B_equals_A_o  <= '1' when (b_i = a_i) else '0';


end architecture Behavioral;
```
## VHDL stimulus process from testbench file
```vhdl
p_stimulus : process
    begin

        report "Stimulus process started" severity note;


		s_b <= "0000"; s_a <= "0000"; wait for 100 ns;
		assert ((s_B_greater_A = '0') and (s_B_equals_A = '1') and (s_B_less_A = '0'))
		report "Test failed for input combination: 0000, 0000" severity error;


		s_b <= "0000"; s_a <= "0001"; wait for 100 ns;
		assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
		report "Test failed for input combination: 0000, 0001" severity error;


		s_b <= "0000"; s_a <= "0010"; wait for 100 ns;
		assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
		report "Test failed for input combination: 0000, 0010" severity error;


		s_b <= "0000"; s_a <= "0011"; wait for 100 ns;
		assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
		report "Test failed for input combination: 0000, 0011" severity error;


		s_b <= "0000"; s_a <= "0100"; wait for 100 ns;
		assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
		report "Test failed for input combination: 0000, 0100" severity error;


      		s_b <= "0000"; s_a <= "0101"; wait for 100 ns;
		assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
		report "Test failed for input combination: 0000, 0101" severity error;


		s_b <= "0000"; s_a <= "0110"; wait for 100 ns;
		assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
		report "Test failed for input combination: 0000, 0110" severity error;


		s_b <= "0000"; s_a <= "0111"; wait for 100 ns;
		assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
		report "Test failed for input combination: 0000, 0111" severity error;


		s_b <= "0000"; s_a <= "1000"; wait for 100 ns;
		assert ((s_B_greater_A = '0') and (s_B_equals_A = '0') and (s_B_less_A = '1'))
		report "Test failed for input combination: 0000, 1000" severity error;


		s_b <= "0000"; s_a <= "1001"; wait for 100 ns;
		assert ((s_B_greater_A = '0') and (s_B_equals_A = '1') and (s_B_less_A = '1'))
		report "Test failed for input combination: 0000, 1001" severity error;
        



        report "Stimulus process finished" severity note;
        wait;
    end process p_stimulus;

```
## Console output

![](https://github.com/viliam-putz/Digital-electronics-1/blob/main/console.png)
