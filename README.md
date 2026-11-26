# WRO Future Engineers 2021 – Saturn NCD 🤖

An autonomous vehicle developed for the **World Robot Olympiad (WRO) Future Engineers 2021** competition, combining embedded systems, ultrasonic sensing, computer vision, and autonomous vehicle control.

The robot was designed using a LEGO-based chassis and a hybrid control architecture integrating an Arduino Mega and Raspberry Pi 4.

## ⚙️ Hardware Architecture

The vehicle consists of the following hardware components:

| Component | Description |
|---|---|
| Main Chassis | LEGO-based mechanical structure |
| Microcontroller | Arduino Mega |
| Embedded Computer | Raspberry Pi 4 |
| Camera | Raspberry Pi Camera Module V2 |
| Distance Sensors | Five ultrasonic sensors |
| Steering | Servo motor with Ackermann steering mechanism |
| Drive System | JSumo 1000 RPM DC motor |
| Transmission | Differential gear driving the rear wheels |
| Power Supply | Li-Po RC batteries |

The system uses a distributed control architecture: the Arduino Mega handles low-level vehicle control and sensor readings, while the Raspberry Pi 4 performs image processing and communicates navigation information to the Arduino through serial communication.

## 💻 Software Architecture and Autonomous Navigation

The software was developed around two main operating configurations, corresponding to the qualifying and final competition rounds.

### 1. Qualifying Rounds – Ultrasonic-Based Navigation

**Source file:** `Round_1_2.ino`

During the qualifying rounds, the autonomous navigation algorithm runs directly on the Arduino Mega.

The robot uses five ultrasonic sensors to estimate distances from surrounding walls and obstacles.

The navigation algorithm implements:

- **Wall Following:** Maintains the robot's trajectory along straight sections using distance measurements from the two side sensors.
- **Turning Decisions:** Uses measurements from the front sensor and one of the front-side sensors to determine the turning direction (left or right).
- **Parking:** Determines when to initiate parking using a dedicated counter and distance measurements from the front ultrasonic sensor.

### 2. Final Rounds – Vision-Assisted Navigation

The final-round architecture integrates the Raspberry Pi 4 to provide camera-based perception and support autonomous navigation.

**Source file:** `RaspberryPI_Python_CODE.py`

The Raspberry Pi Camera Module V2 captures images of the competition arena, and image processing is used to detect the colours of the competition pillars.

Key functionalities include:

- **Pillar Colour Detection:** Identifies pillar colours through image processing.
- **Distance Estimation:** Estimates the distance between the robot and a pillar based on its apparent pixel size in the captured image.
- **Serial Communication:** Sends specific characters and strings to the Arduino Mega to communicate detected pillar information and navigation instructions.

**Arduino control:**

Source file: `Round_3_4.ino`

The Arduino Mega receives information from the Raspberry Pi and executes the corresponding vehicle-control algorithms.

These include:

- Obstacle and cube avoidance using ultrasonic sensor measurements.
- Wall-following control based on navigation instructions received from the Raspberry Pi.
- Parking control using a dedicated counter and front ultrasonic sensor measurements.

## 🔄 System Communication

The two controllers operate together through serial communication:

1. The Raspberry Pi captures and processes camera images.
2. Image processing identifies the colours of the competition pillars.
3. The Raspberry Pi estimates pillar distance using pixel-size information.
4. Navigation information is transmitted to the Arduino Mega through serial communication.
5. The Arduino executes the corresponding control and navigation algorithms using the received information and ultrasonic sensor measurements.

This architecture combines the computational capabilities of the Raspberry Pi with the real-time sensor acquisition and motor-control capabilities of the Arduino Mega.

## 📂 Repository Structure

| File / Directory | Description |
|---|---|
| `Round_1_2.ino` | Arduino navigation algorithm for the qualifying rounds. |
| `Round_3_4.ino` | Arduino control algorithm for the final rounds. |
| `RaspberryPI_Python_CODE.py` | Raspberry Pi image processing and serial communication software. |
| Other files | Supporting project resources and documentation. |

## 📜 License

This project is licensed under the **Creative Commons Attribution 4.0 International License (CC BY 4.0)**.

You are free to share and adapt the project materials, provided appropriate credit is given.

[View the full license](https://creativecommons.org/licenses/by/4.0/).

## 🔗 Original Repository

This project was originally developed and published under my previous GitHub account.

**Original repository:** [Ibraheem-Moalla/WRO_Future_Engineers_Saturn_NCD](https://github.com/Ibraheem-Moalla/WRO_Future_Engineers_Saturn_NCD)

This independently maintained copy preserves the original Git history and commit authorship while providing a dedicated space for project documentation and engineering portfolio presentation.
