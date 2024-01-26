# Automatic-Plant-Watering-System

## Get Started
This project has been executed via wokwi.


### Description
The set-up is to monitor and water three plants. Each blue LED represents a water pump and each potentiometer represents a soil moisture sensor. Under automatic condition potentiometer has an upper threshold value beyond which the pumps turn off and a lower threshold value below which the pumps turn on. When the water level i.e the UltraSonic sensor distance calculated goes above a certain value all the pumps turn of till the water level is restored. There is also an override option. The commands for each of these options are in the code under `screen()` and `start()` functions. The `Serial Monitor` helps communicate with the system and displays the output.


## Components

The model is to automatically water three plants as needed :

The components used are as follows:

| Component name | Description |
| --- | --- |
| Potentiometer | Used as soil moisture sensor |
| LED (blue) | Represents a pump for each plant |
| LED (red) | Used to indicate low water level in the tank |
| Buzzer | Also used to indicate low water level in the tank |
| UltraSonic Sensor | Used to check water level in the tank |
| Resistors | For protection of the components |


### Steps to follow
1. The code to be executed in wokwi: [![Wokwi badge](wokwi_badge.svg)](https://wokwi.com/projects/387913956139463681)
 
2. The outputs and the circuit can be found in `images` folder.
 
3. The code to be executed is found in `code` script. 
