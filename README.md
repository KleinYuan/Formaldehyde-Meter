# Formaldehyde-Meter
Home Made Formaldehyde (HCHO) Meter for Your New House/Office


# Hardware

- [X] DFRobot Gravity: HCHO Sensor ([69.61 CAD on Digikey](https://www.digikey.ca/en/products/detail/dfrobot/SEN0231/7087195))
- [X] Arduino MKR WiFi 1010 ([47~69 CAD on Amazon](https://www.amazon.ca/Arduino-MKR-WiFi-1010-ABX00023/dp/B07FYFF5YZ))

# Software

Update your wifi name and password at the following lines:

```
char ssid[] = "";             //  your network SSID (name) between the " "
char pass[] = "";      // your network password between the " "
```

Connect the two boards with the following mapping:

```
HCHO Sensor S --> MKR A2
HCHO Sensor + --> MKR 3.3V (VCC)
HCHO Sensor - --> MKR GND
```

And set HCHO Sensor to DAC mode (due to SoftwareSerial won't work on this chip unless you want to custom the library).

Burn the [code.ino](code.ino) into the Arduino board and then it will keep sending the HCHO value to it's local IP port 80:

![example](example.png)


# Details

This project is basically following the below two links:

- [X] https://wiki.dfrobot.com/Gravity__HCHO_Sensor_SKU__SEN0231
- [X] https://docs.arduino.cc/tutorials/mkr-wifi-1010/hosting-a-webserver

Q&As:
1. Why use DAC mode ?
   - The DFRobotHCHOSensor Arduino Library does not support MKR chip well, mainly due to the SoftwareSerial.h

2. Why use 3.3V instead of 5V?
   - MKR also outputs 5V however, when I tested it, I found the output number doesn't look correct. I assume the cause is that the voltage is not stable at 5V as the MKR input 3.3V. Besides, the Gravity sensoe DAC mode is quite sensitive to the voltage value. These combined leads me to use 3.3V.
