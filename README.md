#What is srd_assi_controller?

#This package is a ROS2 node that controls ASSI LEDs using GPIO pins on a board like the NVIDIA Jetson AGX Orin.

#In simple terms:

#👉 It listens to a ROS2 topic
#👉 Depending on the received state
#👉 It turns specific LEDs (blue and yellow) ON or OFF through GPIO

#What Problem Does It Solve?

#In many robotics systems (like Formula Student Driverless), the ASSI (Autonomous System Status Indicator) LEDs show the system state:
#Examples:

#🔵 Blue → Autonomous mode active
#🟡 Yellow → Emergency or ready state
#⚫ Off → Manual mode / inactive

#Instead of manually controlling LEDs, this node:
#Subscribes to a system state topic (/as_state)
#Automatically updates LEDs according to that state

#Ovreall architecture:

'''[ System State Node ]
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
      Blue & Yellow LEDs'''

#In One Sentence

#This repository creates a ROS2 node that listens to the autonomous system state and controls physical ASSI status LEDs using GPIO pins.
