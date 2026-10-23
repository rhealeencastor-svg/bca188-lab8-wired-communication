# Laboratory Activity 8: Wired Communication

**Rhea Leen Castor**

BCA188 - Programming For Internet of Things

UART, I2C, and SPI tests using an ESP32 WROOM-32 and an I2C OLED.

## Pins and connections

| Signal | GPIO | Connection |
|---|---:|---|
| UART TX | 17 | Connect to GPIO16 |
| UART RX | 16 | Connect to GPIO17 |
| I2C SDA | 21 | OLED SDA |
| I2C SCL | 22 | OLED SCL |
| SPI SCK | 18 | No external connection for loopback |
| SPI MOSI | 23 | Connect to GPIO19 |
| SPI MISO | 19 | Connect to GPIO23 |
| SPI CS | 27 | No external connection for loopback |

OLED VCC connects to **3V3**, and OLED GND connects to **GND**.

## Sketches

- [uart_loopback](uart_loopback/uart_loopback.ino): sends PING through Serial2 at 9600 baud and prints received bytes.
- [i2c_scanner](i2c_scanner/i2c_scanner.ino): scans for I2C devices once at startup.
- [spi_loopback](spi_loopback/spi_loopback.ino): sends 0xA5 at 1 MHz, MSB first, SPI mode 0.

Upload one sketch at a time. Use Serial Monitor at **115200 baud**, except during the baud-rate test. Unplug USB before changing wires.

## Results

| Test | Expected | Observed |
|---|---|---|
| UART with jumper | PING once per second | PING appeared once per second. |
| UART without jumper | PING stops | No PING received. |
| I2C with OLED | OLED address detected | Found device at 0x3C. |
| I2C without OLED | No devices detected | No I2C devices found. |
| SPI with jumper | Receive 0xA5 | Received 0xA5. |
| SPI without jumper | Receive a different value | Received a value different from 0xA5. |
| Sketch at 9600, monitor at 115200 | Unreadable output | Output was unreadable. |
| Sketch at 9600, monitor at 9600 | Readable PING | PING was readable. |

## Questions

**Why does UART need matching baud rates, while SPI uses a clock line?**

UART has no separate clock, so both sides need matching bit timing. SPI uses SCK to synchronize the data.

**Why can't two devices with the same address share one I2C bus?**

Both would respond to the same address, so the controller could not select them separately and their responses could interfere.

**Why is CS HIGH between SPI transfers?**

For active-low CS, HIGH deselects the device and ends the transfer. LOW selects it for the next transfer.

## Documentation

The labeled wiring photo and Serial Monitor screenshots for all eight tests will be uploaded here. The SPI screenshot without the jumper will show the actual received values.
