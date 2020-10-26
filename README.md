# SHT3x
Driver for the range of SHT3x temperature and humidity sensors.

## Usage
After connecting an SHT3x sensor to your microcontroller via I2C and initialising the bus using Cube you can use this
library to interact with the sensor as shown in the following example. I2C must be running in standard or fast mode and
clock stretching must be enabled:
```c
// Create the handle for the sensor.
sht3x_handle_t handle = {
    .i2c_handle = &hi2c1,
    .device_address = SHT3X_I2C_DEVICE_ADDRESS_ADDR_PIN_LOW
};

// Initialise sensor (tests connection by reading the status register).
if (!sht3x_init(&handle)) {
    printf("SHT3x access failed.\n\r");
}

// Read temperature and humidity.
float temperature, humidity;
sht3x_read_temperature_and_humidity(&handle, &temperature, &humidity);
printf("Initial temperature: %.2fC, humidity: %.2f%%RH\n\r", temperature, humidity);

// Enable heater for two seconds.
sht3x_set_header_enable(&handle, true);
HAL_Delay(2000);
sht3x_set_header_enable(&handle, false);

// Read temperature and humidity again.
sht3x_read_temperature_and_humidity(&handle, &temperature, &humidity);
printf("After heating temperature: %.2fC, humidity: %.2f%%RH\n\r", temperature, humidity);
```

## Supported Platforms
STM32L0 and STM32L4 are supported. The HAL header includes for other platforms may be added in `sht3x.h`.