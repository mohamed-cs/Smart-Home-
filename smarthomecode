#include <LiquidCrystal.h>
#include <Servo.h>
#include<string.h>
int rs = 4, en = 5, d4 = 6, d5 = 7, d6 = 8, d7 = 9;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);

Servo myServogarage;
Servo myServodoor;

int TempSensorPin = A0;
int button1 = 18;
int button2 = 17;
int button3 = 2;
const int trig = 13;
const int echo = 19;

int servogaragepin = 3;
int servodoorpin = 16;
int photores = A1;
int ledpin = 12;

String pass;

void setup() {
  
  Serial.begin(9600);
  lcd.begin(16, 2);
  
  pinMode(button1,INPUT);
  pinMode(button2,INPUT);
  pinMode(button3,INPUT);
  pinMode(TempSensorPin, INPUT);
  pinMode(trig, OUTPUT);
  pinMode(echo, INPUT);
  pinMode(10, OUTPUT);
  pinMode(11, OUTPUT);
  pinMode(photores,INPUT);
  pinMode(ledpin,OUTPUT);
  myServogarage.attach(servogaragepin);
   myServogarage.write(0);
    myServodoor.attach(servodoorpin);
   myServodoor.write(0);
   
}

void loop()
{
 	pass="";
     
  for(int i=0;i<3;)
{
    
  
    
  //Task 1
  
	int value = analogRead(TempSensorPin);
  float myval = value / 1023.0;
  
  myval*=5;
  myval-=0.5;
  myval*=1000;
  
  float c1=myval/10;
 
  lcd.setCursor(0,0);
  //Serial.println(c1);
  lcd.print("Temp: ");
  lcd.print(c1);
  lcd.print(" C");
 
    // task 3 LED 
 int sensorvalue=analogRead(photores);
 float value2=(sensorvalue/1023.0)*5.0;
  int res=(1000*value2)/(5-value2);
  //Serial.println(res);
  if(value2>3.3){
    digitalWrite(ledpin,HIGH);
  }
  else {
  
  digitalWrite(ledpin,LOW);
  
  }
  
  //Task 5
  
  float duration,distance;
  digitalWrite(trig,LOW);
  delayMicroseconds(5);
  
  digitalWrite(trig,HIGH);
  delayMicroseconds(5);

  digitalWrite(trig,LOW);
  duration=pulseIn(echo,HIGH);
  
  distance=duration/29/2;
  
  if(distance<170.0)
  {
     myServogarage.write(90);
    
  }
  else
  {
    myServogarage.write(0); 
  }
  
  
  
  //task 2 
 /* 
  int value2=analogRead(TempSensorPin);
  float mv=value2/1023.0;
  mv=mv*5;
  mv=mv-0.5;
  mv=mv *1000;
  float degree=mv/10;
  Serial.println(degree);
  */
  if(c1>25)
  {
    digitalWrite(10,HIGH);
    digitalWrite(11,LOW);
  }
  else
  {
    digitalWrite(10,LOW);
    digitalWrite(11,LOW);
  }
    
    
    if(digitalRead(button1))
  {   
    
    digitalWrite(button1,LOW);
     Serial.println("button1");
  
     pass+="1";
   
    i++;
 	
  }
  
  else if(digitalRead(button2))
  {   
   digitalWrite(button2,LOW);
   // delay(40);
   Serial.println("button2");
     pass+="2";
    
   i++;
    
  }
 else if(digitalRead(button3))
  {   
 
    digitalWrite(button3,LOW);
    //delay(40);
     Serial.println("button3");
 
     pass+="3";
    
    i++;
  
 }
    
}
  

 Serial.println(pass);
  if(pass=="123")
     {
    	lcd.setCursor(0,1);
 		 lcd.print("Correct pass");
    	 myServodoor.write(90);
       //Serial.println("correct");   
    
      delay(1000);
  lcd.clear();
 myServodoor.write(0);
     }
  else
  {
    lcd.setCursor(0,1);
 	lcd.print("incorrect pass");
     myServodoor.write(0);
    
      delay(500);
 lcd.clear();
 myServodoor.write(0);
  }
 

}
