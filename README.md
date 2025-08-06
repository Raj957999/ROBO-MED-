ROBO‑MED – Smart Medical Liquid Handling System
Overview
ROBO‑MED is an Arduino‑based automated liquid handling system designed to simulate high‑precision fluid dispensing for medical or laboratory use.  
It uses \*\*ultrasonic sensors\*\* to detect containers and \*\*servo motors\*\* to control fluid dispensing, similar to dosing stations or CIP (Clean‑In‑Place) valves in industrial environments.
Features
- Detects presence of container using ultrasonic sensor
- Servo‑controlled liquid dispensing
- LED status indication
- Feedback‑based automation (no manual control required)
- Low‑cost prototype for educational \& industrial use
Components Used
- Arduino Uno
- HC‑SR04 Ultrasonic Sensor
- SG90 Servo Motor
- LED \& Resistor
- Breadboard & Jumper Wires
How It Works
1. Ultrasonic sensor detects if a container is in place
2. If detected → Servo rotates to dispensing position
3. LED turns ON while dispensing
4. Servo returns to original position after completion
Code
The Arduino code reads ultrasonic sensor distance, compares it to a threshold, and controls the servo motor accordingly.
#include <Servo.h>

#define TRIG 9
#define ECHO 8
#define BUTTON 7
#define LED 6

Servo dispenser;
bool manual_mode = false;

void setup() {
  pinMode(TRIG, OUTPUT);
  pinMode(ECHO, INPUT);
  pinMode(BUTTON, INPUT_PULLUP);
  pinMode(LED, OUTPUT);
  dispenser.attach(3);
  dispenser.write(0); // Closed
  Serial.begin(9600);
}

long getDistance() {
  digitalWrite(TRIG, LOW); delayMicroseconds(2);
  digitalWrite(TRIG, HIGH); delayMicroseconds(10);
  digitalWrite(TRIG, LOW);
  long duration = pulseIn(ECHO, HIGH);
  long distance = duration * 0.034 / 2;

  // Filter out very small or large readings (noise)
  if (distance == 0 || distance > 50) {
    return -1; // Invalid reading
  }
  return distance;
}

void loop() {
  long distance = getDistance();
  Serial.print("Distance: "); Serial.println(distance);

  if (digitalRead(BUTTON) == LOW) {
    manual_mode = true;
  }

  if ((distance != -1 && distance < 10) || manual_mode) {
    digitalWrite(LED, HIGH);
    dispenser.write(90); // Open valve
    delay(3000);
    dispenser.write(0);  // Close valve
    digitalWrite(LED, LOW);
    manual_mode = false;
  } else {
    digitalWrite(LED, LOW); // Keep LED OFF when idle
  }

  delay(100);
}
