# stm32f411-adc

### ADC input
---
### ADC
- Reads 12 bit ADC using `HAL_ADC_GetValue(&hadc1)`
- Pin used : **A2**
- `HAL_ADC_GetValue(&hadc1)` returns 32 bit
- Truncate 32 bit into 8 bits and save only smallest 16 bits

### SPI
- Pin used : `A4` => **Chip Select/NSS1**, `A5` => **Clk/SCLK1**, `A6` => **MISO**, `A7` => **MOSI**
- Sends 1 Null bit, 3 Counter Bits, 12 ADC Value bits

### Error Correction
```c
// 8'b0xxx_yyyy - x: Counter , y: MSB of 12 bit data
msg_arr[1] += (counter << 4);

HAL_SPI_Transmit(&hspi1, (uint8_t *)&msg_arr, 1, 0xFF);

// Reset Counter
if(counter > 6)
  counter = 0;
else
  counter++;
 ```
 
 - SPI only transfer 8 bit at a time hence, 1st 8 bit transfer would be smallest 8-bit of the ADC value
 - next 8 bit transfer would be 1 null bit, 3 counter bit and 4 bit ADC value (MSB)
 - Once the counter reach 7, it would reset
