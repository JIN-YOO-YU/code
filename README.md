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



#define TRIGGER_PIN 5
#define ECHO_PIN 6
#define MAX_DISTANCE 30

#define LED_R_PIN 13
#define LED_G_PIN 12
#define LED_B_PIN 11

#define BUZZER_PIN 7

void setup() {
  pinMode(LED_R_PIN, OUTPUT);
  pinMode(LED_G_PIN, OUTPUT);
  pinMode(LED_B_PIN, OUTPUT);
  pinMode(BUZZER_PIN, OUTPUT);
  pinMode(TRIGGER_PIN, OUTPUT);
  pinMode(ECHO_PIN, INPUT);
  Serial.begin(9600);
}

void loop() {
  delay(50);
  digitalWrite(TRIGGER_PIN, LOW);
  delayMicroseconds(2);
  digitalWrite(TRIGGER_PIN, HIGH);
  delayMicroseconds(10);
  digitalWrite(TRIGGER_PIN, LOW);
  long duration = pulseIn(ECHO_PIN, HIGH);
  int distance = duration * 0.0344 / 2;

  if (distance > 0 && distance <= MAX_DISTANCE) {
    Serial.print("Distance: ");
    Serial.println(distance);

    if (distance >= 0 && distance <= 10) {
      digitalWrite(LED_R_PIN, HIGH);
      digitalWrite(LED_G_PIN, LOW);
      digitalWrite(LED_B_PIN, LOW);
      playWarningTone();
    } else if (distance >= 11 && distance <= 20) {
      digitalWrite(LED_R_PIN, LOW);
      digitalWrite(LED_G_PIN, HIGH);
      digitalWrite(LED_B_PIN, LOW);
      playFurElise();
    } else if (distance >= 21 && distance <= 30) {
      digitalWrite(LED_R_PIN, LOW);
      digitalWrite(LED_G_PIN, LOW);
      digitalWrite(LED_B_PIN, HIGH);
      playHandInHand();
    }
  } else {
    Serial.println("Out of range");
  }
}

void playWarningTone() {
  tone(BUZZER_PIN, 1000);
  delay(500);
  noTone(BUZZER_PIN);
  delay(500);
}

void playFurElise() {
  int melody[] = {440, 440, 466, 440, 523, 493, 440, 466, 440, 523, 493, 440, 440, 466, 440, 523, 493};
  int duration[] = {500, 500, 500, 500, 500, 500, 500, 500, 500, 500, 500, 500, 500, 500, 500, 500, 500};
  for (int i = 0; i < 17; i++) {
    tone(BUZZER_PIN, melody[i]);
    delay(duration[i]);
    noTone(BUZZER_PIN);
    delay(50);
  }
}

void playHandInHand() {
  int melody[] = {262, 262, 294, 294, 330, 330, 349, 349, 392, 392, 440, 440};
  int duration[] = {500, 500, 500, 500, 500, 500, 500, 500, 500, 500, 500, 500};
  for (int i = 0; i < 12; i++) {
    tone(BUZZER_PIN, melody[i]);
    delay(duration[i]);
    noTone(BUZZER_PIN);
    delay(50);
  }
}
