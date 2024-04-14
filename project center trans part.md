#include <TinyGPS++.h>
#include <SoftwareSerial.h>
SoftwareSerial GPS_SoftSerial(2, 5);/* (Rx, Tx) */
TinyGPSPlus gps;  // the TinyGPS++ object
float Signal;
int PulseSensorPurplePin = 4;
#include<LiquidCrystal.h>
LiquidCrystal lcd(13, 12, 11, 10, 9, 8);
void setup() {
Serial.begin(9600); 
GPS_SoftSerial.begin(9600);
lcd.begin(16, 2);       
}
void loop() {
if (GPS_SoftSerial.available() > 0) {
if (gps.encode(GPS_SoftSerial.read())) {
if (gps.location.isValid()) {            
Serial.print(F("- latitude: "));
Serial.println(gps.location.lat());
lcd.setCursor(0,0); 
lcd.print("latitude:");
lcd.println(gps.location.lat());
delay(2000);
Serial.print(F("- longitude: "));
Serial.println(gps.location.lng());
lcd.setCursor(0,0); 
lcd.print("longitude:");
lcd.println(gps.location.lng());
delay(2000);
delay(2000);  
Signal = analogRead(PulseSensorPurplePin);  
Signal= Signal/30;   
Serial.print("BPM =  ");
Serial.println(Signal);
lcd.setCursor(0,0); 
lcd.print("A HB Happened!");
lcd.setCursor(0,1);           
lcd.print("BPM: "); 
lcd.println(Signal);
delay(2000);
lcd.clear();
}
}
}
}
