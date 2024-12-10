# Automatic-grass-cutting-robot
A grass-cutting robot is an autonomous device designed to mow lawns efficiently. Equipped with sensors and blades, it navigates predefined areas, avoids obstacles, and ensures uniform cutting. It saves time, reduces effort, and provides consistent results, making it ideal for residential or commercial use.

1.Problem Statement
Maintaining well-trimmed lawns in residential and commercial areas is a time-consuming and labor-intensive task, especially for large or uneven spaces. Traditional lawnmowers require manual operation, which can be inefficient and unsafe. Additionally, inconsistent grass cutting and challenges in navigating obstacles or difficult terrains further hinder the effectiveness of traditional methods. There is a need for an autonomous grass-cutting solution that ensures consistent, efficient, and safe lawn maintenance while minimizing human effort and environmental impact.

2.Scope of the Solution
The proposed grass-cutting robot offers an efficient and automated solution for maintaining lawns in residential, commercial, and public spaces. Equipped with advanced sensors, navigation systems, and cutting mechanisms, the robot can autonomously map the mowing area, detect and avoid obstacles, and provide uniform grass trimming. The scope includes:

Automation and Efficiency:

Reducing human effort and time required for lawn maintenance.
Ensuring consistent and uniform cutting across various lawn sizes and terrains.
Safety:

Incorporating collision detection and obstacle avoidance to prevent accidents.
Operating autonomously, reducing the risk of injuries associated with manual mowers.
Adaptability:

Designing the robot to handle complex landscapes, including slopes, uneven terrain, and tight corners.
Providing flexibility for use in residential backyards, parks, sports fields, and other outdoor spaces.
Sustainability:

Minimizing environmental impact by optimizing energy usage.
Offering eco-friendly operations compared to gas-powered alternatives.
Smart Integration:

Enabling programmability for custom mowing schedules and patterns.
Potential integration with IoT devices for remote monitoring and control.
The solution addresses the need for safer, more reliable, and environmentally friendly lawn maintenance, making it ideal for both small-scale and large-scale applications.
Enabling programmability for custom mowing schedules and patterns.
Potential integration with IoT devices for remote monitoring and control.
The solution addresses the need for safer, more reliable, and environmentally friendly lawn maintenance, making it ideal for both small-scale and large-scale applications.

3.Required components to develop solutions
The list of components required for the grass-cutting robot is detailed in the provided link, which includes essential hardware like sensors, motors, blades, microcontrollers, and a power supply, among others, for efficient functionality.
https://github.com/aleenasojan0325/Automatic-grass-cutting-robot/issues/3#issue-2730183737

To simulate the design and functionality of the grass-cutting robot, the Tinkercad platform was used. This software allowed us to virtually model the circuit and verify its operation before physical implementation.

4.Simulated circuit

Attached are the two links:
https://github.com/aleenasojan0325/Automatic-grass-cutting-robot/issues/2#issue-2730180748
https://github.com/aleenasojan0325/Automatic-grass-cutting-robot/issues/1#issue-2730161482

5.Video of the Demo
Below attached is the link of demo
https://github.com/aleenasojan0325/Automatic-grass-cutting-robot/issues/4#issue-2730285673

6.Gerber File
Below attached is the schematic diagram 


7.Code for the solution


int trig=A2;
int echo=A3;
int dt=10;

// Motor A connections
int enA = 8;
int in1 = 10;
int in2 = 9;
// Motor B connections
int enB = 4;
int in3 = 6;
int in4 = 5;

//int distance,duration;
void setup() {
  // put your setup code here, to run once:
    pinMode(trig,OUTPUT);
    pinMode(echo,INPUT);
    Serial.begin(9600);
    pinMode(A0,HIGH);
  
  	// Set all the motor control pins to outputs
	pinMode(enA, OUTPUT);
	pinMode(enB, OUTPUT);
	pinMode(in1, OUTPUT);
	pinMode(in2, OUTPUT);
	pinMode(in3, OUTPUT);
	pinMode(in4, OUTPUT);
	
	// Turn off motors - Initial state
	digitalWrite(in1, LOW);
	digitalWrite(in2, LOW);
	digitalWrite(in3, LOW);
	digitalWrite(in4, LOW);
}

//This code is written to calculate the DISTANCE using ULTRASONIC SENSOR

int calc_dis()
{
    int duration,distance;
    digitalWrite(trig,HIGH);
    delay(dt);
    digitalWrite(trig,LOW);
    duration=pulseIn(echo,HIGH);
    distance = (duration/2) / 29.1;
    return distance;
}

void loop() {
	directionControl();
	delay(1000);
	speedControl();
	delay(1000);
}

// This function lets you control spinning direction of motors
void directionControl() {
	// Set motors to maximum speed
	// For PWM maximum possible values are 0 to 255
	analogWrite(enA, 255);
	analogWrite(enB, 255);

	// Turn on motor A & B
	digitalWrite(in1, HIGH);
	digitalWrite(in2, LOW);
	digitalWrite(in3, HIGH);
	digitalWrite(in4, LOW);
	delay(2000);
	
	// Now change motor directions
	digitalWrite(in1, LOW);
	digitalWrite(in2, HIGH);
	digitalWrite(in3, LOW);
	digitalWrite(in4, HIGH);
	delay(2000);
	
	// Turn off motors
	digitalWrite(in1, LOW);
	digitalWrite(in2, LOW);
	digitalWrite(in3, LOW);
	digitalWrite(in4, LOW);
}

// This function lets you control speed of the motors
void speedControl() {
	// Turn on motors
	digitalWrite(in1, LOW);
	digitalWrite(in2, HIGH);
	digitalWrite(in3, LOW);
	digitalWrite(in4, HIGH);
	
	// Accelerate from zero to maximum speed
	for (int i = 0; i < 256; i++) {
		analogWrite(enA, i);
		analogWrite(enB, i);
		delay(20);
	}
	
	// Decelerate from maximum speed to zero
	for (int i = 255; i >= 0; --i) {
		analogWrite(enA, i);
		analogWrite(enB, i);
		delay(20);
	}
	
	// Now turn off motors
	digitalWrite(in1, LOW);
	digitalWrite(in2, LOW);
	digitalWrite(in3, LOW);
	digitalWrite(in4, LOW);
}







