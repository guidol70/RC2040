# GPIO pin definitions 
### and where to change them 

The RC2040 was never intended to be board agnostic, but people have asked so....

## Where the GPIO pins are defined. 
Yes this should all be in one place....

## SD Card
the pins are defined in
void spi0_dma_isr();

  .miso_gpio = 4, // GPIO number (not pin number)<br>
  .mosi_gpio = 3,<br>
  .sck_gpio = 2,<br>
  
and the spi module used by these pins must be changed too  
  .hw_inst = spi0
  
and in 

static sd_card_t sd_cards[]<br><br>
  .ss_gpio = 5,<br>
  .card_detect_gpio = 22,   // Card detect



## Sound
The speaker pins, have two defines near the top of RC2040.c<br> 
#define soundIO1 15<br>
#define soundIO2 14<br>

These must be on the same PWMslice

## 8 bit Port
The pins for the 8 bit port are defined in an array near the top of RC2040.c

uint8_t PIOAp[]={16,17,18,19,20,21,26,27};

## Serial
near the top of the RC2040.c
/* Real UART setup*/<br>

#define UART_TX_PIN 0<br>
#define UART_RX_PIN 1<br>

these ofcourse need to be valid Tx/Rx pins to work. and<br> 
#define UART_ID uart0<br>

needs to point to the serial module used.

