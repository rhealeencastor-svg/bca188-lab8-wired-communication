# Lab 8 Documentation

These are my original screenshots. The captions in the main README identify each test.

| File | What it shows |
|---|---|
| [UART with jumper](uart-with-jumper.png) | Repeated PING in Serial Monitor at 115200 baud. |
| [UART without jumper](uart-without-jumper.png) | No new PING appeared after disconnection; the visible lines were retained from the connected test. |
| [Extra UART-disconnected capture at 9600](uart-without-jumper-9600.png) | Code and monitor at 9600; older PING lines remain above the reset text. |
| [I2C with OLED](i2c-with-oled.png) | Found device at 0x3C. |
| [I2C without OLED](i2c-without-oled.png) | No I2C devices found after the next reset. |
| [SPI with jumper](spi-with-jumper.png) | Sent 0xA5, received 0xA5. |
| [SPI without jumper](spi-without-jumper.png) | Sent 0xA5, received 0x00. |
| [UART code 9600 / monitor 115200](uart-9600-monitor-115200.png) | Startup text is visible, with no readable PING in the capture. |
| [UART code 9600 / monitor 9600](uart-9600-monitor-9600.png) | Readable PING with both baud rates set to 9600. |
| [MOLE desktop error](mole-signin-error.png) | Safari sign-in connection error on October 23 at 11:56 PM. |
| [MOLE mobile loading](mole-mobile-loading.png) | Dashboard loading indicators at 23:58. |

All eight test captures are uploaded. The UART-without-jumper screenshot retains older PING lines; no new PING appeared after I disconnected the jumper. The [wiring diagram](../images/wiring.svg) labels the GPIO connections used by my sketches.
