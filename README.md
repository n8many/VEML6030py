# VEML6030py
Python library for reading VEML6030 ambient light sensor from Sparkfun. https://www.sparkfun.com/products/15436

Written for the Raspberry Pi, but should work on other Linux based computers so long as they have an i2c bus you can 
connect to.

## Installation
1. Enable I2C on your computer
2. Install the smbus or smbus2 library (via pip). The library is compatible with both.
3. Add this library to your project. You can either...
    * Clone this repo to your project via:

       ```git clone https://github.com/n8many/VEML6030py.git```

   * Or download "veml6030.py" to have the code in your project base directory.

## Usage

If you cloned the repo to your project, add the CAP1203 object via:

```python
from VEML6030py.veml6030 import VEML6030
```

If you added the file directly to your project, then use:

```python
from veml6030 import VEML6030
```

Initializing a sensor can be as easy as:

```python
import smbus
bus = smbus.SMBus(1)  # For Raspberry Pi 
sensor = VEML6030(bus)
```

To get a reading from the sensor (in lux). You can call the following code:
```python
sensor.read_light()
```

Lux is always returned as a float and is converted back to an int for storage on the sensor.


### Supporting Classes

#### Gain
The ```Gain``` class is used for setting the Sensitivity setting. Available settings are from x1/8-x2 (default x1).

#### IntegrationTime
The ```IntegrationTime``` class is used to change the integration time on the sensor. Available settings are from 
25ms to 800ms

##### NOTE: 
Lux is calculated via the current gain and integration time. Changing gain and integration time should not affect 
the output lux, but will affect the resolution of the reading.

#### ProtectNum
The ```ProtectNum``` class is used for setting the persistence protection setting. Options are 1, 2, 4, 8.

#### PowerSaveMode
The ```PowerSaveMode``` class is used when changing the mode for the power saving setting. More details on what each 
mode does (in combination with integration time and gain) can be found on page 9 of the datasheet.

#### Interrupt
The ```Interrupt``` class is used when detecting which interrupt triggered. These interrupts can be configured by setting 
the low and high interrupt thresholds. It is an ```IntFlag``` class with the available options of:

* Interrupt.0 (none, 0)
* Interrupt.Low (Low threshold, 2)
* Interrupt.High (High threshold, 1)

## History

4/25/20 - Creation

## Credits
Most of this code is being translated from the original Sparkfun library here: 
https://github.com/sparkfun/SparkFun_Ambient_Light_Sensor_Arduino_Library

## License
This is under the MIT License