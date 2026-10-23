# Laboratory Activity 8: Wired Communication

**Rhea Leen P. Castor**

BCA188 - Programming For Internet of Things

I tested UART, I2C, and SPI using an ESP32 WROOM-32 and an I2C OLED.

## Pins and connections

| Signal | GPIO | Connection |
|---|---:|---|
| UART TX | 17 | GPIO16 |
| UART RX | 16 | GPIO17 |
| I2C SDA | 21 | OLED SDA |
| I2C SCL | 22 | OLED SCL |
| SPI SCK | 18 | No external connection for loopback |
| SPI MOSI | 23 | GPIO19 |
| SPI MISO | 19 | GPIO23 |
| SPI CS | 27 | No external connection for loopback |

I connected the OLED's VCC to **3V3** and GND to **GND**.

## Sketches

- [uart_loopback](uart_loopback/uart_loopback.ino): I sent PING through Serial2 at 9600 baud and checked the received bytes.
- [i2c_scanner](i2c_scanner/i2c_scanner.ino): I scanned for the OLED's I2C address.
- [spi_loopback](spi_loopback/spi_loopback.ino): I sent 0xA5 at 1 MHz, MSB first, using SPI mode 0.

I uploaded the sketches separately and used Serial Monitor at **115200 baud**, except for the matching 9600-baud test.

## Results

| Test | Expected | Observed |
|---|---|---|
| UART with jumper | PING once per second | PING appeared once per second. |
| UART without jumper | No repeated PING | No PING received. |
| I2C with OLED | OLED address detected | Found device at 0x3C. |
| I2C without OLED | No devices detected | No I2C devices found. |
| SPI with jumper | 0xA5 received | Received 0xA5. |
| SPI without jumper | A value different from 0xA5 | Received a value different from 0xA5. |
| Sketch at 9600, monitor at 115200 | Unreadable output | Output was unreadable. |
| Sketch at 9600, monitor at 9600 | Readable PING | PING was readable. |

## Questions

**Why does UART need matching baud rates, while SPI uses a clock line?**

UART has no separate clock, so both sides need matching bit timing to read the data correctly. SPI uses SCK to synchronize the data.

**Why can't two devices with the same address share one I2C bus?**

Both devices would respond to the same address, so the controller could not select them separately. Their responses could also interfere with each other.

**Why is CS HIGH between SPI transfers?**

For active-low CS, HIGH deselects the device and ends the transfer. LOW selects it for the next transfer.

## Documentation

My labeled wiring photo and Serial Monitor screenshots are pending upload. The screenshot of SPI without the jumper will show the received values.


## PROOF OF MOLE UNABLE TO OPEN:
<img width="1512" height="982" alt="Screenshot 2026-10-23 at 11 56 19 PM" src="https://github.com/user-attachments/assets/8496b7a2-c9c2-4cf4-ad57-0be5912a1186" />

<img width="922" height="2049" alt="image" src="https://github.com/user-attachments/assets/b7431090-f935-4f78-854f-7ff337ad03be" />
