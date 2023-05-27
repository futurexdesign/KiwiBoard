# Kiwiboard 
Control board for the KiwiCleaner watch cleaning machine.  Intended to provide an all-in-one option for the design. 

## Board Goals
- Have a single PCB with connections for the stepper motor, heater, fan, and user interface for ease of wiring. 
- Integrate a Trinamic silent stepper driver to greatly reduce volume. 
- Simplify the user interface for switching between run-modes. 
- Allow cooling fan to run for a timed period after a dry cycle, to allow the heater to safely cool down. 
- Not cost too much more than the original solution, with the understanding that there is greater functionality. 

## Theory of Operation
- Power input is 12V 
- Input is protected by a resettable PolyFuse with rated 10A constant load capacity.  
- Main Microcontroller is a RaspberryPi Pico (RP2040).  
  - This can be either the normal version, or the "header" version.  Can be mounted either way, board contains both the SMD and THT pads. 
- Display a 240x320 Color TFT LCD Connected via SPI
- User interface is controlled via a rotary encoder with pushbutton
- Pico has full control of stepper via SPI connection to the TMC5160 board. 
   - The Integrated Ramp Generator contained within the TMC5160 is utilized to control all motion, allowing very smooth and precise control over basket motion.  
- Pico can enable / disable the drive output via MOTOR_EN (Active Low)
- Pico can activate the Heater by pulling HEATER_CTL High, switching on the relay (3.3v coil).
- Pico can activate the fan by pulling FAN_CTL high, fan current conducted by the TIP120
- 3.3v power provided by a drop in switching powersupply module for simplicity. 
- All power connectors are Phoenix LPT lever connectors.  These support 12awg - 24awg up to a max of 24A.  Can substitute in SPT or any other phoenix connector with the same 5mm pin spacing

An expansion header has been added to support any additional mods people may want. *Example functionality would be a buzzer module to indicate end of cycle.*  Due to the flexability of the microcontroller, we can expose a ton of functionality on 4 pins.  The following IO is available on the expansion connector. 

- 4 independent GPIO pins for input/output 
- 1 hardware i2c bus (i2c1), and 2 GPIO pins (GPI0 and GPIO1)
- 4 pins with a PIO program assigned to them. 

Additionally the expansion header supplys 3.3V and GND connections. 

