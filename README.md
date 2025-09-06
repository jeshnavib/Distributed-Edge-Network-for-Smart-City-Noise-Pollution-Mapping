# 🌍 GeoMotion Tracker

The **GeoMotion Tracker** is an innovative IoT-based telemetry system designed to monitor **environmental conditions, motion dynamics, and geographic location in real-time** for high-altitude payloads such as weather balloons and aerospace experiments.  

The system leverages the **ESP32 microcontroller** as the master node, interfaced with multiple sensors for motion, environment, and GPS data. It transmits data via **WiFi** to a **Raspberry Pi ground station**, which processes, logs, and visualizes telemetry in real-time through a Python-based dashboard.  

---

## 📌 Abstract
The GeoMotion Tracker employs:
- **ESP32 microcontroller** (master node)  
- **MPU6050 (6-axis motion sensor)** → acceleration & angular velocity  
- **BMP280 (environmental sensor)** → temperature, pressure, and altitude  
- **NEO-6M GPS module** → precise location tracking  

Unlike traditional, costly telemetry systems, this project uses **WiFi for communication** with a **Raspberry Pi (slave node)**. The Pi receives, logs, and visualizes telemetry data using Python, enabling effective monitoring.  

The system is:  
✔️ **Cost-effective**  
✔️ **Scalable**  
✔️ **Modular**  

Applications include environmental monitoring, aerospace research, and educational experiments. Future enhancements include **cloud integration** and **advanced analytics**.  

---

## 📖 Introduction
High-altitude missions (weather balloons, atmospheric research, aerospace experiments) require telemetry systems to monitor environmental and payload dynamics. Traditional solutions are:  
❌ Expensive  
❌ Bulky  
❌ Infrastructure-heavy  

**GeoMotion Tracker** solves these by offering an **IoT-based, WiFi-enabled telemetry system** that is affordable, scalable, and high-performance.  

- **ESP32** handles sensor interfacing and WiFi communication.  
- **Sensors used**:  
  - MPU6050 → motion tracking  
  - BMP280 → environmental monitoring  
  - NEO-6M GPS → geolocation  
- **Raspberry Pi** serves as ground station for **data processing, logging, and visualization**.  

---

## ⚙️ Components Used

### 1. ESP32 (Master Node)
- **Role**: Collects sensor data & transmits via WiFi  
- **Features**: Dual-core processor, integrated WiFi + Bluetooth, multiple interfaces (I2C, SPI, UART, ADC), low-power modes  
- **Specs**:  
  - Operating Voltage: 3.3V  
  - GPIO: 36 pins  
  - Flash: 4MB  
  - ADC: 12-bit resolution  

### 2. MPU6050 – Motion Sensor
- **Role**: 6-axis motion tracking (accel + gyro)  
- **Specs**:  
  - Accelerometer: ±2g to ±16g  
  - Gyroscope: ±250°/s to ±2000°/s  
  - Communication: I2C (0x68)  

### 3. BMP280 – Environmental Sensor
- **Role**: Measures temperature, pressure, calculates altitude  
- **Specs**:  
  - Temp: -40°C to +85°C  
  - Pressure: 300–1100 hPa  
  - Altitude: Derived from pressure  
  - Communication: I2C/SPI  

### 4. NEO-6M GPS Module
- **Role**: Real-time GPS (lat, long, alt, timestamp)  
- **Specs**:  
  - Accuracy: 2.5m  
  - Update rate: 5 Hz  
  - Communication: UART (9600 baud)  

### 5. Raspberry Pi (Slave Node)
- **Role**: Ground station for receiving, logging, visualization  
- **Features**:  
  - OS: Raspberry Pi OS  
  - Connectivity: WiFi  
  - Programming: Python (Tkinter, Flask, Matplotlib)  

### 6. Connecting Wires & Breadboard
- Jumper wires (M-M, M-F)  
- Breadboard (400+ tie points)  

### 7. Power Supply
- ESP32: 3.7V Li-Po battery (1000mAh+) with regulator  
- Raspberry Pi: 5V, 2.5A/3A adapter  

### 8. Software Components
- **ESP32**: Arduino C++ (Arduino IDE)  
  - Libraries: `WiFi`, `Wire`, `Adafruit_BMP280`, `MPU6050`, `TinyGPS++`  
- **Raspberry Pi**: Python  
  - Libraries: `socket`, `csv`, `matplotlib`, `tkinter`  

---

## 🔄 Working of GeoMotion Tracker

### Step 1: System Initialization
- ESP32: Connects to WiFi & initializes sensors  
- Raspberry Pi: Runs Python UDP server to listen for data  

### Step 2: Sensor Data Collection
- MPU6050 → accel & gyro data  
- BMP280 → temp, pressure, altitude  
- NEO-6M GPS → coordinates & timestamp  
- ESP32 monitors battery voltage  

### Step 3: Data Processing & Transmission
- ESP32 formats data into CSV-like string  
- Sends data via UDP packets every second  

### Step 4: Data Reception & Processing
- Raspberry Pi receives, parses, and validates data  
- Logs into CSV for analysis  
- Alerts on threshold breaches (e.g., high temp, low battery)  

### Step 5: Real-Time Visualization
- Python dashboard with `matplotlib` & `tkinter`  
- Displays graphs for sensors + GPS mapping  
- Optional: Flask web dashboard / ThingSpeak cloud upload  

### Step 6: Continuous Monitoring
- Loop continues until mission ends  
- Supports future enhancements (cloud, alerts, quaternion motion analysis)  

---

## 🛠 Practical Considerations
- **WiFi Range**: ~100–200m (extendable with antenna)  
- **Power**: Li-Po battery capacity critical for mission duration  
- **Enclosure**: Weather-resistant casing required  
- **Error Handling**: Handles WiFi drops, sensor failures, GPS loss  

---

## 🚀 Applications
- Environmental monitoring  
- Aerospace research  
- Educational experiments  

---

## 🔮 Future Enhancements
- Cloud-based data storage  
- Advanced motion analytics  
- More sensor integrations  

---

## 📷 Block Diagram (Suggested)
```text
ESP32 (Master Node)
   ├── MPU6050 (Motion)
   ├── BMP280 (Environment)
   ├── NEO-6M GPS
   └── WiFi Transmission
           ↓
Raspberry Pi (Slave Node)
   ├── UDP Socket (Python)
   ├── Data Logging (CSV)
   └── Real-Time Dashboard
