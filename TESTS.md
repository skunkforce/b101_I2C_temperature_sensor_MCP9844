# communication test
## setup
Connect to b018 via I2C connector. Run the following micropython code:
```python
import machine
import utime
sda = machine.Pin(18)
scl = machine.Pin(19)
i2c=machine.I2C(1,sda=sda, scl=scl, freq=400000)
devices = i2c.scan()
if devices:
    for d in devices:
        print(hex(d))

while True:
    i2c.writeto(0x18,b'\x05')
    res=i2c.readfrom(0x18,2)
    print(hex(res[0]))
    print(hex(res[1]))
    utime.sleep(1)
    
```

Verify that the values in the temperature register at address 5 change with changing temperature.
## results
Values of the temperature register change when I change the temperature of the chip (by heating it with a hot air soldering tool).
