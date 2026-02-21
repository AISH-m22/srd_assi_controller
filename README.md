# srd_assi_controller

## What is srd_assi_controller?

This package is a ROS 2 node that controls ASSI LEDs using GPIO pins on a board like the NVIDIA Jetson AGX Orin.

### In simple terms

- 👉 It listens to a ROS 2 topic  
- 👉 Depending on the received state  
- 👉 It turns specific LEDs (blue and yellow) ON or OFF through GPIO  

## What Problem Does It Solve?

In many robotics systems (like Formula Student Driverless), the ASSI LEDs show the system state:

- 🔵 Blue → Autonomous mode active  
- 🟡 Yellow → Emergency or ready state  
- ⚫ Off → Manual mode / inactive  

Instead of manually controlling LEDs, this node:

- Subscribes to `/as_state`
- Automatically updates LEDs according to that state

## Overall Architecture

```text
[ System State Node ]
            │
            │ publishes
            ▼
        /as_state
            │
            ▼
    [ srd_assi_controller ]
            │
            │ uses gpiod
            ▼
     GPIO Pins (85, 86)
            │
            ▼
      Blue & Yellow LEDs
```

## In one sentece
This repository creates a ROS 2 node that listens to the autonomous system state and controls physical ASSI status LEDs using GPIO pins.
