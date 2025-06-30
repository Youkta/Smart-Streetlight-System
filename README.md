# Smart Streetlight Dimmer Based on Traffic Flow

A responsive and sustainable streetlighting system that adapts in real-time to traffic and environmental conditions.
Developed as a group project under the Texas Instruments Women in Semiconductor & Hardware (WiSH) 2025 mentorship program, this solution combines motion detection, ambient light sensing, and solar-powered control to intelligently manage brightness—minimizing energy waste while maintaining public safety in diverse urban scenarios.

## Project Summary

Conventional streetlights waste energy by staying on at full brightness all night, regardless of road usage. Our system uses a combination of motion sensors, ambient light sensors, and communication modules to intelligently dim or brighten lights based on real-time traffic conditions and environment.

## Key Features

- **Three Smart Operating Modes**  
  - **Time Mode**: Fixed schedule-based lighting.  
  - **Zone Pulse Mode**: Local motion detection triggers brightening.  
  - **Urban Wave Mode**: Lights dynamically follow vehicles using mmWave and Zigbee sync.

- **Smart Components**
  - PIR & mmWave sensors for motion
  - BH1750 sensor for ambient light
  - ESP32-H2 + SIM800L for processing and fault alerts
  - Solar panel + Lead-acid battery for off-grid operation

- **Built-in Fault Detection**
  - Detects sensor, power, and controller failures using cross-check logic, without using any external components
  - Sends SMS alerts via GSM when faults occur

- **Sustainable & Scalable**
  - Solar-powered with optional AC fallback
  - Independent poles with minimal maintenance
  - Break-even within ~3 years

## System Architecture

Each streetlight pole contains:

- **Power**
  - 100W LED + LED driver
  - Solar panel + 12V 70Ah Lead-acid battery
  - PWM Charge Controller (auto-switches to AC when needed)
  - Buck converter & LDO for safe voltage regulation

- **Sensors**
  - **PIR sensor** for pedestrian motion
  - **mmWave radar** (1 per 15 poles) for vehicle speed and direction
  - **Ambient light sensor (BH1750)** for auto-dimming logic

- **Control**
  - **ESP32-H2** microcontroller
  - **SIM800L GSM Module** for SMS alerts
  - **Zigbee module** (Urban Wave mode) for inter-pole sync

## Fault Detection Logic

All faults are detected using existing sensors—no extra hardware required.  
Examples:

| Component         | Detected By                                                                 |
|-------------------|-----------------------------------------------------------------------------|
| Solar Panel       | Bright ambient light + no battery charge rise                               |
| Battery           | Voltage < 11V during daytime                                                |
| ESP32 MCU         | Daily GSM “All OK” message not received                                     |
| PIR/mmWave        | No signal or abnormal activity for long durations                           |
| LED/Driver        | No change in brightness after PWM signal sent                               |
| Charge Controller | Sunlight present but battery voltage stays flat                             |

## Cost & ROI

| Mode           | Avg Cost per Pole | Power Consumption | Notes                          |
|----------------|-------------------|--------------------|-------------------------------|
| Time Mode      | ₹18,490           | ~80W               | Fixed schedule lighting       |
| Zone Pulse     | ₹20,820           | ~65W               | PIR-based dimming             |
| Urban Wave     | ₹22,935           | ~67W               | mmWave + Zigbee sync lighting |

- ROI estimated within **2.5 to 4 years**
- Saves up to **60% energy** vs traditional LED setups
- ~80% coverage using solar power

## Use Case Mapping

| Location Type             | Recommended Mode | Why                                       |
|---------------------------|------------------|-------------------------------------------|
| Villages, Trails          | Time Mode        | Low activity, fixed schedule works best   |
| Residential Areas         | Zone Pulse       | Moderate, sporadic motion                 |
| Highways, Smart City Roads| Urban Wave       | High-speed traffic, dynamic lighting sync |

## Testing Methodology

- Simulated all three modes on hardware testbed
- Verified:
  - Sensor-triggered dimming
  - GSM alert triggering
  - Zigbee latency in Urban Wave Mode
  - Fault detection & SoC behavior

## Market Opportunity

India has ~3 crore streetlights. Even targeting 5% conversion = ₹2,700+ crore market.  
Government schemes & CSR funding make this a scalable and impactful solution.

## Limitations

- High initial cost (~₹16k–₹20k/pole)
- PIR reliability in high-temperature zones
- Zigbee mesh may degrade in dense RF environments
- Urban Wave setup is more complex (requires calibration)
- No full-scale field deployment yet

We're actively improving fault tolerance, optimizing battery health tracking, and exploring TinyML for predictive lighting.

---

