# addon-sku_rm0004
Home Assistant Community Add-on: Pi Rack Pro (RM0004) OLED Display

This is a add-on wrapper for the UCTRONICS Pi Rack Pro [SKU_RM0004](https://github.com/darkgrue/SKU_RM0004) OLED display driver.

## Prerequisites
The Home Assistant Operating System is a managed environment, which means `raspi-config` can’t be used to enable the I2C bus on a Raspberry Pi.
In order to use I2C devices you will have to follow the instructions on the [Common Tasks - Operating System](https://www.home-assistant.io/common-tasks/os/#enable-i2c) page to enable I2C for Home Assistant OS.

### I2C
Begin by enabling the I2C interface, add the following to the /boot/config.txt file:

```bash
dtparam=i2c_arm=on,i2c_arm_baudrate=400000
```

### Enable Shutdown Function
Add the following to the /boot/config.txt file:

```bash
dtoverlay=gpio-shutdown,gpio_pin=4,active_low=1,gpio_pull=up
```
