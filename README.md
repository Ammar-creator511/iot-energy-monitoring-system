# IoT Energy Monitoring System

## Project Overview
This is an ESP32-based IoT Energy Monitoring System that measures voltage, current, and power factor in real-time. The data is sent to a cloud dashboard for live monitoring and alerts.

## Hardware Components
- ESP32 Dev Module
- PZEM-004T Energy Meter
- Current Transformer (CT) Sensor
- 16x2 I2C LCD
- Power Supply Module

## Software & Technologies
- Embedded C++ (ESP32)
- Python (optional, for data processing)
- WiFi, MQTT / HTTP
- Cloud Dashboard (Blynk / Thingspeak / Web)

## Data Flow
Sensors → ESP32 → WiFi → Cloud Dashboard → User Alerts

## My Role
- Firmware development (sensor integration, WiFi, data handling)
- Hardware interfacing and testing
- Cloud dashboard setup

## Future Improvements
- Design PCB (KiCad / Altium)
- Mobile app integration
- AI-based energy consumption prediction
