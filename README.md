# Antisleep-Glasses
# Anti-Sleep Glasses with Vibration Alert

## Project Description

This project is an Arduino-based wearable device designed to help prevent drowsiness, particularly aimed at drivers or individuals needing to stay alert. The glasses detect prolonged eye closure (a sign of falling asleep) and trigger a vibration motor to alert the wearer.

**Note:** This is a prototype and proof-of-concept. It should **NOT** be relied upon as a primary safety device for preventing accidents caused by drowsiness. Always prioritize rest and responsible behavior.

## Features

*   Detects eye closure using a sensor.
*   Triggers a vibration alert if eyes remain closed for a predefined duration.
*   Uses an Arduino microcontroller for processing.
*   Wearable form factor (mounted on glasses).
*   Adjustable sensitivity/thresholds in the code.

## How it Works

1.  **Sensing:** An infrared (IR) proximity sensor (or similar eye-tracking sensor) is mounted on the glasses frame, pointing towards the eyelid. When the eye is open, the sensor reads a certain value. When the eyelid closes and comes near the sensor, the sensor's output changes (often going LOW when an obstacle is detected within range).
2.  **Processing:** The Arduino continuously reads the state of the sensor.
3.  **Detection Logic:** If the sensor indicates the eye is closed (obstacle detected) for longer than a specified duration (e.g., 1-2 seconds), the Arduino interprets this as a potential microsleep event.
4.  **Alert:** Upon detecting prolonged closure, the Arduino activates a small vibration motor, also mounted on the glasses frame, providing a physical alert to the wearer.
5.  **Reset:** The vibration typically stops once the sensor detects the eye has opened again.

## Hardware Requirements

*   **Microcontroller:** Arduino board (e.g., Arduino Nano, Uno, Pro Mini)
*   **Sensor:** Eye Closure Sensor (e.g., IR Obstacle Avoidance Sensor, IR Reflective Sensor like TCRT5000). *Specify the exact sensor you used.*
*   **Actuator:** Small Vibration Motor (Coin type or cylindrical pager motor)
*   **Motor Driver (Recommended):**
    *   NPN Transistor (e.g., 2N2222, BC547)
    *   Resistor (e.g., 1kΩ for the transistor base)
    *   Diode (e.g., 1N4007 or similar - for flyback protection across the motor)
*   **Power Source:** Battery Pack suitable for the Arduino and motor (e.g., 3.7V LiPo with appropriate voltage regulation, or 9V battery with VIN connection). *Specify your power setup.*
*   **Frame:** Old pair of glasses or dedicated frame for mounting components.
*   **Wires:** Jumper wires or thin gauge wires.
*   **Tools:** Soldering iron, solder, hot glue gun (for mounting).
*   **(Optional):** Small on/off switch.

## Software Requirements

*   [Arduino IDE](https://www.arduino.cc/en/software)

## Wiring / Connections (Example - Adjust pins as needed)

*   **IR Sensor:**
    *   VCC -> Arduino 5V (or 3.3V depending on sensor)
    *   GND -> Arduino GND
    *   OUT/Signal -> Arduino Digital Pin (e.g., `D2`)
*   **Vibration Motor Circuit:**
    *   Motor (+) -> Power Source (+) (e.g., Battery V+, or Arduino 5V if motor current is low and power source allows)
    *   Motor (-) -> Transistor Collector Pin
    *   Transistor Emitter Pin -> Arduino GND
    *   Transistor Base Pin -> 1kΩ Resistor -> Arduino Digital Pin (e.g., `D3`)
    *   Diode Cathode (Line/Band) -> Motor (+)
    *   Diode Anode -> Motor (-) (Connect diode *across* the motor terminals)
*   **Arduino Power:**
    *   Connect Battery Pack to Arduino VIN/GND (if using >5V) or 5V/GND (if using a regulated 5V source like a power bank).

*Make sure all GND connections are common.*

## Setup & Installation

1.  **Mount Components:** Carefully mount the sensor, vibration motor, Arduino, and battery onto the glasses frame using hot glue or other secure methods. Position the sensor so it reliably detects eyelid closure without obstructing vision.
2.  **Wire Components:** Solder or connect the components according to the wiring diagram above (or your specific configuration). Ensure connections are secure and insulated.
3.  **Install Arduino IDE:** Download and install the Arduino IDE if you haven't already.
4.  **Open Sketch:** Open the `.ino` project file in the Arduino IDE.
5.  **Configure Code:** Adjust pin definitions (`SENSOR_PIN`, `MOTOR_PIN`) and thresholds (`CLOSURE_DURATION_MS`, potentially a sensor threshold value) in the code if necessary.
6.  **Select Board & Port:** Choose the correct Arduino board type and COM port from the `Tools` menu in the IDE.
7.  **Upload Code:** Click the "Upload" button to flash the code onto your Arduino board.

## Usage

1.  Power on the device (using the battery and optional switch).
2.  Wear the glasses normally.
3.  The sensor will monitor your eyelid.
4.  If your eye remains closed for longer than the `CLOSURE_DURATION_MS` defined in the code, the vibration motor will activate.
5.  Open your eyes to stop the vibration (based on typical code logic).

## Customization

You can adjust the following parameters in the Arduino code (`.ino` file):

*   `SENSOR_PIN`: The digital pin connected to the IR sensor's output.
*   `MOTOR_PIN`: The digital pin controlling the vibration motor (via the transistor).
*   `CLOSURE_DURATION_MS`: The time (in milliseconds) the eye needs to be detected as closed before the alarm triggers (e.g., `1500` for 1.5 seconds).
*   **(If applicable)** `SENSOR_THRESHOLD`: If using an analog sensor or needing finer control over the IR sensor's digital trigger point (sometimes adjustable via potentiometer on the sensor module).

## Future Improvements

*   Add sensitivity adjustment via a potentiometer.
*   Implement different vibration patterns.
*   Add an audible alarm (small buzzer) alongside vibration.
*   Implement power-saving modes.
*   Use more sophisticated eye-tracking sensors for higher accuracy.
*   Add Bluetooth connectivity to log events or adjust settings via an app.

## **DISCLAIMER**

**This project is intended for educational and experimental purposes only. It is NOT a certified medical or safety device. Do not rely on this device to prevent falling asleep while driving or operating machinery. Fatigue can impair judgment regardless of alerts. Always prioritize adequate rest and take breaks when needed. The creators assume no liability for accidents or incidents related to the use or misuse of this device.**
