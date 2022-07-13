# -Servo-Stepper-brushless-Motors
bjective: design electronic circuit to control servo and stepper and dc  motor by using some electronic components with Arduino
used components: Arduino uno - Potentiometer - Servo motor - Stepper motor - dc motor - 9V Battery - H-bridge Motor Driver - wires - Breadboard
Attached files: circuit View - the arduino code - Schematic View 
NOTE the Dc and stepper motor there is a Potentiometer act as a button so we can control the motor by adjusting the potentiometer.

Servo motor code: 
#include <Servo.h>

int SensorValue = 0;

int outputvalue = 0;

Servo servo_9;

void setup()
{
  pinMode(A0, INPUT);
  servo_9.attach(9, 500, 2500);
}

void loop()
{
  SensorValue = analogRead(A0);
  outputvalue = map(SensorValue, 0, 1023, 0, 180);
  servo_9.write(outputvalue);
  delay(10); // Delay a little bit to improve simulation performance
}
-------
Stepper motor code: 

#include <Stepper.h>
const int stepsPerRevolution = 200; 
Stepper myStepper(stepsPerRevolution, 8, 9, 10, 11);
int stepCount = 0;  
void setup() {
}
void loop() {
  int sensorReading = analogRead(A0);
  int motorSpeed = map(sensorReading, 0, 1023, 0, 100);
  if (motorSpeed > 0) {
    myStepper.setSpeed(motorSpeed);
    myStepper.step(stepsPerRevolution / 100);
  }
}

--------
DC motor code: 

int potIn;

 int fwdPin = 5;
 int revPin = 6;


 void setup()
 {
   
    pinMode (fwdPin, OUTPUT);
    pinMode (revPin, OUTPUT);
   
   
    Serial.begin(9600);
   
   
 }

void loop()
{
  
  potIn = analogRead(A0);
  int output = potIn/4;
  
  analogWrite (revPin, output);
  
  Serial.println(output);
  delay(100);
  
}
------------










