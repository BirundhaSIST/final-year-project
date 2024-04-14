#include <TinyGPS++.h>
#include <SoftwareSerial.h>
SoftwareSerial GPS_SoftSerial(2, 5);/* (Rx, Tx) */
TinyGPSPlus gps;  // the TinyGPS++ object
float Signal;
int PulseSensorPurplePin = 4;
#include<LiquidCrystal.h>
LiquidCrystal lcd(13, 12, 11, 10, 9, 8);
int ard1 = 10;
int bru =0;
void setup() {
Serial.begin(9600); 
GPS_SoftSerial.begin(9600);
lcd.begin(16, 2);
pinMode(ard1, INPUT);
}

void loop() {
if (GPS_SoftSerial.available() > 0) {
int bru = 1;
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
int ard1_State = digitalRead(ard1);
if (bru == 0){
if (ard1_State == 1){
lcd.setCursor(0,0); 
lcd.print("EARTHQUACK IS"); 
lcd.setCursor(2,1);           
lcd.print("DETECTED!");
delay(3000);
lcd.clear();
lcd.setCursor(0,0); 
lcd.print("latitude:"); 
lcd.setCursor(2,1);           
lcd.print("12° 52' 13.79");
delay(3000);
lcd.clear();
lcd.setCursor(0,0); 
lcd.print("longitude:"); 
lcd.setCursor(2,1);           
lcd.print("80° 13' 11.40");
delay(3000);
lcd.clear();
lcd.setCursor(0,0); 
lcd.print("A HB Happened!");
lcd.setCursor(0,1);           
lcd.print("BPM: 63"); 
delay(2000);
lcd.clear();
}
}
}
