# ESP8266 Hall Sensor RPM Counter with Web Interface

This project provides software for the ESP8266 microcontroller, implementing an RPM counter based on a Hall sensor with information display via a web interface. The project is aimed at beginners and teachers of technical disciplines who need a simple example of working with ESP8266, a web server, and processing signals from a Hall sensor.

## Description

The firmware allows counting the number of revolutions per minute (RPM) using a Hall sensor connected to the ESP8266 and displaying the result on a built-in web page. The web interface is easy to understand and suitable for educational purposes.

**Key features:**
- RPM counting using a Hall sensor
- Support for ESP8266 (e.g., NodeMCU, Wemos D1 Mini)
- Built-in HTTP web server for displaying current RPM readings
- Real-time RPM value updates

## Project Structure

```
ESP8266_Hall_Sensor/
│   platformio.ini          # PlatformIO configuration
│   README.md
│   
├───include/
│       README             # Description of the include folder
│       wifi_credentials.h         # Wi-Fi settings (do not add to git!)
│       wifi_credentials.h.example # Template for Wi-Fi settings
│       
├───lib/
│       README             # Description of the lib folder
│
├───src/
│       main.cpp           # Main firmware code
│
└───test/
        README             # Description of the test folder
```

## Hardware Requirements

- **ESP8266** (NodeMCU, Wemos D1 Mini or similar board)
- **Hall Sensor** (A3144, SS49E, OH49E or similar) - 2 pcs.
- **TM1637 Display** (4-digit 7-segment) - 2 pcs.
- **Connecting wires** (dupont or breadboard wires)
- **USB cable** for programming ESP8266
- **Breadboard** (optional, for easy assembly)

## Full Connection Diagram

### Pin layout on NodeMCU v1.0:
```
                    ESP8266 NodeMCU
                ┌─────────────────────┐
                │                     │
             A0 │ •                 • │ D0
             G  │ •                 • │ D1  <- Display 1 CLK
             VV │ •                 • │ D2  <- Display 1 DIO
             S3 │ •                 • │ D3  <- Display 2 CLK
             S2 │ •                 • │ D4  <- Display 2 DIO
             S1 │ •                 • │ 3V
             SC │ •                 • │ G
             S0 │ •                 • │ D5  <- Hall Sensor 1
             SK │ •                 • │ D6  <- Hall Sensor 2
             SD │ •                 • │ D7
             CMD│ •                 • │ D8
                │      [USB]          │
             3V │ •                 • │ RX
      VCC -> G  │ •                 • │ TX
             EN │ •                 • │ G
             RST│ •                 • │ G   
      GND -> VIN│ •                 • │ 3V  
                └─────────────────────┘
```

### TM1637 Display Connection Diagram

**First display (for sensor 1):**
```
ESP8266 NodeMCU          TM1637 Display #1
┌─────────────────┐      ┌─────────────────┐
│                 │      │                 │
│    3V3 (3.3V) ──┼──────┼── VCC           │
│                 │      │                 │
│    GND ─────────┼──────┼── GND           │
│                 │      │                 │
│    D1 (GPIO5) ──┼──────┼── CLK           │
│                 │      │                 │
│    D2 (GPIO4) ──┼──────┼── DIO           │
│                 │      │                 │
└─────────────────┘      └─────────────────┘
```

**Second display (for sensor 2):**
```
ESP8266 NodeMCU          TM1637 Display #2
┌─────────────────┐      ┌─────────────────┐
│                 │      │                 │
│    3V3 (3.3V) ──┼──────┼── VCC           │
│                 │      │                 │
│    GND ─────────┼──────┼── GND           │
│                 │      │                 │
│    D3 (GPIO0) ──┼──────┼── CLK           │
│                 │      │                 │
│    D4 (GPIO2) ──┼──────┼── DIO           │
│                 │      │                 │
└─────────────────┘      └─────────────────┘
```

### Hall Sensor Connection Diagram

**First Hall Sensor A3144 (for display 1):**
```
ESP8266 NodeMCU          Hall Sensor A3144 #1
┌─────────────────┐      ┌─────────────────┐
│                 │      │                 │
│    3V3 (3.3V) ──┼──────┼── VCC           │
│                 │      │                 │
│    GND ─────────┼──────┼── GND           │
│                 │      │                 │
│    D5 (GPIO14) ─┼──────┼── OUT           │
│                 │      │                 │
└─────────────────┘      └─────────────────┘
```

**Second Hall Sensor A3144 (for display 2):**
```
ESP8266 NodeMCU          Hall Sensor A3144 #2
┌─────────────────┐      ┌─────────────────┐
│                 │      │                 │
│    3V3 (3.3V) ──┼──────┼── VCC           │
│                 │      │                 │
│    GND ─────────┼──────┼── GND           │
│                 │      │                 │
│    D6 (GPIO12) ─┼──────┼── OUT           │
│                 │      │                 │
└─────────────────┘      └─────────────────┘
```

### Connection Summary Table:

| Component | ESP8266 Pin | Description |
|-----------|-------------|-------------|
| **Display 1** | | |
| TM1637 CLK1 | D1 (GPIO5) | Display 1 clock signal |
| TM1637 DIO1 | D2 (GPIO4) | Display 1 data |
| **Display 2** | | |
| TM1637 CLK2 | D3 (GPIO0) | Display 2 clock signal |
| TM1637 DIO2 | D4 (GPIO2) | Display 2 data |
| **Hall Sensors** | | |
| Hall Sensor 1 | D5 (GPIO14) | Hall sensor 1 output |
| Hall Sensor 2 | D6 (GPIO12) | Hall sensor 2 output |
| **Power** | | |
| VCC (all components) | 3V3 | +3.3V power |
| GND (all components) | GND | Common ground |

### Magnet Connection:
- Magnets should be at a distance of 1-10 mm from the corresponding Hall sensors
- When rotating objects, magnets should periodically approach the sensors
- Sensors trigger when the south pole of the magnet approaches (for A3144)

## Development Environment Setup

### Step 1: Installing Visual Studio Code
1. Go to the [official VS Code website](https://code.visualstudio.com/)
2. Download the version for your operating system
3. Run the installer and follow the instructions

### Step 2: Installing PlatformIO
1. Open VS Code
2. Press **Ctrl+Shift+X** (or go to Extensions on the sidebar)
3. In the search field, enter: `PlatformIO IDE`
4. Find the "PlatformIO IDE" extension by PlatformIO
5. Click **Install**
6. Wait for the installation to complete (may take several minutes)
7. Restart VS Code

### Step 3: Obtaining the Project

**Option A: Downloading ZIP Archive (for those without Git)**
1. Go to the [repository page](https://github.com/beecynical637/ESP8266_Hall_Sensor)
2. Click the green **Code** button
3. Select **Download ZIP**
4. Unpack the archive into a convenient folder
5. In VS Code: **File → Open Folder** → select the unpacked folder

**Option B: Cloning via Git (if Git is installed)**
```bash
git clone https://github.com/beecynical637/ESP8266_Hall_Sensor.git
```

## Wi-Fi Connection Setup

### Creating a Configuration File:
1. Open the project folder in VS Code
2. Go to the `include/` folder
3. Find the file `wifi_credentials.h.example`
4. **Copy** this file in the same folder
5. **Rename** the copy to `wifi_credentials.h`

### Editing Wi-Fi Settings:
1. Open the file `include/wifi_credentials.h`
2. Find the lines:
   ```cpp
   const char* ssid = "YOUR_WIFI_SSID";
   const char* password = "YOUR_WIFI_PASSWORD";
   ```
3. Replace with your data:
   ```cpp
   const char* ssid = "MyWiFiNetwork";           // Your Wi-Fi network name
   const char* password = "MyWiFiPassword";     // Wi-Fi password
   ```
4. Save the file (**Ctrl+S**)

**Important:**
- Use the exact network name (case-sensitive)
- ESP8266 only supports 2.4 GHz networks (not 5 GHz)

## Firmware Compilation and Upload

### Preparation:
1. Connect ESP8266 to the computer via USB cable
2. Ensure drivers are installed (usually installed automatically)

### Uploading via PlatformIO:
1. Open the project in VS Code
2. Find the PlatformIO icon on the left sidebar (ant head icon)
3. Click it, the PlatformIO panel will open
4. In the "PROJECT TASKS" section, find your project
5. Expand "env:nodemcuv2" (or the corresponding environment)
6. Click **"Upload"**

**Alternative upload methods:**
- Hotkeys: **Ctrl+Alt+U**
- Via command palette: **Ctrl+Shift+P** → "PlatformIO: Upload"
- Via bottom panel: right arrow button

### Monitoring the Process:
A terminal will appear at the bottom of VS Code with compilation and upload information:
```
Building .pio/build/nodemcuv2/src/main.cpp.o
Linking .pio/build/nodemcuv2/firmware.elf
Building .pio/build/nodemcuv2/firmware.bin
Uploading .pio/build/nodemcuv2/firmware.bin
...
Writing at 0x00000000... (100 %)
Wrote 261136 bytes (189516 compressed) at 0x00000000 in 16.7 seconds
Hash of data verified.
```

## Usage

### Checking Connection:
1. After uploading, open Serial Monitor:
   - **Ctrl+Shift+P** → "PlatformIO: Serial Monitor"
   - Or via PlatformIO panel → "Monitor"
2. Set speed to **115200 baud**
3. You will see the Wi-Fi connection process:
   ```
   Connecting to WiFi...
   WiFi connected!
   IP address: 192.168.1.100
   Web server started
   ```

### Checking Displays:
1. After successful firmware upload, both TM1637 displays should show "0"
2. When rotating magnets near the Hall sensors, RPM values should update on the corresponding displays
3. Display 1 shows RPM from sensor 1 (D5)
4. Display 2 shows RPM from sensor 2 (D6)

### Accessing the Web Interface:
1. Copy the IP address from Serial Monitor
2. Open a browser on any device in the same network
3. Enter the IP address in the address bar
4. Press Enter - a page with RPM readings from both sensors will open

### Testing Sensors:
1. Bring magnets close to the corresponding Hall sensors
2. Slowly rotate the magnets or move them back and forth
3. Serial Monitor should show messages about both sensors triggering
4. Displays and web page should update RPM values in real time for each sensor separately

## Possible Issues and Solutions

### ESP8266 does not connect to Wi-Fi:
- **Check settings:** ensure SSID and password in `wifi_credentials.h` are entered correctly
- **Network frequency:** ESP8266 only works with 2.4 GHz networks (not 5 GHz)
- **Distance:** bring ESP8266 closer to the router
- **Reboot:** press the RESET button on ESP8266

### TM1637 displays do not work:
- **Check connection:** ensure CLK and DIO wires are connected correctly
- **Power:** check 3.3V supply to VCC and GND connection
- **Connection quality:** ensure reliable contacts
- **Display compatibility:** some displays may require 5V power

### RPM not counting:
- **Check sensor connection:** ensure wires are connected correctly to pins D5 and D6
- **Test sensors:** connect a multimeter to sensor outputs - voltage should change when magnets approach
- **Magnet strength:** use stronger magnets or bring closer (1-5 mm)
- **Polarity:** try flipping the magnets (some sensors respond to a specific pole)

### Unable to upload firmware:
- **Port:** ensure ESP8266 is detected in the system (Device Manager in Windows)
- **Drivers:** install drivers for CH340 or CP2102 (depends on the board)
- **USB cable:** use a cable that supports data transfer (not just charging)
- **BOOT button:** on some boards, hold the BOOT/FLASH button during upload

### Compilation issues:
- **Update PlatformIO:** Tools → PlatformIO → Update All
- **Clean project:** PlatformIO → Clean
- **Check platformio.ini:** ensure the file is not corrupted
- **TM1637 library:** ensure the TM1637Display library is installed

## Additional Information

### TM1637 Display Characteristics:
- Supply voltage: 3.3V - 5V
- Number of digits: 4
- Type: 7-segment LED
- Interface: 2-wire (CLK + DIO)
- Brightness: adjustable (8 levels)

### A3144 Sensor Characteristics:
- Supply voltage: 4.5-24V (works from 3.3V)
- Output current: up to 25 mA
- Temperature range: -40°C to +85°C
- Sensitivity: ~35 Gauss

### Setup for Other Sensors:
If using a different Hall sensor, you may need to change the logic in the code:
- **Analog sensors** (e.g., SS49E): require connection to analog pin A0
- **Digital sensors with inverted logic**: may require signal inversion in the code

## License

The project is distributed under the MIT license. Use and modify for educational purposes!