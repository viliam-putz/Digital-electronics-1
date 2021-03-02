# Assignment 3
## Table with connection of 16 slide switches and 16 LEDs on Nexys A7 board
| **Switch** | **I/O Port** | **LED** | **I/O Port** |
| :-: | :-: | :-: | :-: |
| SW0 | J15 | LED0 | H17 |
| SW1 | L16 | LED1 | K15 |
| SW2 | M13 | LED2 | J13 |
| SW3 | R15 | LED3 | N14 |
| SW4 | R17 | LED4 | R18 |
| SW5 | T18 | LED5 | V17 |
| SW6 | U18 | LED6 | U17 |
| SW7 | R13 | LED7 | U16 |
| SW8 | T8 | LED8 | V16 |
| SW9 | U8 | LED9 | T15 |
| SW10 | R16 | LED10 | U14 |
| SW11 | T13 | LED11 | T16 |
| SW12 | H6 | LED12 | V15 |
| SW13 | U12 | LED13 | V14 |
| SW14 | U11 | LED14 | V12 |
| SW15 | V10 | LED15 | V11 |

## Two-bit wide 4-to-1 multiplexer
```vhdl
architecture Behavioral of mux_2bit_4to1 is
begin
  f_o <= a_i when (sel_i="00") else
         b_i when (sel_i="01") else
         c_i when (sel_i="10") else
         d_i;
  end architecture Behavioral;
```
