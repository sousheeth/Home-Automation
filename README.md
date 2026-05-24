# Home-Automation
A decentralized system architecture blueprint for an IoT smart home network. Features real-time telemetry ingestion using MQTT over TLS, edge-processing configurations for ESP32 microcontrollers, and a containerized time-series database pipeline (InfluxDB) for automated climate and energy optimizations.
## ⚙️ System Architecture Overview
The system is architected around a **Publish-Subscribe network topology** designed to decouple data generation (sensors) from data consumption (dashboards/actuators). 

* **Edge Devices (Peripherals):** Low-power **ESP32 microcontrollers** programmed to handle hardware-interrupt-driven sensor sampling (Temperature, Humidity, Motion) and payload serializing.
* **Central Gateway Hub:** A **Raspberry Pi 4** node executing a local containerized ecosystem acting as the local processing edge.
* **Message Broker:** An **MQTT Broker (Mosquitto)** facilitating low-overhead, asynchronous, real-time message routing with Quality of Service (QoS 1) guarantees.
* **Database Tier:** A specialized **InfluxDB Time-Series Database** optimal for high-frequency telemetry ingestion and minimal storage degradation.

## 🛠️ Tech Stack & Protocols
* **Hardware Frameworks:** ESP32-WROOM-32, Raspberry Pi 4 Model B, Shelly Actuators.
* **Communication Protocols:** MQTT (Message Queuing Telemetry Transport), HTTP/REST, WebSockets.
* **Data Serialization:** JSON / Protocol Buffers.
* **Storage Tier:** InfluxDB (Time-Series Data), SQLite (Local device state persistence).
* **Languages Represented in Configurations:** Python, C++ (Embedded Arduino), JSON.

## 🔒 Security & Resilience Design
1.  **Transport Layer Security:** All MQTT communication over port 8883 utilizing TLS/SSL certificate bridging to prevent middle-person data tampering.
2.  **Network Isolation:** Edge devices run on an isolated, local VLAN with zero outbound internet routing capabilities unless proxied through the Central Hub.
3.  **Graceful Degradation:** Microcontrollers feature local non-volatile memory (NVM) caching to store up to 4 hours of telemetry data in the event of local Wi-Fi disconnection.

## 📊 Sample Data Payload Structure
Devices publish metrics as minified JSON payloads to minimize transmission bandwidth over network infrastructure:

```json
{
  "timestamp": "2026-05-23T23:42:00Z",
  "device_id": "ESP32_LIVING_ROOM_TEMP",
  "metrics": {
    "temperature_celsius": 22.4,
    "humidity_percentage": 45.2
  },
  "network_rssi_dbm": -65
}
