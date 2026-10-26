# Laboratory Activity 8: Wired Communication

**Rhea Leen P. Castor**

BCA188 - Programming For Internet of Things

I tested UART, I2C, and SPI using an ESP32 and an I2C OLED.

## Pins and connections

| Signal | GPIO | Connection |
|---|---:|---|
| UART TX | 17 | GPIO16 |
| UART RX | 16 | GPIO17 |
| I2C SDA | 21 | OLED SDA |
| I2C SCL | 22 | OLED SCL |
| SPI SCK | 18 | Configured in the sketch; no external wire for loopback |
| SPI MOSI | 23 | GPIO19 |
| SPI MISO | 19 | GPIO23 |
| SPI CS | 27 | Configured in the sketch; no external wire for loopback |

I connected the OLED's VCC to **3V3** and GND to **GND**. The diagram shows the GPIO connections used by my sketches.

![UART, I2C OLED, and SPI GPIO connection diagram](images/wiring.svg)

## Sketches

- [uart_loopback](uart_loopback/uart_loopback.ino): sends PING through Serial2 at 9600 baud and prints the received bytes.
- [i2c_scanner](i2c_scanner/i2c_scanner.ino): scans for the OLED's I2C address once at startup.
- [spi_loopback](spi_loopback/spi_loopback.ino): sends 0xA5 at 1 MHz, MSB first, using SPI mode 0.

I uploaded the sketches separately and used Serial Monitor at **115200 baud**, except for the matching 9600-baud test.

## Results

| Test | Expected | Observed | Screenshot |
|---|---|---|---|
| UART with jumper | PING once per second | PING appeared once per second. | [Uploaded](documentation/uart-with-jumper.png) |
| UART without jumper | No repeated PING | PING text is visible in the capture; whether new lines stopped is awaiting confirmation. | [Uploaded; result needs confirmation](documentation/uart-without-jumper.png) |
| I2C with OLED | OLED address detected | Found device at 0x3C. | [Uploaded](documentation/i2c-with-oled.png) |
| I2C without OLED | No devices detected | No I2C devices found. | [Uploaded](documentation/i2c-without-oled.png) |
| SPI with jumper | 0xA5 received | Received 0xA5. | [Uploaded](documentation/spi-with-jumper.png) |
| SPI without jumper | A value different from 0xA5 | Received a value different from 0xA5. | Dedicated capture pending |
| Sketch at 9600, monitor at 115200 | Unreadable output | Output was unreadable. | Pending upload |
| Sketch at 9600, monitor at 9600 | Readable PING | PING was readable. | Pending upload |

Five Serial Monitor captures are included below. The UART disconnection result needs confirmation; the SPI-without-jumper and both baud-rate captures are still pending upload.

## Questions

**Why does UART need matching baud rates, while SPI uses a clock line?**

UART has no separate clock, so both sides need matching bit timing to read the data correctly. SPI uses SCK to synchronize the data.

**Why can't two devices with the same address share one I2C bus?**

Both devices would respond to the same address, so the controller could not select them separately. Their responses could also interfere with each other.

**Why is CS HIGH between SPI transfers?**

For active-low CS, HIGH deselects the device and ends the transfer. LOW selects it for the next transfer.

## Documentation

My original screenshots are saved in [documentation](documentation/).

<details>
<summary>1. UART with jumper — PING received</summary>

The monitor shows repeated PING lines. USB serial is set to 115200 baud, while Serial2 uses 9600 baud.

![UART loopback showing repeated PING at 115200 monitor baud](documentation/uart-with-jumper.png)

</details>

<details>
<summary>2. UART disconnection capture — result awaiting confirmation</summary>

This is my capture for the UART test after disconnecting the jumper. PING text is still visible. The image alone does not show whether these were retained lines or whether new lines continued, so the result is awaiting confirmation.

![UART disconnection capture at 115200 baud with PING text still visible](documentation/uart-without-jumper.png)

</details>

<details>
<summary>3. I2C with OLED — address 0x3C found</summary>

The scanner detected the OLED at address **0x3C**. This test checks its I2C response, so the screen does not need to display anything.

![I2C scanner detecting the OLED at address 0x3C](documentation/i2c-with-oled.png)

</details>

<details>
<summary>4. I2C without OLED — no devices found</summary>

After the next reset, the scanner printed **No I2C devices found**. The older 0x3C result is still visible above that reset.

![I2C scanner reporting no devices after the next reset](documentation/i2c-without-oled.png)

</details>

<details>
<summary>5. SPI with jumper — 0xA5 received</summary>

The monitor shows **Sent 0xA5, received 0xA5**, so the transmitted and received bytes matched.

![SPI loopback showing sent 0xA5 and received 0xA5](documentation/spi-with-jumper.png)

</details>

## MOLE access issues

I could not open the MOLE sign-in page in Safari on October 23 at 11:56 PM. My mobile dashboard also showed loading indicators.

<details>
<summary>Desktop sign-in error and mobile loading screen</summary>

**Desktop:** Safari reported that the server unexpectedly dropped the connection.

![MOLE sign-in connection error in Safari on October 23 at 11:56 PM](documentation/mole-signin-error.png)

**Mobile:** the dashboard showed loading indicators at 23:58.

![MOLE mobile dashboard with course areas showing Loading at 23:58](documentation/mole-mobile-loading.png)

</details>
