/************************************************************
   Project: IoT Smart Home Automation using ESP32 & Blynk
   Platform: ESP32
   Developed By: Sushma M
   Description:
   Control 4 home appliances remotely using Blynk mobile app.
*************************************************************/

#define BLYNK_PRINT Serial

#include <WiFi.h>
#include <WiFiClient.h>
#include <BlynkSimpleEsp32.h>

// 🔑 ENTER YOUR BLYNK AUTH TOKEN
char auth[] = "Your_Blynk_Auth_Token";

// 🌐 ENTER YOUR WIFI DETAILS
char ssid[] = "Your_WiFi_Name";
char pass[] = "Your_WiFi_Password";

// 🔌 RELAY PIN CONNECTIONS
#define RELAY1 23
#define RELAY2 22
#define RELAY3 21
#define RELAY4 19

// 🔘 Blynk Virtual Buttons
// V1 -> Relay1
// V2 -> Relay2
// V3 -> Relay3
// V4 -> Relay4

void setup()
{
  Serial.begin(9600);

  pinMode(RELAY1, OUTPUT);
  pinMode(RELAY2, OUTPUT);
  pinMode(RELAY3, OUTPUT);
  pinMode(RELAY4, OUTPUT);

  // All devices OFF initially
  digitalWrite(RELAY1, HIGH);
  digitalWrite(RELAY2, HIGH);
  digitalWrite(RELAY3, HIGH);
  digitalWrite(RELAY4, HIGH);

  // Connect to Blynk Cloud
  Blynk.begin(auth, ssid, pass);
}

// 🔵 Blynk Button V1
BLYNK_WRITE(V1)
{
  int value = param.asInt();
  digitalWrite(RELAY1, value ? LOW : HIGH);
}

// 🔵 Blynk Button V2
BLYNK_WRITE(V2)
{
  int value = param.asInt();
  digitalWrite(RELAY2, value ? LOW : HIGH);
}

// 🔵 Blynk Button V3
BLYNK_WRITE(V3)
{
  int value = param.asInt();
  digitalWrite(RELAY3, value ? LOW : HIGH);
}

// 🔵 Blynk Button V4
BLYNK_WRITE(V4)
{
  int value = param.asInt();
  digitalWrite(RELAY4, value ? LOW : HIGH);
}

void loop()
{
  Blynk.run();
}

