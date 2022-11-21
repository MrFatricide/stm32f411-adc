# stm32f411-adc

### ADC input
---
### ADC
- Reads 12 bit ADC using `HAL_ADC_GetValue(&hadc1)`
- Pin used : **A2**
- `HAL_ADC_GetValue(&hadc1)` returns 32 bit
- Truncate 32 bit into 8 bits and save only smallest 16 bits

### SPI
- Pin used : `A4` => **Chip Select/NSS1**, `A5` => **Clk/SCLK1**, `A6' => **MISO**, `A7` => **MOSI**
