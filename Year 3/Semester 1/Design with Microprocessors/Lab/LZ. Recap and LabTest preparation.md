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

### 3. LCD and External Interrupts
- LCD
- Create characters in LCD
- write data to LCD
- external interrupts
	- Assembly accessing
	- `attachInterrupt` method

### 4. Timers
- use the System Timers
- generating the PWM

### 5. Communication
- Serial (UART)
- I2C
	- master/slave side

### 6. Analog signal processing
- Use a temperature sensor
- Use a potentiometer
- Analog to Digital Converter Arduino (not insisted)

### Processing IDE - skip ⏩

### 7. Bluetooth communication
- Similar to serial

### 8. Motors
- DC Motor and H bridge
- Servo motor and `Servo.h`


## Exercises:

#### 1.  Visit: interrupts, serial communication,  analog signal processing, bluetooth communication, servo

Idea: Use a phone for visualizing and sending commands to a temperature management unit. When the temperature is meant to be raised the servo pushes the button at a certain angle, when cooling needs to be accessed, the servo pushes at another angle. Add a switch between manual and phone mode. On manual mode one needs to use buttons for control (interrupts).

```c

```

#### 2. Visit: dc motors + pwm, i2c communication with multiple slaves, timers, LCD with custom character, millis() usage

```c
```