# Forest Fire Detection 🔥🌲

This project is aimed at detecting forest fires using [insert technique: ML/CV/IoT]. It can help in early detection and reduce the impact of wildfires.


## 🔧 Technologies Used

- Ardiuno IDE
- C++ 
- Sensor data



## 📟 Sensor Requirements

To replicate this system using physical sensors, you will need:

       Component                      Function                             Operating Voltage 


 **DHT11 / DHT22** - For measuring temperature and humidity                          3.3V - 5V
 
 **MQ-2 / MQ-135** - Gas sensor to detect smoke, methane, CO, etc.                   3.3V - 5V
 
 **NodeMCU**  - Microcontroller or single-board computer to read sensors                3.3V
 


⚙️ Optional Hardware Upgrades
 
 Component                       Function                          Operating Voltage  

**GPS Module (NEO-6M)**  - Location tracking(latitude, longitude)     3.3V – 5V         
**Rain Sensor**          - Detects rain                               3.3V – 5V         
**Soil Moisture Sensor** - Detects soil dryness                       3.3V – 5V         
**UV Sensor (e.g., ML8511)** - Detects UV light from flame            3.3V – 5V         
**Li-ion Battery (18650)** - Power supply (portable)                  3.7V (nominal)    
**Battery Management System (BMS)** - Protects batteries                   —                 
**Solar Panel (Mini 5V)** - Rechargeable power                        5V output        
**LoRa Module (SX1278)** - Long-range wireless communication          3.3V              
**GSM Module (SIM800L)** - Sends SMS alerts                           3.7V – 4.2V       
**Buzzer / LED**         - Local sound/light alerts                   3.3V – 5V
**Arduino/ Raspberry Pi**- single-board computer to read sensors      3.3V - 5V
**Flame Sensor**  - Detects infrared light from fire                  3.3V - 5V
**SIM800L GSM Module**-Sends SMS alerts via mobile network            3.3V - 5V


> ⚠️ *Always check your specific component’s datasheet — some modules include voltage regulators, others don't. ESP32 especially can be damaged if directly fed 5V to GPIO pins.*


## 📁 Project Structure

forest-fire-detection-esp8266/
├── src/
│   ├── main.ino                      # Main program with all logic 
│   ├── SensorManager.h               # Optional: Abstraction for DHT, MQ sensor
│   ├── SensorManager.cpp             # Optional: Sensor reading & processing
│   ├── WebServerHandler.h            # Optional: Web page + JSON response handlers
│   ├── WebServerHandler.cpp          # Optional: Contains handleRoot() and handleData()
│
├── data/                             # For SPIFFS (if needed later for HTML/CSS/JS)
│   └── index.html                    # Optional: Separate HTML (for SPIFFS hosting)
│
├── include/                          # Additional headers 
│
├── lib/                              # Third-party or custom libraries
│
├── assets/                           # (Optional) Store images, diagrams, mockups
│   └── wiring_diagram.png            # Wiring diagram or schematic
│
├── .vscode/                          # If using VS Code + PlatformIO
│   └── settings.json
└── 




 
