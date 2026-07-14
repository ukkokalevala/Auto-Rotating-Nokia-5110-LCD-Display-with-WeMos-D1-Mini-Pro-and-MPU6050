Auto-Rotating Nokia 5110 LCD Display with WeMos D1 Mini Pro and MPU6050
This project demonstrates a smartphone-style auto-rotating display using a WeMos D1 Mini Pro, a Nokia 5110 (PCD8544) LCD, and an MPU6050 accelerometer/gyroscope sensor. The MPU6050 continuously measures the orientation of the device by detecting gravity on the X and Y axes. The WeMos processes this data and automatically rotates the display content to remain upright, regardless of how the board is held.
The system supports four orientations: normal (0°), right (90°), upside down (180°), and left (270°). When the board is rotated, the software calculates the angle from the accelerometer readings and updates the LCD rotation accordingly. Text and graphics are automatically repositioned to fit the display in both horizontal and vertical modes, creating an intuitive user experience similar to that of a smartphone or tablet.
This project is an excellent introduction to motion sensing, I2C communication, display control, and orientation-based user interfaces. It can be expanded into portable instruments, digital badges, handheld games, GPS devices, weather stations, and other embedded systems that benefit from automatic screen rotation.
Nokia 5110 LCD
LCD Pin	Wemos Pin	Function
VCC	3.3V	Power
GND	GND	Ground
SCE	D6	Chip Select
RST	D7	Reset
D/C	D5	Data/Command
MOSI	D2	SPI Data
SCLK	D1	SPI Clock
LED	3.3V	Backlight (with resistor)
MPU6050 Sensor
Sensor Pin	Wemos Pin	Function
VCC	3.3V	Power
GND	GND	Ground
SDA	D3	I2C Data
SCL	D4	I2C Clock
AD0	GND	I2C Address (0x68)

1. Orientation Detection
The MPU6050 measures gravitational acceleration on the X and Y axes. The angle is calculated using:
angle = atan2(accY, accX) * 180 / PI;

2. Rotation Logic
The angle determines which quadrant the device is in:
-45° to 45°     → Normal (0°)
45° to 135°     → Right (90°)
135° to 180°    → Upside Down (180°)
-135° to -45°   → Left (270°)
3. Display Update
When orientation changes, display.setRotation() rotates the entire screen buffer. The layout adapts:

Horizontal: "Hello World!" on one line

Vertical: "Hello" and "World!" on two lines

4. Visual Feedback
A rotation indicator (N/R/U/L) appears in the corner, and a border frame resizes to fit the current orientation.
Libraries Required
#include <SPI.h>                 // Built-in
#include <Wire.h>                // Built-in
#include <Adafruit_GFX.h>        // Graphics library
#include <Adafruit_PCD8544.h>    // Nokia LCD driver
