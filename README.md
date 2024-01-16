# **RPN CALCULATOR BY STUDP7 AND BORGN1**
## **Projekt : INSERT PROJEKT NAME**
### In this file can be found a general description of the project for the rpn calculator described using VHDL 
> For every file you can find which block are included, a diagram, a port table, a signal table, process and if any instantiations.

> After the descriptions of all entities can be found the order in which the files were compiled. (STILL NOT DONE) 

## **Work distribution**
In order to divide the work among us, we as a first step carefully read the task and determined which blocks were needed, after that it proceeded quite "automatically" whenever someone had finished a specific block he would inform the other and inquire about what stage the other was at, in this way it was known what the next block was to be made and one could immediately start. 

## **Work distribution table**
### In the following list you can see who did which file (Block) of the projekt
- rpn_calculator_top_leguan.vhdl  => GIVEN (MHT1)
- RGBArrayColumnScanning.vhdl     => GIVEN (MHT1)
- rpn_calculator_module.vhdl      => STUDP7
- keyboard_Reader.vhd             => STUDP7
- shift_register.vhd              => BORGN1
- BCD_2_7Seg.vhd                  => BORGN1
- BCD_2_BIN.vhd                   => BORGN1
- lifo_stack_pkg.vhd              => STUDP7
- lifo_stack.vhd                  => STUDP7
- multiplier.vhd                  => STUDP7
- divider.vhd                     => STUDP7
- calc.vhd                        => STUDP7
- BIN_2_BCD.vhd                   => BORGN1
- REAME.md                        => BORGN1

# Entity: rpn_calculator_top_leguan 
- **File**: rpn_calculator_top_leguan.vhdl

## Diagram
![rpn_calculator_top_leguan](https://github.com/NikBia02/rpn_calculator_STUDP7_BORGN1/assets/156720168/c3fffd46-3d7a-4337-bef2-0b99fe1271cc)

## Ports

| Port name      | Direction | Type                         | Description |
| -------------- | --------- | ---------------------------- | ----------- |
| clk_25_MHz     | in        | std_logic                    |             |
| reset_n        | in        | std_logic                    |             |
| btn_pop_lifo_n | in        | std_logic                    |             |
| seg1_n         | out       | std_logic_vector(6 downto 0) |             |
| seg2_n         | out       | std_logic_vector(6 downto 0) |             |
| seg3_n         | out       | std_logic_vector(6 downto 0) |             |
| seg4_n         | out       | std_logic_vector(6 downto 0) |             |
| overflow_n     | out       | std_logic                    |             |
| div_by_zero_n  | out       | std_logic                    |             |
| row            | in        | std_logic_vector(1 to 4)     |             |
| col            | out       | std_logic_vector(1 to 4)     |             |
| columnAddress  | out       | std_logic_vector(3 downto 0) |             |
| rowRedLeds_b   | out       | std_logic_vector(9 downto 0) |             |
| rowGreenLeds_b | out       | std_logic_vector(9 downto 0) |             |
| rowBlueLeds_b  | out       | std_logic_vector(9 downto 0) |             |

## Signals

| Name           | Type                           | Description |
| -------------- | ------------------------------ | ----------- |
| s_btn_pop_lifo | std_logic                      |             |
| s_seg1         | std_logic_vector(6 downto 0)   |             |
| s_seg2         | std_logic_vector(6 downto 0)   |             |
| s_seg3         | std_logic_vector(6 downto 0)   |             |
| s_seg4         | std_logic_vector(6 downto 0)   |             |
| s_overflow     | std_logic                      |             |
| s_div_by_zero  | std_logic                      |             |
| s_leds         | std_logic_vector(109 downto 0) |             |
| s_led_matrix   | led_array                      |             |

## Processes
- unnamed: ( s_led_matrix )

## Instantiations

- rpn_calculator_module_inst: rpn_calculator_module
- RGBArrayColumnScanning_inst: RGBArrayColumnScanning


# Entity: RGBArrayColumnScanning 
- **File**: RGBArrayColumnScanning.vhdl

## Diagram
![RGBArrayColumnScanning](https://github.com/NikBia02/rpn_calculator_STUDP7_BORGN1/assets/156720168/f03c706a-07d2-4e09-b1cb-c7784e499f4f)

## Generics

| Generic name        | Type                           | Value | Description |
| ------------------- | ------------------------------ | ----- | ----------- |
| singleColor         | std_logic                      | '0'   |             |
| singleColorValueRGB | std_logic_vector( 2 downto 0 ) | "101" |             |

## Ports

| Port name         | Direction | Type                             | Description |
| ----------------- | --------- | -------------------------------- | ----------- |
| clock25MHz        | in        | std_logic                        |             |
| internalRedLeds   | in        | std_logic_vector( 109 downto 0 ) |             |
| internalBlueLeds  | in        | std_logic_vector( 109 downto 0 ) |             |
| internalGreenLeds | in        | std_logic_vector( 109 downto 0 ) |             |
| columnAddress     | out       | std_logic_vector( 3 downto 0 )   |             |
| rowRedLeds_b      | out       | std_logic_vector( 9 downto 0 )   |             |
| rowGreenLeds_b    | out       | std_logic_vector( 9 downto 0 )   |             |
| rowBlueLeds_b     | out       | std_logic_vector( 9 downto 0 )   |             |

## Signals

| Name                  | Type                           | Description |
| --------------------- | ------------------------------ | ----------- |
| s_scanningCounterReg  | unsigned( 14 downto 0 )        |             |
| s_scanningCounterNext | unsigned( 14 downto 0 )        |             |
| s_tickNext            | std_logic                      |             |
| s_tickReg             | std_logic                      |             |
| s_columnCounterNext   | unsigned( 3 downto 0 )         |             |
| s_columnCounterReg    | unsigned( 3 downto 0 )         |             |
| s_correctRedColumn    | std_logic_vector( 9 downto 0 ) |             |
| s_correctGreenColumn  | std_logic_vector( 9 downto 0 ) |             |
| s_correctBlueColumn   | std_logic_vector( 9 downto 0 ) |             |

## Processes
- scanningFlipFlops: ( clock25MHz )
- columnCounterFlipFlops: ( clock25MHz )
- selectCorrectColumn: ( s_columnCounterReg , internalRedLeds, internalBlueLeds ,
                                  internalGreenLeds )


# Entity: rpn_calculator_module 
- **File**: rpn_calculator_module.vhdl

## Diagram
![rpn_calculator_module](https://github.com/NikBia02/rpn_calculator_STUDP7_BORGN1/assets/156720168/4368636d-dac2-4a1c-abc6-a040470ea7d1)

## Ports

| Port name    | Direction | Type                         | Description |
| ------------ | --------- | ---------------------------- | ----------- |
| clk          | in        | std_logic                    |             |
| reset_n      | in        | std_logic                    |             |
| btn_pop_lifo | in        | std_logic                    |             |
| seg1         | out       | std_logic_vector(6 downto 0) |             |
| seg2         | out       | std_logic_vector(6 downto 0) |             |
| seg3         | out       | std_logic_vector(6 downto 0) |             |
| seg4         | out       | std_logic_vector(6 downto 0) |             |
| overflow     | out       | std_logic                    |             |
| div_by_zero  | out       | std_logic                    |             |
| row          | in        | std_logic_vector(1 to 4)     |             |
| col          | out       | std_logic_vector(1 to 4)     |             |
| led_matrix   | out       | led_array                    |             |

## Signals

| Name                | Type                          | Description |
| ------------------- | ----------------------------- | ----------- |
| keypad_out          | std_logic_vector(3 downto 0)  |             |
| keypad_strobe       | std_logic                     |             |
| shift_reg_sign      | std_logic                     |             |
| shift_reg_en        | std_logic                     |             |
| shift_reg_reset     | std_logic                     |             |
| shift_reg_in        | std_logic_vector(3 downto 0)  |             |
| shift_reg_out       | std_logic_vector(12 downto 0) |             |
| shift_reg_direct    | std_logic_vector(10 downto 0) |             |
| shift_reg_overwrite | std_logic                     |             |
| x_op                | std_logic_vector(10 downto 0) |             |
| y_op                | std_logic_vector(10 downto 0) |             |
| push_sig            | std_logic                     |             |
| pop_sig             | std_logic                     |             |
| lifo_stack_out      | stack_type                    |             |
| pop_btn_debounced   | std_logic                     |             |
| pop_btn_debounced2  | std_logic                     |             |
| pop_vec             | std_logic_vector(40 downto 0) |             |
| operation           | std_logic_vector(1 downto 0)  |             |
| calc_en             | std_logic                     |             |
| calc_done           | std_logic                     |             |
| calc_overflow       | std_logic                     |             |
| calc_div_zero       | std_logic                     |             |
| calc_result         | std_logic_vector(10 downto 0) |             |
| current_state       | fsm_states                    |             |
| last_state          | fsm_states                    |             |

## Types

| Name       | Type                                                                                                                                                                                                                                                     | Description |
| ---------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| fsm_states | (WAIT_INPUT,<br><span style="padding-left:20px"> CALC_WAIT,<br><span style="padding-left:20px"> CALC_OK,<br><span style="padding-left:20px"> CALC_NO_OK,<br><span style="padding-left:20px"> SHIFT_RESET,<br><span style="padding-left:20px"> PUSH_LIFO) |             |

## Processes
- FSM: ( clk )
- pop_debounce: ( clk )

## Instantiations

- kread: work.keyboard_reader
- shift_reg1: work.shift_register
- sevenSeg1: work.BCD_2_7Seg
- BCD2Bin: work.BCD_2_BIN
- lifo_stack: work.lifo_stack
- calc: work.calc

## State machines

![fsm_rpn_calculator_module_00](https://github.com/NikBia02/rpn_calculator_STUDP7_BORGN1/assets/156720168/4b70001d-391a-424e-9ca6-8931a54acdf0)

 
# Entity: keyboard_reader 
- **File**: keyboard_reader.vhd

## Diagram
![keyboard_reader](https://github.com/NikBia02/rpn_calculator_STUDP7_BORGN1/assets/156720168/8406514e-bf3d-4d38-b936-52fad0c7dcaa)

## Ports

| Port name | Direction | Type                         | Description |
| --------- | --------- | ---------------------------- | ----------- |
| clk       | in        | std_logic                    |             |
| reset     | in        | std_logic                    |             |
| key_out   | out       | std_logic_vector(3 downto 0) |             |
| strobe    | in        | std_logic_vector(1 to 4)     |             |
| col       | out       | std_logic_vector(1 to 4)     |             |

## Signals

| Name        | Type                         | Description |
| ----------- | ---------------------------- | ----------- |
| state_reg   | states                       |             |
| state_next  | states                       |             |
| pulse_1ms   | std_logic                    |             |
| key_pressed | std_logic_vector(4 downto 0) |             |
| key_storage | key_array                    |             |

## Types

| Name      | Type                                                                                                                                                                                                                                                    | Description |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------- |
| states    | (READ_COL1,<br><span style="padding-left:20px"> READ_COL2,<br><span style="padding-left:20px"> READ_COL3,<br><span style="padding-left:20px"> READ_COL4,<br><span style="padding-left:20px"> SHIFT_REG,<br><span style="padding-left:20px"> OUTPUT_KEY) |             |
| key_array |                                                                                                                                                                                                                                                         |             |

## Processes
- REG: ( clk, reset )
- OL: ( state_reg, row, clk )
- NSL: ( state_reg, pulse_1ms )

## Instantiations

- clk1: work.pulse_generator_1KHz(dfl)

## State machines
![fsm_keyboard_reader_00](https://github.com/NikBia02/rpn_calculator_STUDP7_BORGN1/assets/156720168/1759ad5f-12e4-41e7-9db9-abcb264fbe32)


# Entity: shift_register 
- **File**: shift_register.vhd

## Diagram
![shift_register](https://github.com/NikBia02/rpn_calculator_STUDP7_BORGN1/assets/156720168/adc4ec97-263c-408b-bc73-9fead6b0b321)

## Ports

| Port name     | Direction | Type                           | Description |
| ------------- | --------- | ------------------------------ | ----------- |
| clk           | in        | std_logic                      |             |
| reset         | in        | std_logic                      |             |
| sign          | in        | std_logic                      |             |
| enable        | in        | std_logic                      |             |
| overwrite     | in        | std_logic                      |             |
| pressed_key   | in        | std_logic_vector (3 downto 0)  |             |
| direct_in     | in        | std_logic_vector(10 downto 0)  |             |
| shift_reg_out | out       | std_logic_vector (12 downto 0) |             |

## Signals

| Name              | Type                           | Description |
| ----------------- | ------------------------------ | ----------- |
| x_Operator_Intern | std_logic_vector (12 downto 0) |             |
| bin2bcd_ones      | std_logic_vector(3 downto 0)   |             |
| bin2bcd_tens      | std_logic_vector(3 downto 0)   |             |
| bin2bcd_hunderts  | std_logic_vector(3 downto 0)   |             |
| bin2bcd_sign      | std_logic                      |             |

## Processes
- enabled: ( enable, clk )

## Instantiations

- Bin2BCD: work.BIN_2_BCD



# Entity: BCD_2_7Seg 
- **File**: BCD_2_7Seg.vhd

## Diagram
![BCD_2_7Seg](https://github.com/NikBia02/rpn_calculator_STUDP7_BORGN1/assets/156720168/b591d0f1-69b0-4979-84cd-e1f6ad812fa9)
## Ports


| Port name | Direction | Type                          | Description |
| --------- | --------- | ----------------------------- | ----------- |
| number    | in        | std_logic_vector(12 downto 0) |             |
| unity     | out       | std_logic_vector(6 downto 0)  |             |
| tens      | out       | std_logic_vector(6 downto 0)  |             |
| hunderts  | out       | std_logic_vector(6 downto 0)  |             |
| POS_NEG   | out       | std_logic_vector(6 downto 0)  |             |

## Processes
- First: ( number )
- Second: ( number )
- Third: ( number )
- Negative: ( number )


# Entity: BCD_2_BIN 
- **File**: BCD_2_BIN.vhd

## Diagram
![BCD_2_BIN](https://github.com/NikBia02/rpn_calculator_STUDP7_BORGN1/assets/156720168/307ba079-5d22-46b2-9a84-1a90dadc76ca)

## Ports

| Port name   | Direction | Type                          | Description |
| ----------- | --------- | ----------------------------- | ----------- |
| clk         | in        | std_logic                     |             |
| unit_in     | in        | std_logic_vector (3 downto 0) |             |
| tens_in     | in        | std_logic_vector (3 downto 0) |             |
| hundreds_in | in        | std_logic_vector (3 downto 0) |             |
| sign_in     | in        | std_logic                     |             |
| bin_out     | out       | std_logic_vector(10 downto 0) |             |

## Processes
- controll_sign: ( sign_in, unit_in, tens_in, hundreds_in, clk )


# Package: lifo_stack_pkg 
- **File**: lifo_stack_pkg.vhd

## Constants

| Name  | Type     | Value | Description |
| ----- | -------- | ----- | ----------- |
| DEPTH | positive | 9     |             |
| NBITS | positive | 11    |             |

## Types

| Name       | Type | Description |
| ---------- | ---- | ----------- |
| stack_type |      |             |


# Entity: lifo_stack 
- **File**: lifo_stack.vhd

## Diagram
![lifo_stack](https://github.com/NikBia02/rpn_calculator_STUDP7_BORGN1/assets/156720168/1ce6cc9f-4a22-45bc-9577-762979f96562)

## Ports

| Port name | Direction | Type                                 | Description |
| --------- | --------- | ------------------------------------ | ----------- |
| clk       | in        | std_logic                            |             |
| reset     | in        | std_logic                            |             |
| push      | in        | std_logic                            |             |
| pop       | in        | std_logic                            |             |
| input     | in        | std_logic_vector(NBITS - 1 downto 0) |             |
| output    | out       | std_logic_vector(NBITS - 1 downto 0) |             |
| stack_out | out       | stack_type                           |             |

## Signals

| Name  | Type       | Description |
| ----- | ---------- | ----------- |
| stack | stack_type |             |

## Processes
- unnamed: ( clk, reset )


# Entity: multiplier 
- **File**: multiplier.vhd

## Diagram
![multiplier](https://github.com/NikBia02/rpn_calculator_STUDP7_BORGN1/assets/156720168/fa5d0fba-a40c-49d4-958f-afb330aa46fa)

## Generics

| Generic name | Type     | Value | Description |
| ------------ | -------- | ----- | ----------- |
| NBITS        | positive | 11    |             |

## Ports

| Port name | Direction | Type                                 | Description |
| --------- | --------- | ------------------------------------ | ----------- |
| clk       | in        | std_logic                            |             |
| y_in      | in        | std_logic_vector(NBITS - 1 downto 0) |             |
| x_in      | in        | std_logic_vector(NBITS - 1 downto 0) |             |
| error_sig | out       | std_logic                            |             |
| output    | out       | signed(NBITS - 1 downto 0)           |             |

## Types

| Name  | Type | Description |
| ----- | ---- | ----------- |
| multi |      |             |

## Processes
- unnamed: ( y_in, x_in )


# Entity: divider 
- **File**: divider.vhd

## Diagram
![divider](https://github.com/NikBia02/rpn_calculator_STUDP7_BORGN1/assets/156720168/9ce7df8d-f09a-42c3-a644-92d0f834989b)

## Generics

| Generic name | Type     | Value | Description |
| ------------ | -------- | ----- | ----------- |
| NBITS        | positive | 11    |             |

## Ports

| Port name | Direction | Type                                 | Description |
| --------- | --------- | ------------------------------------ | ----------- |
| clk       | in        | std_logic                            |             |
| y_in      | in        | std_logic_vector(NBITS - 1 downto 0) |             |
| x_in      | in        | std_logic_vector(NBITS - 1 downto 0) |             |
| error_sig | out       | std_logic                            |             |
| output    | out       | signed(NBITS - 1 downto 0)           |             |

## Processes
- unnamed: ( y_in, x_in )


# Entity: calc 
- **File**: calc.vhd

## Diagram
![calc](https://github.com/NikBia02/rpn_calculator_STUDP7_BORGN1/assets/156720168/a10bb3d6-e574-444a-b5ea-233ed1db9fbe)

## Generics

| Generic name | Type     | Value | Description |
| ------------ | -------- | ----- | ----------- |
| NBITS        | positive | 11    |             |

## Ports

| Port name | Direction | Type                                 | Description |
| --------- | --------- | ------------------------------------ | ----------- |
| clk       | in        | std_logic                            |             |
| y_in      | in        | std_logic_vector(NBITS - 1 downto 0) |             |
| x_in      | in        | std_logic_vector(NBITS - 1 downto 0) |             |
| start     | in        | std_logic                            |             |
| operation | in        | std_logic_vector(1 downto 0)         |             |
| done      | out       | std_logic                            |             |
| error_sig | out       | std_logic                            |             |
| error_div | out       | std_logic                            |             |
| output    | out       | std_logic_vector(NBITS - 1 downto 0) |             |

## Signals

| Name         | Type                        | Description |
| ------------ | --------------------------- | ----------- |
| done_intern  | std_logic                   |             |
| start_intern | std_logic                   |             |
| out_sig      | signed (NBITS - 1 downto 0) |             |
| err_mult     | std_logic                   |             |
| out_mult     | signed (NBITS - 1 downto 0) |             |
| err_div      | std_logic                   |             |
| out_div      | signed (NBITS - 1 downto 0) |             |
| y_comp       | signed (NBITS - 1 downto 0) |             |
| x_comp       | signed (NBITS - 1 downto 0) |             |

## Processes
- unnamed: ( clk )

## Instantiations

- multi: work.multiplier
- div: work.divider


# Entity: BIN_2_BCD 
- **File**: BIN_2_BCD.vhd

## Diagram
![BIN_2_BCD](https://github.com/NikBia02/rpn_calculator_STUDP7_BORGN1/assets/156720168/08b4f979-8489-45eb-817c-ec1f2dfded0c)

## Ports

| Port name    | Direction | Type                           | Description |
| ------------ | --------- | ------------------------------ | ----------- |
| input        | in        | std_logic_vector (10 downto 0) |             |
| clk          | in        | std_logic                      |             |
| sign_out     | out       | std_logic                      |             |
| BCD_unit_out | out       | std_logic_vector (3 downto 0)  |             |
| BCD_tens_out | out       | std_logic_vector (3 downto 0)  |             |
| BCD_hund_out | out       | std_logic_vector (3 downto 0)  |             |

## Signals

| Name   | Type                          | Description |
| ------ | ----------------------------- | ----------- |
| binary | std_logic_vector (9 downto 0) |             |

## Processes
- bin_2_bcd: ( binary, clk )

