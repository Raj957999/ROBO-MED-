ROBO‑MED – Smart Medical Liquid Handling System



**Overview**

ROBO‑MED is an Arduino‑based automated liquid handling system designed to simulate high‑precision fluid dispensing for medical or laboratory use.  

It uses \*\*ultrasonic sensors\*\* to detect containers and \*\*servo motors\*\* to control fluid dispensing, similar to dosing stations or CIP (Clean‑In‑Place) valves in industrial environments.



**Features**

\- Detects presence of container using ultrasonic sensor

\- Servo‑controlled liquid dispensing

\- LED status indication

\- Feedback‑based automation (no manual control required)

\- Low‑cost prototype for educational \& industrial use



**Components Used**

\- Arduino Uno

\- HC‑SR04 Ultrasonic Sensor

\- SG90 Servo Motor

\- LED \& Resistor

\- Breadboard \& Jumper Wires



**How It Works**

1\. Ultrasonic sensor detects if a container is in place

2\. If detected → Servo rotates to dispensing position

3\. LED turns ON while dispensing

4\. Servo returns to original position after completion



**Code**

The Arduino code reads ultrasonic sensor distance, compares it to a threshold, and controls the servo motor accordingly.





