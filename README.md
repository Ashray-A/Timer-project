# Timer Project

A MicroPython-based digital timer display system designed for ESP32 microcontrollers with HUB75 RGB LED matrix panels. This project creates a smart timer that can display time, custom messages, and logos on LED matrix displays with cloud connectivity through AWS IoT.

## 🚀 Features

- **Digital Clock Display**: Real-time clock with custom pixel font rendering
- **HUB75 LED Matrix Support**: Full RGB color support for 16x32 LED panels
- **Custom Graphics**: Display logos, letters, and animations
- **AWS IoT Integration**: Cloud connectivity for remote control and updates
- **MQTT Communication**: Wireless message publishing and subscribing
- **WiFi Connectivity**: Connect to wireless networks for internet access
- **Modular Design**: Easy-to-extend codebase with separate modules

## 🛠 Hardware Requirements

- **ESP32 Development Board** (NodeMCU ESP-32S v1.1 or compatible)
- **HUB75 RGB LED Matrix Panel** (16x32 pixels recommended)
- **Hub75 Blaster PCB** (optional, for easier connections)
- **Power Supply** (5V, adequate amperage for LED panel)

### Pin Configuration

The project uses the following pin configuration for HUB75 connection:

| Function | ESP32 Pin |
|----------|-----------|
| Red1 | GPIO 27 |
| Blue1 | GPIO 26 |
| Green1 | GPIO 14 |
| Red2 | GPIO 12 |
| Blue2 | GPIO 25 |
| Green2 | GPIO 15 |
| Clock | GPIO 0 |
| Latch | GPIO 2 |
| Output Enable | GPIO 4 |
| Line Select A | GPIO 32 |
| Line Select B | GPIO 17 |
| Line Select C | GPIO 33 |
| Line Select D | GPIO 16 |
| Line Select E | GPIO 5 |

## 📁 Project Structure

```
Timer-project/
├── APIs/                    # Core LED matrix communication
│   ├── hub75.py            # HUB75 protocol implementation
│   └── matrixdata.py       # Matrix data management
├── AWS/                     # Cloud integration
│   ├── lambda_db.py        # Database Lambda functions
│   └── lambdaapi.py        # API Gateway Lambda handler
├── display-content/         # Content rendering
│   └── letters.py          # Alphabet and character definitions
├── logo-display/           # Logo and animation display
│   ├── displaylogo.py      # Logo display controller
│   └── logo.py             # Logo bitmap data
├── mqtt/                   # MQTT communication
│   ├── mqttconnect.py      # AWS IoT MQTT connection
│   ├── robust.py           # Robust MQTT client
│   ├── simple.py           # Simple MQTT client
│   ├── communication/      # MQTT pub/sub modules
│   │   ├── publisher.py    # Message publisher
│   │   └── subscribe.py    # Message subscriber
│   └── wifi_connect/       # WiFi connectivity
│       ├── esp32connecttoWifi.py  # WiFi connection handler
│       └── esp32led.py     # LED status indicators
├── time/                   # Time display modules
│   ├── local_time.py       # Local time management
│   └── numbers.py          # Number bitmap definitions
└── timer/                  # Timer functionality
    ├── localtime.py        # Timer implementation
    └── numbers.py          # Timer number graphics
```

## 🔧 Installation & Setup

### 1. Prerequisites

- **MicroPython**: Install MicroPython firmware on your ESP32
- **Required Libraries**: 
  - `ulab` (for numpy-like operations)
  - `machine` (ESP32 hardware control)
  - `umqtt.simple` or `umqtt.robust` (MQTT)

### 2. Hardware Setup

1. Connect your HUB75 LED matrix to the ESP32 according to the pin configuration above
2. Ensure proper power supply for both ESP32 and LED matrix
3. Double-check all connections before powering on

### 3. Software Setup

1. **Clone or download** this repository to your local machine
2. **Upload files** to your ESP32 using tools like:
   - Thonny IDE
   - ampy
   - WebREPL
   - VS Code with Pymakr extension

3. **Configure WiFi**: Update WiFi credentials in `mqtt/wifi_connect/esp32connecttoWifi.py`
4. **AWS IoT Setup** (optional): Configure your AWS IoT certificates in `mqtt/mqttconnect.py`

### 4. AWS IoT Configuration (Optional)

If you want to use cloud features:

1. Create an AWS IoT Thing
2. Generate certificates
3. Update the following in `mqtt/mqttconnect.py`:
   - `aws_endpoint`
   - Certificate files (`test-private.pem.key`, `test-certificate.pem.crt`)
   - Thing name

## 🎮 Usage

### Basic Time Display

```python
import time.local_time as timer
# The timer will automatically display current time on the LED matrix
```

### Display Custom Text

```python
import display-content.letters as display
# Use the letters module to display custom text
```

### Show Logos/Animations

```python
import logo-display.displaylogo as logo_display
# Displays animated logos on the matrix
```

### MQTT Communication

```python
import mqtt.mqttconnect as mqtt
client = mqtt.mqtt_connect()
# Now you can publish/subscribe to AWS IoT topics
```

## 🎨 Customization

### Adding New Characters

Edit `display-content/letters.py` to add new character bitmap definitions.

### Creating Custom Logos

1. Create bitmap arrays in `logo-display/logo.py`
2. Update `logo-display/displaylogo.py` to use your custom logo

### Modifying Display Colors

The project uses 3-bit color mapping:
- Black: 0 (0b000)
- Blue: 1 (0b001) 
- Green: 2 (0b010)
- Cyan: 3 (0b011)
- Red: 4 (0b100)
- Magenta: 5 (0b101)
- Yellow: 6 (0b110)
- White: 7 (0b111)

## 🌐 Cloud Features

- **Remote Control**: Send commands via AWS IoT
- **Time Synchronization**: Sync time from internet
- **Message Display**: Display messages sent from cloud
- **Status Monitoring**: Monitor device status remotely

## 🤝 Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 License

This project is open source. Feel free to use, modify, and distribute as needed.

## 🐛 Troubleshooting

### Common Issues

1. **Display not working**: Check power supply and pin connections
2. **WiFi connection fails**: Verify credentials and signal strength
3. **Time not displaying**: Check local time configuration
4. **AWS IoT connection issues**: Verify certificates and endpoint URL

### Debug Tips

- Use serial monitor to check for error messages
- Test individual modules separately
- Verify power supply adequacy for LED matrix

## 📧 Support

For questions or issues, please create an issue in this repository.

---

**Happy Making! 🎉**
