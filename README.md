# micropython-ssd1306-oled-1.3-drivers
MicroPython SSD1306 1.3" OLED driver, I2C and SPI interfaces

![demo](https://github.com/Eivs/micropython-ssd1306-oled-1.3-drivers/raw/main/demo.jpg)


# How to use

```python
from machine import Pin, I2C
import ssd1306

i2c = I2C(scl=Pin(22), sda=Pin(21))


def init_oled():
    global oled
    oled_width = 128
    oled_height = 64
    oled = ssd1306.SSD1306_I2C(oled_width, oled_height, i2c)
    oled.contrast(100)
    oled.invert(0)
    oled.rotate(True)
    oled.fill(0)
    
def scan_devices():
  print('Scan i2c bus...')
  devices = i2c.scan()

  if len(devices) == 0:
      print("No i2c device !")
  else:
      print('i2c devices found:',len(devices))
      for device in devices:  
          print("Decimal address: ",device," | Hexa address: ",hex(device))
      init_oled()
      return True

if scan_devices():
    oled.rect(0, 0, 128, 64, 1)
    oled.fill_rect(2, 2, 30, 30, 1)
    oled.fill_rect(4, 4, 26, 26, 0)
    oled.vline(9, 8, 22, 1)
    oled.vline(16, 2, 22, 1)
    oled.vline(23, 8, 22, 1)
    oled.fill_rect(27, 24, 1, 2, 1)
    oled.text('MicroPython', 38, 2, 1)
    oled.text('SSD1306', 38, 14, 1)
    oled.text('OLED 128x64', 38, 26, 1)
    oled.text('JMD 1.3 Inch', 18, 50, 1)
    oled.show()
```
