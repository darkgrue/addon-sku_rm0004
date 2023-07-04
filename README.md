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
The `dtoverlay=gpio-shutdown` method for shutdown is not compatible with Home Assistant Operating System (hassio).

Instead, use the [Home Assistant Raspberry Pi GPIO custom integration](https://github.com/thecode/ha-rpi_gpio).

Add the following sensor to your HA configuration:

```yaml
  # https://github.com/thecode/ha-rpi_gpio
  # HACS Raspberry Pi GPIO Integration 
  binary_sensor:
    - platform: rpi_gpio
      sensors:
        - port: 4               # pin 7
          name: "HA Safe Shutdown Button"
          unique_id: "ha_safe_shutdown_button"
          bouncetime: 80
          invert_logic: true    # Active low
          pull_mode: UP         # pull-up resistor
```
Call the service 'hassio.host_shutdown'.
