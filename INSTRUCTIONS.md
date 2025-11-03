# Smart Parking Monitor System

## Overview
This is an ESP32-based parking slot monitoring system that uses ultrasonic sensors to detect vehicle presence and indicates availability using LEDs.

## Hardware Requirements
- 1x ESP32 Development Board
- 3x HC-SR04 Ultrasonic Sensors
- 6x LEDs (3 Red, 3 Green)
- 6x 220Ω Resistors
- Breadboard and jumper wires
- USB cable for programming

## Software Requirements
- Arduino IDE (1.8.x or later) OR PlatformIO
- ESP32 Board Support Package

## Installation

### Option 1: Arduino IDE
1. Install Arduino IDE from https://www.arduino.cc/en/software
2. Add ESP32 board support:
   - Go to File → Preferences
   - Add to "Additional Board Manager URLs": 
     `https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json`
   - Go to Tools → Board → Boards Manager
   - Search for "esp32" and install "esp32 by Espressif Systems"
3. Open `parking_monitor.ino`
4. Select board: Tools → Board → ESP32 Arduino → ESP32 Dev Module
5. Select port: Tools → Port → (your ESP32 port)
6. Click Upload

### Option 2: PlatformIO
1. Install PlatformIO IDE or PlatformIO Core
2. Navigate to project directory
3. Run: `pio run --target upload`
4. Monitor serial output: `pio device monitor`

## Circuit Connections
See `circuit_diagram.txt` for detailed wiring instructions.

## How It Works
1. Each parking slot has one ultrasonic sensor and two LEDs (red and green)
2. The sensor measures distance every second
3. If distance < 10 cm: RED LED turns on (slot occupied)
4. If distance >= 10 cm: GREEN LED turns on (slot available)
5. Serial monitor displays real-time distance readings

## Monitoring
Open Serial Monitor at 115200 baud to see distance readings:
```
Slot 1: 25 cm  |  Slot 2: 8 cm  |  Slot 3: 15 cm
```

## Troubleshooting
- **No readings**: Check sensor VCC/GND connections
- **Erratic readings**: Ensure sensors are mounted firmly
- **LEDs not working**: Verify GPIO connections and resistor values
- **Upload fails**: Press and hold BOOT button during upload

## Customization
To adjust detection threshold, modify line in `controlLEDs()` function:
```cpp
if (distance > 0 && distance < 10) {  // Change 10 to desired threshold
```

## License
Open source - feel free to modify and distribute.
