#include <ESP8266WiFi.h>
#include <ESP8266WebServer.h>
#include <DHT.h>

#define MQ_SENSOR_PIN A0
#define DHTPIN D4
#define DHTTYPE DHT11

const char* ssid = "JAY 2424";
const char* password = "jaymataji";

DHT dht(DHTPIN, DHTTYPE);
ESP8266WebServer server(80);

int tempThreshold = 35;
float temperature = 0.0, humidity = 0.0;
int smokeLevel = 0;
String fireStatus = "No Fire Detected";
String gasTypes = "Clean Air";

void handleRoot() {
  String page = R"rawliteral(
    <!DOCTYPE html>
    <html>
    <head>
      <title>Fire Detection System</title>
      <meta name="viewport" content="width=device-width, initial-scale=1">
      <style>
        body {
          font-family: 'Poppins', sans-serif;
          background-color: #121212;
          color: #ffffff;
          text-align: center;
          padding: 20px;
        }
        h1 {
          color: #f8b400;
        }
        .container {
          display: flex;
          flex-wrap: wrap;
          justify-content: center;
          gap: 20px;
        }
        .card {
          background: #1e1e1e;
          padding: 20px;
          border-radius: 10px;
          width: 250px;
          box-shadow: 0px 4px 10px rgba(255, 204, 0, 0.3);
        }
        .title { font-size: 18px; font-weight: 600; }
        .value { font-size: 22px; color: #f8b400; }
        .fire-status { font-size: 20px; font-weight: 600; }
        .danger { color: red; }
        .safe { color: green; }
      </style>
      <script>
        function fetchData() {
          fetch('/data')
            .then(response => response.json())
            .then(data => {
              document.getElementById('temperature').innerHTML = data.temperature + " °C";
              document.getElementById('humidity').innerHTML = data.humidity + " %";
              document.getElementById('smoke').innerHTML = data.smokeLevel;
              document.getElementById('gases').innerHTML = data.gasTypes;
              document.getElementById('fireStatus').innerHTML = data.fireStatus;
              document.getElementById('fireStatus').className = data.fireStatus.includes("WARNING") ? "fire-status danger" : "fire-status safe";
            });
        }
        setInterval(fetchData, 1000);
      </script>
    </head>
    <body onload="fetchData()">
      <h1> Fire Detection System </h1>
      <div class="container">
        <div class="card">
          <div class="title">Temperature</div>
          <div class="value" id="temperature">-- °C</div>
        </div>
        <div class="card">
          <div class="title">Humidity</div>
          <div class="value" id="humidity">-- %</div>
        </div>
        <div class="card">
          <div class="title">Smoke Level</div>
          <div class="value" id="smoke">--</div>
        </div>
        <div class="card">
          <div class="title">Gas Types</div>
          <div class="value" id="gases">--</div>
        </div>
      </div>
      <h2 class="fire-status" id="fireStatus">No Fire Detected</h2>
    </body>
    </html>
  )rawliteral";

  server.send(200, "text/html", page);
}

void handleData() {
  String jsonResponse = "{";
  jsonResponse += "\"temperature\": " + String(temperature) + ",";
  jsonResponse += "\"humidity\": " + String(humidity) + ",";
  jsonResponse += "\"smokeLevel\": " + String(smokeLevel) + ",";
  jsonResponse += "\"gasTypes\": \"" + gasTypes + "\",";
  jsonResponse += "\"fireStatus\": \"" + fireStatus + "\"";
  jsonResponse += "}";

  server.send(200, "application/json", jsonResponse);
}

void setup() {
  Serial.begin(9600);
  delay(1000);
  Serial.println("\n\nStarting...");

  dht.begin();

  WiFi.begin(ssid, password);
  Serial.print("Connecting to WiFi");

  unsigned long startTime = millis();
  while (WiFi.status() != WL_CONNECTED) {
    delay(500);
    Serial.print(".");
    if (millis() - startTime > 15000) {
      Serial.println("\nWiFi Connection Failed!");
      return;
    }
  }

  Serial.println("\nWiFi Connected!");
  Serial.print("IP Address: ");
  Serial.println(WiFi.localIP());

  server.on("/", handleRoot);
  server.on("/data", handleData);
  server.begin();
  Serial.println("Web server started.");
}

void loop() {
  server.handleClient();

  float temp = dht.readTemperature();
  float hum = dht.readHumidity();
  smokeLevel = analogRead(MQ_SENSOR_PIN);

  if (!isnan(temp)) temperature = temp;
  if (!isnan(hum)) humidity = hum;

  // Gas Type Logic
  gasTypes = (smokeLevel > 700) ? "LPG"
            : (smokeLevel > 500) ? "CO"
            : (smokeLevel > 450) ? "Methane"
            : "Clean Air";

  // Fire Status Logic
  fireStatus = (temperature > tempThreshold && smokeLevel > 450)
               ? "WARNING:Fire detected!"
               : "No Fire Detected";

  // Debug Output
  Serial.print("Temp: ");
  Serial.print(temperature);
  Serial.print(" °C | Humidity: ");
  Serial.print(humidity);
  Serial.print(" % | Smoke: ");
  Serial.print(smokeLevel);
  Serial.print(" | Gas: ");
  Serial.print(gasTypes);
  Serial.print(" | Status: ");
  Serial.println(fireStatus);

  delay(1000);
}
