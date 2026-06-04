# Storm Drain Auto-Declogger

An Arduino-powered device that autonomously detects and clears debris from storm drain grates to prevent urban flooding. Permanently installed inside a drain, it uses an ultrasonic distance sensor to detect debris buildup and deploys a rotating arm with a fan blade and sweeper to clear the blockage — without any human intervention.

---

## The Problem

Clogged storm drains are one of the leading causes of urban street flooding. Leaves, trash, and debris accumulate on drain grates during storms, preventing water from entering the drain system entirely. Current solutions rely on manual inspection crews dispatched after storms — slow, expensive, and reactive.

## Our Solution

A self-contained unit that sits inside the drain grate and monitors for debris continuously. When the ultrasonic sensor detects that the distance to the surface has shortened (indicating debris has piled up), it automatically runs a cleaning cycle and returns to standby — no human needed.

---

## How It Works

**Detection:**
An ultrasonic sensor pings upward toward the drain grate surface once per second. Under normal conditions it reads a consistent baseline distance. When debris accumulates on the grate, the measured distance shortens. If it drops below the threshold (default: 20cm), a cleaning cycle is triggered.

**Cleaning Cycle:**
1. LED pulses as a visual warning to pedestrians
2. Arm extends outward from the drain housing
3. Fan blade spins and sweeper oscillates back and forth 3 times, clearing debris into the drain or agitating it to be carried away by water flow
4. Fan and sweeper power down
5. Arm retracts to home position
6. System enters a 5-second cooldown before resuming monitoring

---

## Hardware

| Component | Purpose |
|---|---|
| Arduino (Uno/Nano) | Main controller |
| HC-SR04 Ultrasonic Sensor | Debris detection |
| Continuous Rotation Servo (x2) | Fan blade + sweeper |
| Standard Servo | Extending/retracting arm |
| LED | Visual warning during cleaning |
| Battery Pack | Power supply |

---

## Wiring

| Component | Arduino Pin |
|---|---|
| Ultrasonic TRIG | 7 |
| Ultrasonic ECHO | 6 |
| LED | 13 |
| Fan Servo | 9 |
| Arm Servo | 10 |
| Sweeper Servo | 11 |

---

## Software

**Dependencies:**
- `Servo.h` (built into Arduino IDE)

**Key Settings (adjustable in code):**

```cpp
const int clogThreshold = 20; // Distance in cm that triggers cleaning
const int stopValue     = 90; // Stop signal for continuous servos
const int speedValue    = 99; // Full speed signal for continuous servos
```

Adjust `clogThreshold` based on your drain depth and installation height.

---

## Installation

1. Clone this repo and open `drain_declogger.ino` in the Arduino IDE
2. Connect hardware per the wiring table above
3. Upload to your Arduino board
4. Open Serial Monitor at 9600 baud to observe sensor readings in real time
5. Mount the unit inside the drain housing, sensor facing upward toward the grate

---

## Serial Output

```
Monitoring Drain... Distance: 34 cm
Monitoring Drain... Distance: 33 cm
Monitoring Drain... Distance: 18 cm
CLOG DETECTED! Initiating Clean Cycle...
Cleaning Complete. System Standby.
```

---

## Future Development

- Solar charging to eliminate battery replacement
- Wireless data logging to track cleaning frequency per drain
- Water-jet mechanism to replace fan blade for heavier wet debris
- Mesh network across multiple drains for city-wide monitoring dashboard

---

## Background

Developed as an engineering school project targeting urban flood prevention. Clogged catch basins are listed by the NYC Department of Environmental Protection as one of the three primary causes of street flooding. Impervious city surfaces contribute to an estimated $9 billion in flood damages annually in the US. This device targets the problem at its source.
