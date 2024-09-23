# Voltage Logger for a Three-Phase System

## Overview

This project is designed to log **phase-to-phase voltages** in a **three-phase system** using an Arduino, a ZMPT101B voltage sensor, and a 2-channel relay module. The data is stored on an SD card via the Arduino Ethernet Shield. The system can also be expanded to support internet-based logging or more accurate timekeeping with an RTC module.

### Key Features
- Measure voltages between any two wires in a three-phase system.
- Log voltage data to an SD card with timestamps.
- Future-proof for internet-based data logging using an Ethernet Shield or additional logic.

## Hardware Requirements

- **Arduino**, with Uno used as example
- **ZMPT101B voltage sensor**
- **2-channel double relay module**
- **SD card module** (for logging data), with the Arduino Ethernet Shield as an example 
- **SD card**
- **Three-phase system wires**
- **Jumper wires**
- **Breadboard (optional)**

## Wiring and Relay Switching Logic

The project uses relays to switch between phase pairs (A-B, B-C, A-C), allowing you to measure voltages between any two phases:

- **Relay 1 OFF, Relay 2 OFF** → Measure voltage between **A and C** (V<sub>AC</sub>)
- **Relay 1 ON, Relay 2 OFF** → Measure voltage between **B and C** (V<sub>BC</sub>)
- **Relay 1 OFF, Relay 2 ON** → Measure voltage between **A and B** (V<sub>AB</sub>)

Each phase combination is measured, and the voltage values are logged along with a timestamp.

## Setup and Calibration Process

### 1. **Initial Calibration**
Before running the logger, follow these steps to establish a baseline:

1. **Attach the wires** from the three-phase system to the relays, marking them as A, B, and C.
2. Use a **multimeter** to manually measure the phase-to-phase voltages (A-C, B-C, A-B).
3. **Record the time** and the voltage values manually. This will serve as a reference for scaling the logged data if necessary.

### 2. **System Logging**
Once the Arduino starts logging, it will record voltages at defined intervals (e.g., every second). Arduino’s **millis()** function is used to generate a simple timestamp. This is generally reliable over short periods, but may drift over extended durations (days/weeks). You can compare the initial manual readings with the logged data to check for any significant deviation and adjust or scale the values as needed.

## Data Processing

After collecting data, you can import the CSV file into **Google Sheets** or any other data analysis tool. We will provide a **Google Sheets template** to help you **plot** and **filter** the voltage data, making it easier to visualize and analyze the results.

### Continuous Data Monitoring (Optional)
You can modify the system to continuously read voltages in real time and log data only when specific conditions are met, like an external trigger or button press.

## Setup Verification and Monitoring

To ensure that the system is running correctly, check the following:

- **Relay Clicks**: Listen for the **clicks** of the relays as they switch between different phase measurements (A-C, B-C, A-B). This ensures the relays are working properly.
- **LED or Display (Optional)**: You can add an LED to indicate when data is being logged or relays are switching. Alternatively, an LCD display can show real-time status updates.

This helps confirm that the loop is running, and the system is actively collecting data.

## Future Improvements

### 1. **Real-Time Clock (RTC) Module**
For more accurate timekeeping, especially for long-term logging, you can integrate an **RTC module** like the DS3231. This will ensure that timestamps remain accurate over several days or weeks.

### 2. **Internet-Based Logging**
In future iterations, you can use the **Ethernet Shield** or other modules for logging data over the internet, enabling real-time remote monitoring of voltage data.
