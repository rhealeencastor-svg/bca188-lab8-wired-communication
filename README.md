# Laboratory Activity 8: Wired Communication

**Rhea Leen P. Castor**
2024-2802
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
| UART without jumper | No repeated PING | No new PING appeared after disconnection; older lines remained visible. | [115200 capture](documentation/uart-without-jumper.png), [extra 9600 capture](documentation/uart-without-jumper-9600.png) |
| I2C with OLED | OLED address detected | Found device at 0x3C. | [Uploaded](documentation/i2c-with-oled-20261026.png) |
| I2C without OLED | No devices detected | No I2C devices found. | [Uploaded](documentation/i2c-without-oled-20261026.png) |
| SPI with jumper | 0xA5 received | Received 0xA5. | [Uploaded](documentation/spi-with-jumper.png) |
| SPI without jumper | A value different from 0xA5 | Sent 0xA5, received 0x00. | [Uploaded](documentation/spi-without-jumper.png) |
| UART USB serial at 9600, monitor at 115200 | Unreadable PING output | Only startup text is visible; no readable PING appears in this capture. | [Uploaded](documentation/uart-9600-monitor-115200.png) |
| UART USB serial at 9600, monitor at 9600 | Readable PING | PING was readable with both baud rates set to 9600. | [Uploaded](documentation/uart-9600-monitor-9600.png) |

All eight test captures are included below, along with my wiring photos and UART and SPI recordings.

## Questions

**Why does UART need matching baud rates, while SPI uses a clock line?**

UART has no separate clock, so both sides need matching bit timing to read the data correctly. SPI uses SCK to synchronize the data.

**Why can't two devices with the same address share one I2C bus?**

Both devices would respond to the same address, so the controller could not select them separately. Their responses could also interfere with each other.

**Why is CS HIGH between SPI transfers?**

For active-low CS, HIGH deselects the device and ends the transfer. LOW selects it for the next transfer.

## Documentation

My screenshots, wiring photos, and recordings are saved in [documentation](documentation/).

<details>
<summary>1. UART with jumper — PING received</summary>

The monitor shows repeated PING lines. USB serial is set to 115200 baud, while Serial2 uses 9600 baud.

![UART loopback showing repeated PING at 115200 monitor baud](documentation/uart-with-jumper.png)

I connected **GPIO17 (TX)** to **GPIO16 (RX)** through the breadboard. The OLED is also visible in my setup.

![My UART setup with the GPIO17-to-GPIO16 connection joined on the breadboard](documentation/uart-connected-wiring.jpg)

In this **27-second recording**, PING appears before I remove the jumper. After I clear the monitor, no new PING appears.

https://github.com/user-attachments/assets/2284021b-3dc7-4259-aea7-40a2ec16baa5

[Download the UART demonstration](documentation/uart-ping-demo.mp4)

</details>

<details>
<summary>2. UART without jumper — no new PING</summary>

After I disconnected the jumper, no new PING lines appeared. The PING lines visible in this screenshot were left over from the earlier test with the jumper connected.

![UART without jumper at 115200 baud with older PING lines retained](documentation/uart-without-jumper.png)

I removed one end of the connection between GPIO17 and GPIO16.

![My UART setup with one jumper end disconnected](documentation/uart-disconnected-wiring.jpg)

This **12-second recording** shows the disconnected test. The previous PING and reset messages remain on screen, with no new PING appearing.

https://github.com/user-attachments/assets/7beb164e-2e7f-463b-9bc7-e64e15fe48ab

[Download the disconnected UART recording](documentation/uart-disconnected-demo.mp4)

I also took a capture with the jumper disconnected while both the code and monitor were set to **9600 baud**. Older PING lines remain visible above the reset text.

![Additional UART-disconnected capture with code and monitor at 9600 and retained PING lines above reset text](documentation/uart-without-jumper-9600.png)

</details>

<details>
<summary>3. I2C with OLED — address 0x3C found</summary>

The scanner detected the OLED at address **0x3C**. This test checks its I2C response, so the screen does not need to display anything.

![I2C scanner detecting the OLED at address 0x3C](documentation/i2c-with-oled-20261026.png)

My OLED was connected for this test. I used VCC to 3V3, GND to GND, SDA to GPIO21, and SCL to GPIO22.

![My ESP32 and OLED setup for the connected I2C test](documentation/i2c-connected-wiring.jpg)

I also photographed the monitor showing **Found device at 0x3C**.

![Photo of Serial Monitor showing the OLED detected at 0x3C](documentation/i2c-found-monitor-photo.jpg)

</details>

<details>
<summary>4. I2C without OLED — no devices found</summary>

After the next reset, the scanner printed **No I2C devices found**. The older 0x3C result is still visible above that reset.

![I2C scanner reporting no devices after the next reset](documentation/i2c-without-oled-20261026.png)

I disconnected the OLED wires for the test without a module.

![My I2C setup with the OLED wires disconnected](documentation/i2c-disconnected-wiring.jpg)

</details>

<details>
<summary>5. SPI with jumper — 0xA5 received</summary>

The monitor shows **Sent 0xA5, received 0xA5**, so the transmitted and received bytes matched.

![SPI loopback showing sent 0xA5 and received 0xA5](documentation/spi-with-jumper.png)

I connected **GPIO23 (MOSI)** to **GPIO19 (MISO)** through the breadboard for the loopback test.

![My SPI setup with the loopback jumper connected](documentation/spi-connected-wiring.jpg)

My **15-second recording** shows repeated **Sent 0xA5, received 0xA5**.

https://github.com/user-attachments/assets/c89417ab-446a-4cb1-8a8a-c663c0c2e55f

[Download the connected SPI recording](documentation/spi-connected-demo.mp4)

</details>

<details>
<summary>6. SPI without jumper — 0x00 received</summary>

With the MOSI-to-MISO jumper disconnected, the monitor shows **Sent 0xA5, received 0x00**. The received byte differed from 0xA5. This was my observed value; an unconnected MISO does not have one guaranteed value.

![SPI without jumper showing sent 0xA5 and received 0x00](documentation/spi-without-jumper.png)

I removed one end of the MOSI-to-MISO connection.

![My SPI setup with one jumper end disconnected](documentation/spi-disconnected-wiring.jpg)

My **10-second recording** shows repeated **Sent 0xA5, received 0x00**.

https://github.com/user-attachments/assets/a7458a6d-94c4-49a7-9632-43e6c22f771e

[Download the disconnected SPI recording](documentation/spi-disconnected-demo.mp4)

</details>

<details>
<summary>7. UART code 9600 / monitor 115200 — no readable PING</summary>

My code is set to **9600 baud**, while Serial Monitor is set to **115200 baud**. This capture shows startup text but no readable PING. The startup text is separate from the loopback output.

![UART code at 9600 and monitor at 115200 showing startup text without readable PING](documentation/uart-9600-monitor-115200.png)

</details>

<details>
<summary>8. UART code 9600 / monitor 9600 — readable PING</summary>

With my code and Serial Monitor both set to **9600 baud**, PING was readable again. This shows the difference between matching baud rates and the earlier 9600/115200 settings.

![UART code and Serial Monitor both at 9600 baud showing readable PING](documentation/uart-9600-monitor-9600.png)

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
