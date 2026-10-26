# Lab 8 Documentation

These are my screenshots, wiring photos, and recordings. The captions in the main README identify each test.

| File | What it shows |
|---|---|
| [UART with jumper](uart-with-jumper.png) | Repeated PING in Serial Monitor at 115200 baud. |
| [UART without jumper](uart-without-jumper.png) | No new PING appeared after disconnection; the visible lines were retained from the connected test. |
| [UART connected wiring photo](uart-connected-wiring.jpg) | GPIO17 (TX) connected to GPIO16 (RX) through the breadboard. |
| [UART disconnected wiring photo](uart-disconnected-wiring.jpg) | One end of the GPIO17-to-GPIO16 connection removed. |
| [UART demonstration, 27 seconds](uart-ping-demo.mp4) | PING before the jumper is removed, followed by no new output after clearing the monitor. |
| [UART disconnected recording, 12 seconds](uart-disconnected-demo.mp4) | Previous PING and reset messages remain, with no new PING during the disconnected test. |
| [Extra UART-disconnected capture at 9600](uart-without-jumper-9600.png) | Code and monitor at 9600; older PING lines remain above the reset text. |
| [I2C with OLED](i2c-with-oled-20261026.png) | Found device at 0x3C. |
| [I2C without OLED](i2c-without-oled-20261026.png) | No I2C devices found after the next reset. |
| [I2C connected wiring photo](i2c-connected-wiring.jpg) | My ESP32 and OLED setup for the connected test. |
| [I2C disconnected wiring photo](i2c-disconnected-wiring.jpg) | The OLED wires disconnected for the test without a module. |
| [I2C monitor photo](i2c-found-monitor-photo.jpg) | A photo of the monitor showing Found device at 0x3C. |
| [SPI with jumper](spi-with-jumper.png) | Sent 0xA5, received 0xA5. |
| [SPI without jumper](spi-without-jumper.png) | Sent 0xA5, received 0x00. |
| [SPI connected wiring photo](spi-connected-wiring.jpg) | My SPI setup with the loopback jumper connected. |
| [SPI disconnected wiring photo](spi-disconnected-wiring.jpg) | One end of the loopback connection removed. |
| [SPI connected recording, 15 seconds](spi-connected-demo.mp4) | Sent 0xA5, received 0xA5 repeatedly. |
| [SPI disconnected recording, 10 seconds](spi-disconnected-demo.mp4) | Sent 0xA5, received 0x00 repeatedly. |
| [UART code 9600 / monitor 115200](uart-9600-monitor-115200.png) | Startup text is visible, with no readable PING in the capture. |
| [UART code 9600 / monitor 9600](uart-9600-monitor-9600.png) | Readable PING with both baud rates set to 9600. |
| [MOLE desktop error](mole-signin-error.png) | Safari sign-in connection error on October 23 at 11:56 PM. |
| [MOLE mobile loading](mole-mobile-loading.png) | Dashboard loading indicators at 23:58. |

All eight test captures, my wiring photos, and the UART and SPI recordings are uploaded. The UART-without-jumper screenshot retains older PING lines; no new PING appeared after I disconnected the jumper. The [wiring diagram](../images/wiring.svg) labels the GPIO connections used by my sketches.
