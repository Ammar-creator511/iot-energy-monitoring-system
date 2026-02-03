#define BLYNK_TEMPLATE_ID "your token id"
#define BLYNK_TEMPLATE_NAME "Diamond Distributor"
#define BLYNK_AUTH_TOKEN "copy auth token here"

#include <WiFi.h>
#include <WiFiClient.h>
#include <BlynkSimpleEsp32.h>
#include <PZEM004Tv30.h>
#include <LiquidCrystal_I2C.h>
#include <Wire.h>

char ssid[] = "wifi name";     
char pass[] = "password"; 

LiquidCrystal_I2C lcd(0x27, 16, 2); 
PZEM004Tv30 pzem(Serial2, 16, 17);
BlynkTimer timer;

void updateSystem() {
  float v  = pzem.voltage();
  float c  = pzem.current();
  float p  = pzem.power(); // Power in Watts
  float pf = pzem.pf();

  lcd.clear();
  if (isnan(v)) {
    lcd.setCursor(0, 0);
    lcd.print("PZEM ERROR");
    lcd.setCursor(0, 1);
    lcd.print("Check AC Supply");
  } else {
    // Row 0: Voltage, Current, and WiFi Status
    lcd.setCursor(0, 0);
    lcd.print((int)v); lcd.print("V "); 
    lcd.print(c, 1);   lcd.print("A ");
    
    // WIFI STATUS: Shows "ON" if connected
    lcd.setCursor(12, 0); 
    if (WiFi.status() == WL_CONNECTED) {
      lcd.print("W:ON"); 
    } else {
      lcd.print("W:--"); 
    }

    // Row 1: Power in Watts and Power Factor
    lcd.setCursor(0, 1);
    lcd.print((int)p); lcd.print("W "); // Power in Watts
    lcd.setCursor(8, 1);
    lcd.print("PF:"); lcd.print(pf, 2);

    // Sync to Blynk only if WiFi is connected
    if (WiFi.status() == WL_CONNECTED) {
      Blynk.virtualWrite(V4, v);  
      Blynk.virtualWrite(V2, c);  
      Blynk.virtualWrite(V3, p); // Sending Watts to V3
      Blynk.virtualWrite(V0, pf); 
      Blynk.virtualWrite(V1, 255); 
    }
  }
}

void setup() {
  // Wait for LCD hardware to stabilize
  delay(1500); 
  
  Wire.begin(21, 22); 
  lcd.init();
  lcd.backlight();
  lcd.clear();

  // Screen 1: Submission
  lcd.setCursor(0, 0);
  lcd.print("Submitted To:");
  lcd.setCursor(0, 1);
  lcd.print("Engr.TouseefAbid");
  delay(5000); 

  // Screen 2: Group ID
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Submitted by:");
  lcd.setCursor(0, 1);
  lcd.print("23-ELE-32,34,41");
  delay(5000);
  
  // Start WiFi (Non-Blocking)
  WiFi.begin(ssid, pass); 
  Blynk.config(BLYNK_AUTH_TOKEN); 
  
  pzem.resetEnergy();
  timer.setInterval(2000L, updateSystem); 
}

void loop() {
  // Only run Blynk if online to prevent screen lag
  if (WiFi.status() == WL_CONNECTED) {
    Blynk.run();
  }
  timer.run();
}
