# code
#include <LiquidCrystal_I2C.h>
#include <Wire.h>
LiquidCrystal_I2C lcd(0x27, 16, 2);
void setup() {
  // put your setup code here, to run once:
  lcd.init();
  lcd.backlight();
  }
  
void loop() {
  // put your main code here, to run repeatedly:
  int value = random(0, 3);
  if (value == 0) {
    lcd.setCursor(0,0);
    lcd.print(" seoil ");
  }
  else if(value == 1) {
    lcd.setCursor(0,1);
    lcd.print(" Hello World ");
  }
  else if(value == 2) {
    lcd.setCursor(0,0);
    lcd.print(" student name ");
    lcd.setCursor(0,1);
    lcd.print(" Hello World ");
  }
  delay(1000);
  lcd.clear();
}
