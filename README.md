# 🌱 Smart Greenhouse Monitoring System  
### ESP32 + Adafruit IO (MQTT) + OpenWeather API

## 📌 Overview

This project implements a Smart Greenhouse Monitoring System using an ESP32 microcontroller.  
The system combines local environmental sensing with cloud connectivity and sustainability-based decision logic.

It monitors greenhouse temperature, humidity, soil moisture, and light levels, publishes the data to Adafruit IO using MQTT, and retrieves live San Antonio weather data using the OpenWeather API.

Instead of displaying raw data only, the system applies decision rules to generate real-time alerts and recommendations.

---

## 🚀 Features

### 🌡 Greenhouse Monitoring
- Temperature (DHT22, converted to °F)
- Humidity
- Soil moisture (0–100%)
- Light level (0–100%)

### ☁ Cloud Integration
- MQTT publishing to Adafruit IO dashboard
- Remote LED control via MQTT subscription
- Live outdoor weather retrieval using OpenWeather API
- JSON parsing with ArduinoJson

### 📟 LCD Smart Display (Cycles Every 2 Seconds)

**Screen 1**
- Top: GH Temp + Humidity  
- Bottom: SA Temp + Humidity  

**Screen 2**
- Top: Light (%)  
- Bottom: Moisture (%)  

**Screen 3**
- Top: "SA Weather"  
- Bottom: Weather condition (Clear, Clouds, Rain, etc.)

Alert messages override the normal cycle when triggered.

---

## 🌿 Sustainability Decision Logic

The system converts sensor readings into actionable decisions:

- **Water Conservation Rule**  
  If moisture < 30% → Display “Needs Water” and turn LED ON.

- **Overwatering Rule**  
  If moisture > 80% → Display “Too Wet” and turn LED OFF.

- **Heat Stress Rule**  
  If greenhouse temperature > 85°F → Display “Heat Risk” and recommend shade/ventilation.

These rules promote more sustainable plant care practices.

---

## 🔧 Hardware Components

- ESP32 Dev Module  
- DHT22 Temperature/Humidity Sensor  
- Soil Moisture Sensor (simulated via potentiometer in Wokwi)  
- Photoresistor Light Sensor Module  
- 16x2 I2C LCD  
- LED (alert indicator)

---

## 🧠 System Architecture

```
Greenhouse Sensors (DHT22, Moisture, Light)
                ↓
              ESP32
        ↙                 ↘
     LCD Output        MQTT → Adafruit IO Dashboard
                               ↑
                     OpenWeather API (HTTP + JSON)
```

---

## 🔄 Timing Configuration

- Greenhouse sensor publish interval: **10 seconds**
- OpenWeather API refresh interval: **30 seconds**
- LCD display cycle interval: **2 seconds**

---

## 📊 Adafruit IO Feeds Used

- Temperature  
- Humidity  
- Moisture  
- Light  
- sa_temp_f  
- sa_humidity  
- sa_weather  
- LED (subscription)

---

## 🧪 Simulation

The full system was tested and validated in the Wokwi ESP32 simulator.

Due to time limitations and a faulty USB-C dongle on my MacBook that prevented reliable ESP32 hardware communication, the system was not deployed to physical hardware. However, all functionality was verified in simulation, and the code is ready for direct hardware implementation.

---

## 🛠 Technologies Used

- ESP32 (Arduino framework)
- Adafruit MQTT Library
- ArduinoJson
- HTTPClient
- OpenWeather API
- Adafruit IO
- Wokwi Simulator

---

## 📚 What I Learned

- Combining MQTT and HTTP protocols in one embedded system  
- JSON parsing on microcontrollers  
- Managing timed events using `millis()`  
- Designing sustainability-based automation logic  
- Integrating cloud dashboards with embedded hardware  

---

## 🔮 Future Improvements

- Add automatic water pump control
- Store historical data for trend analysis
- Add mobile notifications
- Implement plant-specific threshold profiles

---

## 👨‍💻 Author

Sebastian Cadena 
