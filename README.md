NOTE: This is **archived** because the Electronics Workshop class we ported it for no longer uses this sensor. It may still work, but we use the [AS7341](https://github.com/AHSPC/AS7341_micropython) instead.

# AS726x 

Pure MicroPython driver for the AS726x RGB color sensor. Ported from Adafruit's CircuitPython driver.
(Tested on RPI Pico)

Depends on [our port of Adafruit's i2c_device CircuitPython library](https://github.com/AHSPC/adafruit_i2c_device_micropython_port).

Example usage:

```python
from machine import Pin, I2C
from time import sleep
from adafruit_as726x import AS726x_I2C

i2c = I2C(id=0, scl=Pin(1), sda=Pin(0))
print(i2c.scan())
print("hi")
as726x = AS726x_I2C(i2c_bus=i2c)
print("hi2")
print(as726x.temperature)
# as726x.indicator_led = True
# as726x.driver_led = True

as726x.conversion_mode = as726x.MODE_2

def graph_map(x):
    return min(int(x * 80 / 16000), 80)

# while True:
# Wait for data to be ready
# while not as726x.data_ready:
#     sleep(0.1)
#     print("(no data yet)")

print("\n")
print("V: " + graph_map(as726x.violet) * "=")
print("B: " + graph_map(as726x.blue) * "=")
print("G: " + graph_map(as726x.green) * "=")
print("Y: " + graph_map(as726x.yellow) * "=")
print("O: " + graph_map(as726x.orange) * "=")
print("R: " + graph_map(as726x.red) * "=")
sleep(0.5)
```


