# line-follow-tracking-
https://youtu.be/SQBg9QUfQVQ

//header file or library 
#include <Servo.h>
#include <AFMotor.h>

//defining pins and variables
int lefts = A0;
int  rights = A1;
int middles = A2;

//defining motors
AF_DCMotor motor1(1, MOTOR12_1KHZ); 
AF_DCMotor motor2(2, MOTOR12_1KHZ);
AF_DCMotor motor3(3, MOTOR34_1KHZ);
AF_DCMotor motor4(4, MOTOR34_1KHZ);
int speed = 180;
int time = 10;

void setup() {
  //Setting the motor speed
  motor1.setSpeed(speed);
  motor2.setSpeed(speed);
  motor3.setSpeed(speed);
  motor4.setSpeed(speed);
  //Declaring PIN input types
  pinMode(lefts,INPUT);
  pinMode(rights,INPUT);
  pinMode(middles,INPUT);
  //Begin serial communication
  Serial.begin(9600);
}

void loop(){

  if(digitalRead(lefts)== LOW && digitalRead(middles)== HIGH && digitalRead(rights)== LOW){
    forward();
  }
  else if(digitalRead(lefts) == HIGH && digitalRead(middles) == HIGH && digitalRead(rights)== LOW){
    turnleft();
  }
  else if(digitalRead(lefts) == HIGH && digitalRead(rights) == LOW && digitalRead(middles)== LOW){
    turnleft();
  }
  else if(digitalRead(lefts) == LOW && digitalRead(middles)== HIGH && digitalRead(rights)== HIGH){
    turnright();  
  }
  else if(digitalRead(lefts) == LOW && digitalRead(middles)== LOW && digitalRead(rights)== HIGH){
    turnright();  
  }
  else if(digitalRead(lefts)==HIGH && digitalRead(middles) == HIGH && digitalRead(rights)== HIGH){
    stop();
  }

  Serial.print(" Left ");
  Serial.print(digitalRead(lefts));
  Serial.print(" middles ");
  Serial.println(digitalRead(middles));
  Serial.print(" Right ");
  Serial.print(digitalRead(rights));
}

//function
void forward(){
  motor1.run(FORWARD);
  motor2.run(FORWARD);
  motor3.run(FORWARD);
  motor4.run(FORWARD);
}

void turnleft(){
  motor1.run(FORWARD);
  motor2.run(BACKWARD);
  motor3.run(BACKWARD);
  motor4.run(FORWARD);
}

void turnright(){
  motor1.run(BACKWARD);
  motor2.run(FORWARD);
  motor3.run(FORWARD);
  motor4.run(BACKWARD);
}

void stop(){
  motor1.run(RELEASE);
  motor2.run(RELEASE);
  motor3.run(RELEASE);
  motor4.run(RELEASE);
}
