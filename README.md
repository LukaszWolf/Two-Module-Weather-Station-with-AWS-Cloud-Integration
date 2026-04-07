# Two-Module Weather Station with AWS Cloud Integration

An advanced IoT ecosystem designed for distributed weather monitoring. This system integrates local sensor networks with enterprise-grade cloud computing to provide real-time data visualization through both a physical touchscreen interface and a dedicated web application.

## Overview
This project was developed as a 5th-semester project at the **Silesian University of Technology**. It features a distributed architecture where an indoor central hub manages data from remote outdoor sensors and synchronizes it with the AWS Cloud.

### Key Features
* **Distributed Hardware:** Independent indoor hub and outdoor sensor module.
* **ESP-NOW Protocol:** Low-power local link ensuring months of battery life for the outdoor unit.
* **AWS IoT Integration:** Secure MQTT communication via X.509 certificates.
* **4" TFT Touch Interface:** Custom-built GUI for real-time monitoring and system setup.
* **Hybrid Mode:** Fully functional offline mode with automatic cloud synchronization upon reconnection.
* **Deep Sleep Management:** Optimized power consumption for battery-operated components.
* **Auto-Brightness:** Ambient light sensing via photoresistor for adaptive display intensity.

---

## Technical Stack

### Hardware
* **Indoor Hub (ESP32):**
    * **Sensors:** DS18B20 (Internal Temp), DS3231 RTC (Timekeeping).
    * **Storage:** LittleFS for GUI assets.
* **Outdoor Sensor (ESP32-C3 Mini):**
    * RISC-V architecture for high efficiency.
    * **Sensors:** BME280 (Temp, Humidity, Pressure), GUVA-S12SD (UV Index).

### Software & Cloud
* **Firmware:** C++ (VS Code + PlatformIO).
* **AWS Infrastructure:**
    * **IoT Core:** Secure MQTT Broker.
    * **Lambda:** Serverless data processing.
    * **Cognito:** User authentication and security.
    * **API Gateway:** Secure entry point managing traffic and **CORS** (Cross-Origin Resource Sharing) for cross-domain communication
    **S3:** Used for hosting the static files of the web application
* **Web App:** React-based dashboard with live charts and external API integration.

---

## System Configuration
The station features a built-in **Captive Portal**. On first boot or network change:
1.  The hub creates a local Access Point: `Meteo-Setup`.
2.  Users connect via a browser to securely provide home WiFi credentials.
3.  The device automatically switches to station mode and connects to AWS.

---

## Development Highlights
* **Memory Management:** Implemented "Lazy Loading" for graphics from LittleFS and used `PROGMEM` for static assets to eliminate RAM leaks.
* **Link Stability:** Integrated WiFi channel scanning to ensure ESP-NOW and WiFi coexist without interference.
* **Hardware Filtering:** Used ferrite beads and decoupling capacitors to remove screen flickering caused by WiFi power spikes.
