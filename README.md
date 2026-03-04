# ESP32 Residential IoT System

## Overview

This project implements a **residential IoT system using the ESP32 and ESP-IDF framework**.  
The device connects to a WiFi network, hosts an **embedded web server**, and allows users to monitor environmental data and control home devices through a **web interface**.

The system collects **temperature and humidity data from a DHT sensor** and allows the control of multiple **GPIO-based devices** (such as lights, relays, or appliances).

The project was designed as a learning exercise in **embedded systems, IoT architecture, and ESP-IDF development**.

---

## Features

- WiFi connectivity using **ESP-IDF WiFi stack**
- Embedded **HTTP Web Server**
- Web dashboard for device control
- Temperature and humidity monitoring using **DHT sensor**
- Control of multiple GPIO devices
- Modular firmware architecture
- FreeRTOS-based task management

---

## Hardware Requirements

- **ESP32 development board**
- **DHT temperature and humidity sensor**
- Up to **3 controllable devices** (e.g., relays or LEDs)
- WiFi network
- Computer or smartphone with a web browser

---

## System Architecture

The firmware is organized into multiple modules that handle different parts of the system.

### WiFi Manager (`wifi_app`)

Responsible for:

- Connecting to the configured WiFi network
- Managing connection events
- Starting the HTTP server once the connection is established

---

### HTTP Server (`http_server`)

Provides the web interface used to interact with the system.

Main functions:

- Serving static web files (HTML, CSS, JavaScript)
- Handling API requests
- Returning sensor data
- Receiving commands to toggle devices

The web interface is located in:

```
main/webpage/
```

Files included:

- `index.html`
- `app.css`
- `app.js`
- `jquery`

---

### Sensor Module (`dht`)

Handles the **DHT temperature and humidity sensor**.

Responsibilities:

- Reading environmental data
- Running as a periodic FreeRTOS task
- Providing sensor values to the web interface

---

### Device Control (`devices`)

Controls the **GPIO devices connected to the ESP32**.

Capabilities:

- Configure GPIO pins
- Toggle device state
- Receive commands from the HTTP server

Three devices are supported by default:

- Device 1
- Device 2
- Device 3

These can be connected to **relays, LEDs, or other actuators**.

---

### Task Management

The firmware uses **FreeRTOS tasks** to run components independently:

| Task | Description |
|-----|-------------|
| WiFi Task | Handles WiFi connection and events |
| HTTP Server Task | Serves web interface |
| DHT Task | Periodically reads sensor values |
| Device Task | Controls GPIO devices |

---

## Project Structure

```
esp-residential-iot
│
├── CMakeLists.txt
├── main/
│   │
│   ├── main.c
│   ├── wifi_app.c
│   ├── wifi_app.h
│   ├── http_server.c
│   ├── http_server.h
│   ├── devices.c
│   ├── devices.h
│   ├── dht.c
│   ├── dht.h
│   ├── rgb_led.c
│   ├── rgb_led.h
│   ├── tasks_common.h
│   │
│   └── webpage/
│       ├── index.html
│       ├── app.css
│       ├── app.js
│       └── jquery-3.3.1.min.js
```

---

## How It Works

1. The ESP32 initializes NVS and system components.
2. The device connects to the configured WiFi network.
3. Once connected, the **HTTP server is started**.
4. The user accesses the ESP32 through a web browser.
5. The web interface allows:
   - monitoring temperature and humidity
   - toggling connected devices.

---

## Building the Project

This project uses the **ESP-IDF build system**.

### Requirements

- ESP-IDF installed
- Python environment configured
- ESP32 toolchain

### Build

```bash
idf.py build
```

### Flash

```bash
idf.py -p PORT flash
```

### Monitor

```bash
idf.py monitor
```

---

## Accessing the Web Interface

After flashing and connecting to WiFi:

1. Check the ESP32 IP address in the serial monitor.
2. Open a web browser.
3. Enter the IP address of the ESP32.

Example:

```
http://192.168.1.100
```

---

## Possible Improvements

Future improvements may include:

- MQTT integration
- Home Assistant compatibility
- OTA firmware updates
- More sensor support
- Authentication for the web interface
- Mobile-friendly dashboard

---

## License

MIT
