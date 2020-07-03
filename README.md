# ShuttleGRBL
Contour's ShuttleExpress for smoothly jogging a GRBL CNC machine under cncjs and Linux on a RaspberryPi using USB/hidraw

![Image of CNC machine](https://github.com/Duffmann/ShuttleGRBL/blob/master/doc/Sorotec_CL04.jpg)

Note: I am an absolute beginner when it comes to nodeJS, JavaScript and even git...

## Install

1.) Clone or download this repo
2.) cd into directory
3.) run 'npm install'
4.) copy new udev rule 'sudo cp udev/99-shuttlexpress.rules /etc/udev/rules.d/'
5.) Setup a rule in cncjs to auto-start the ShuttleExpress pendant like in the animated gif below

![Adjust cncjs settings to auto-start ShuttleExpress pendant](https://github.com/Duffmann/ShuttleGRBL/blob/master/doc/cncjs_event_settings_for_ShuttleJog.gif)

Make sure to adjust the path ('/home/pi/ShuttleExpress/bin/cncjs-pendant-keyboard' in the example) and the name of your GRBL's serial port (here: /dev/ttyACM0) to your own setup.

## Usage

Jogging is locked out until you select one of the Axis by pressing one of the three middle buttons. Sequence is 'X', 'Y' and 'Z' from the left.

After selecting the Axis you want to jog you can either use the Shuttle-Wheel or the Dial:
* Shuttle Wheel uses GRBL great realtime Jog extensions
  * Turning the Shuttle Wheel left will jog towards positive coordinates, to the right will jog into negative coordinate direction
    * Speed of Jogging depends on how far you turn the wheel. Default is 5x the number of ticks you turn in mm/s
      * Example: Turning the wheel 5 ticks to the left will jog your selected axis with 25mm/s, 7 ticks to the right jogs -35mm/s
      * If you want to change this you can simply edit the line '''const JOG_SPEEDUP = 5
  * Turn the Dial left will jog towards positive coordinates, to the right will jog into negative coordinate direction
    * If you don't keep either the leftmost nor the rightmost buttons pressed while turing the dial it will Jog by 0.01mm per tick
    * If you keep the leftmost button pressed while turing the dial it will Jog by 10x 0.01mm = 0.1mm per tick
    * If you keep the rightmost button pressed while turing the dial it will Jog by 100x 0.01mm = 1mm per tick
    
