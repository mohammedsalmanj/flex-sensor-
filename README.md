# flex-sensor-
code for angle measurement 
#include <LiquidCrystal.h>
const int FLEXPIN = A0; 
const float VCC = 4.98;
const float RDIV = 10000.0;
const int rs = 12, en = 11, d4 = 5, d5 = 4, d6 = 3, d7 = 2;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);
const float STRAIGHTRESISTANCE=59591.0; 
const float BENDRESISTANCE = 177444.0; 

void setup() 
{
  Serial.begin(9600);
  pinMode(FLEXPIN, INPUT);
    lcd.begin(16, 2);
    lcd.print("DIGI GONIO");
    
  
}

void loop() 
{
  int flexADC = analogRead(FLEXPIN);
  float flexV = flexADC * VCC / 1023.0;
  float flexR = RDIV * (VCC / flexV - 1.0);
  Serial.println("Resistance: " + String(flexR) + " ohms");
  
  float angle = map(flexR, STRAIGHTRESISTANCE, BENDRESISTANCE,
                   0, 90.0);
  Serial.println("Bend: " + String(angle) + " degrees");
  lcd.setCursor(1,1);
  lcd.print("angle: " + String(angle) + " deg");
  
  Serial.println();

  delay(10000);
}
