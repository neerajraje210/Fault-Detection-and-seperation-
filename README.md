# Fault-Detection-and-seperation-
As the project's name is " Fault detection and Seperation" as the name tells our project detects the faulty product and seperates it from the perfect ones.
## CODE

#include <Wire.h> 
#include <LiquidCrystal_I2C.h>
#include <Servo.h>
LiquidCrystal_I2C lcd(0x27,20,4);
Servo tap_servo;
int sensor_pin = 4;
int tap_servo_pin =5;
int val;
int buzzer=11;

void setup()
{
 lcd.init();                       
 pinMode(11,OUTPUT);
 lcd.backlight();
 lcd.setCursor(0,1);
 
 for(int i= 0; i<= 20; i++)
{ 
  lcd.clear(); 
  lcd.setCursor(i,0); 
  lcd.print("FAULT DETECTION");
  delay(200); 
}
 
 lcd.clear(); 
  pinMode(sensor_pin,INPUT);
  tap_servo.attach(tap_servo_pin);
}

void loop()
{
 
val = digitalRead(sensor_pin);
delay(200);
if (val==LOW)
{
 tap_servo.write(0);
  digitalWrite(11,HIGH);
   delay(500);
   lcd.print("FAULT DETECTED");
   delay(400);
   lcd.clear();
   digitalWrite(11,LOW);
   delay(500);

}
if (val==HIGH)
{
tap_servo.write(360);
digitalWrite(11,LOW);

}

}
