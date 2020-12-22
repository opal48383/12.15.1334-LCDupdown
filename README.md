# 12.15.1334-LCDupdown
/*    
  The circuit:  
 * LCD RS pin to digital pin 12  
 * LCD Enable pin to digital pin 11  
 * LCD D4 pin to digital pin 5  
 * LCD D5 pin to digital pin 4  
 * LCD D6 pin to digital pin 3  
 * LCD D7 pin to digital pin 2  
 * LCD R/W pin to ground  
 * LCD VSS pin to ground  
 * LCD VCC pin to 5V  
 * 10K resistor:  
 * ends to +5V and ground  
*/  
#include <LiquidCrystal.h>  
const int rs = 12, en = 11, d4 = 5, d5 = 4, d6 = 3, d7 = 2;  
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);  
String LCD[]{"A","B","C","D"};  
  
int a=0,b=0;  
bool SW=false;  
  
void setup() {  
  pinMode(7,INPUT);  
  pinMode(6,INPUT);  
  lcd.begin(16, 2);  
  lcd.clear();  
  lcd.print("Welcome!");  
}  
  
void loop() {  
    if(SW == false){  
    if (digitalRead(7) == 0 || digitalRead(6) == 0) {  
    while (digitalRead(7) == 0 || digitalRead(6) == 0){}  
    SW = true;  
    lcd.clear();  
    delay(200);  
   }  
    }  
   else{  
     if (digitalRead(7) == 0) {  
        while (digitalRead(7) == 0){}  
         a++;  
         delay(200);  
         lcd.clear();  
      }  
      if (digitalRead(6) == 0) {  
        while (digitalRead(6) == 0){}  
        a--;  
        delay(200);  
        lcd.clear();  
      }  
      b = a + 1;  
     if (a>=4){a=0;}  
     if (b>=4){b=0;}  
     if (a<=-1){a=3;}  
     if (b<=-1){b=3;}  
     lcd.setCursor(0, 0);  
     lcd.print(LCD[a]);  
     lcd.setCursor(0, 1);  
     lcd.print(LCD[b]);  
   }  
}  
