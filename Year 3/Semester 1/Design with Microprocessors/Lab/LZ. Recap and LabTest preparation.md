> [!important] Main Goal
> - have a clear understanding on the concepts visited
> - be able to write code to use them in a real-life context

## Concepts:

### 1. Reading Digital Data and basic I/O functions
- Using the internal PULLUP registers for buttons
- Using digitalRead

### 2. I/O Modules
- Seven Segment Display
- Ports of the ATMega 
	- Read Port
	- Enable Port
	- Set port for Read/Write

To visit:
- [x] Reading PINs, setting PORTs
- [x] SSD (dont insist ig)
	- `shiftOut` method

### 3. LCD and External Interrupts
- LCD
- Create characters in LCD
- write data to LCD
- external interrupts
	- Assembly accessing
	- `attachInterrupt` method

To Visit:
- [x] LCD functions
- [x] Interrupts attached 

### 4. Timers
- use the System Timers
- generating the PWM
	- `analogWrite(dutyCycle)`

To visit:
- [x] use system timers
- [x] generate signals with specific duty cycle

### 5. Communication
- Serial (UART)
	- read byte by bye
	- use `SerialEvent` to detect data input + `while(Serial.available())`
- I2C
	- master/slave side
	- `begin(slaveAddress)`, bind functions with `Wire.onReceive(method-has access to nr of bytes-), Wire.onRequest()`
	- `Wire.read()` for reading a byte
	- `Wire.beginTransmission() -> Wire.write() -> Wire.endTransmission()`

To Visit:
- [x] Serial communication
- [x] I2C

### 6. Analog signal processing
- Use a temperature sensor
- Use a potentiometer
	- read the voltage and include it in a range
- Analog to Digital Converter Arduino (not insisted)

To Visit:
- [x] Analog read temperature
- [x] Reading a potentiometer - maybe generate a signal with variable duty cycle

- careful to put the read value into context (multiply it with adc resolution to get voltage, divide by measurement apparatus resolution to get the right value)

### Processing IDE - skip ⏩

### 7. Bluetooth communication
- Similar to serial
- ![[Pasted image 20221216114229.png]]
To visit:
- [x] Bluetooth

### 8. Motors
- DC Motor and H bridge
	- have 2 inputs for determining if the motor goes forward, bakward or stops
	- need to delay to see the effect of the operations 
	- specify speed as `analogWrite(0-255)`
- Servo motor and `Servo.h
	- `Servo.attach(pin)`
	- one data pin to specify angle (0 - 180)

To Visit:
- [x] Servo
- [x] DC

## Exercises:

#### 1.  Visit: interrupts, serial communication,  analog signal processing, bluetooth communication, servo

Idea: Use a phone for visualizing and sending commands to a temperature management unit. When the temperature is meant to be raised the servo pushes the button at a certain angle, when cooling needs to be accessed, the servo pushes at another angle. Add a switch between manual and phone mode. On manual mode one needs to use buttons for control (interrupts).

```c
#include "Serial1.h"
#include "Servo.h"

volatile int mode = 0; //describes manual = 0/bluetooth = 1 mode
int btnUp = 3; // Digital input pin
int btnDown = 4; //Digital input pin
int btnMode = 5; //Digital input pin

Servo servoObj;

int servoPin = 6; //digital output pin PWM
volatile int servoAngle = 90; //neutral angle;

int tempRead = A0; //pin for temperature sensor
float tempValue = 0;
float ADCResolution = 0.0049;
float resolutionSensor = 0.01; //0.01 V per degree
float tempOffset = 0.5; //for reading negtive values

void setup() {
	Serial1.begin(9600); //initialize bluetooth connection RX 19, TX 18
	
	pinMode(btnUp, INPUT_PULLUP);
	pinMode(btnDown, INPUT_PULLUP);
	pinMode(btnDown, INPUT_PULLUP);
	
	pinMode(tempRead, INPUT);
	analogReference(DEFAULT); //refrence for ADC (5V)

	attachInterrupt(digitalPinToInterrupt(btnUp), heatManual, FALLING);
	attachInterrupt(digitalPinToInterrupt(btnDown), coolManual, FALLING);
	attachInterrupt(digitalPinToInterrupt(btnMode), changeMode, FALLING);

	servo.attach(servoPin); // implicit values for angles
	servo.write(servoAngle); //place on neutral position 0 to 180
}

void loop() {
	// read temperature and send it on bluetooth
	tempValue = readTemperature();
	writeTemperatureOnSerial();

	if (mode == 1) {
		readBluetoothCommand();
	}

	// command the servo
	actOnServo();
}

void readBluetoothCommand() {
	receivedString = "";
		bool thereWasSomethingAvailable = false;
	while(Serial1.available()) {
		char readChar = (char) Serial1.read();
		receivedString += readChar;
		thereWasSomethingAvailable = true;
	}

	if(thereWasSomethingAvailable) {
		parseBluetoothCommand(receivedString);
	}
}

void parseBluetoothCommand(String input) {
	if(input.equals("Heat up!")) {
		servoAngle = 120;
	}
	else if(input.equals("Cool down!")) {
		servoAngle = 60;
	}
	else {
		Serial1.println("invalid command!");
	}
}

float readTemperature() {
	//read multiple times, apply the Vref and all that
	float sumTemp
	
	for(int i = 0; i < 10; i++) {
		int readValueInt = analogRead(tempRead);
		float voltageRead = ADCResolution * readValueInt; //voltage read
		float tempCelsius = (voltageRead - tempOffset) / resolutionSensor; 
		//get read of the offset (no negative reading) and divide by res.
		sumTemp += tempCelsius
	}

	float finalTemp = sumTemp / 10;
	return finalTemp;
}

void writeTemperatureOnSerial() {
	Serial1.println("The current temperature: ");
	Serial1.println(tempValue);
}

void actOnServo() {
	if(servoAngle != 90) {
		servoObj.write(servoAngle);
		delay(1000); //keep it there for one second;
		servoAngle = 90;
		servoObj.write(servoAngle);
	}
}

void heatManual() {
	if(mode == 0) {
		servoAngle = 120;
	}
}

void coolManual() {
	if(mode == 0) {
		servoAngle = 60;
	}
}

void changeMode() {
	if(mode = 0) {
		mode = 1;
	}
	else if(mode = 1) {
		mode = 0;
	}
}
```

#### 2. Visit: dc motors + pwm, i2c communication with multiple slaves, timers, LCD with custom character, millis() usage - measure a rate or so

Have two devices that can play the role of master and 2 slaves in a water pump system. One device is the commander that sends every slave every 10 seconds the speed with which to run the pump (DC Motor), the slaves send back a digital signal whose duty cycle is printed on the LCD

```c
/* MASTER */
#include "Wire.h" //i2c
#include "TimerOne.h" //send signal at a regular rate
#include "LiquidCrystal.h"

LiquidCrystal lcd(7, 6, 5, 4, 3, 2);

//custom characters for slave 1 and 2
byte slave1Logo[8] = {
	B00000,
	B10000,
	B01000,
	B00100,
	B00010,
	B00001,
	B00000,
	B00000
}
byte slave2Logo[8] = {
	B00000,
	B11111,
	B01010,
	B10101,
	B01010,
	B11111,
	B00000,
	B00000
}

int speed;

void setup() {
	Wire.begin(); //Master I2C
	
	lcd.createChar(1, slave1Logo);
	lcd.createChar(2, slave2Logo);

	Timer1.initialize(10000000); //1 sec interval
	Timer1.attachInterrupt(sendSpeed);

	lcd.begin(16, 2);
	lcd.setCursor(0, 1);
	lcd.write(1);
	lcd.print(": ");
	lcd.setCursor(0, 1);
	lcd.write(2);
	lcd.print(": ")
}

void printMotorsStatus() {
	
}

void sendSpeed(int slaveAddr) {
	Wire.beginTransmission(slaveAddr);
	Wire.write((char)speed);
	Wire.endTransmission
}

void loop() {
	readFromSlave1();
	readFromSlave2();
}
```

```c
/* SLAVE 1 */
#include <Wire.h>

//motor pins
int motorI0  = 3;
int motorI1 = 4;

void setup() {
	Wire.begin(8); //slave address
	Wire.onRequest(sendMessage)
	Wire.onReceive(receiveEvent)
}

void moveMotor(int pin1, int pin2, boolean forward, int speed) {
	if (speed == 0) {
		digitalWrite(pin1, 0);
		digitalWrite(pin2, 0);
	}
	else {
		if (forward) {
			digitalWrite(m1, 0);
			analogWrite(m2, speed);
		}
		else {
			analogWrite(m1, speed);
			digitalWrite(m2, 0)
		}
	}
}

void delayStopper(int delay_r) {
	moveMotor(motorI0, motorI1, 0, 0);
	delay(delay_r)
}

void actOnMotor() {
	moveMotor(motorI0 motorI1, 1, receivedSpeed);
	delay(2000); //on
	delayStopper(); //off
}

void receiveEvent(int bytes) {
	char receivedSpeed = Wire.read();
	int intSpeed = (int) receivedSpeed;
	actOnMotor();
}

void sendMessge() {
	Wire.write("Henlo");
}

void loop() {
	
}

```

```c
/* SLAVE 2 */
```
