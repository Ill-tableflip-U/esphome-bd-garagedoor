# esphome B&D garage door configuration

This is how to build an ESPhome device to interface with a B&D garage door with ESPhome (specifically a 2012 model)


the B&D stock remote control can be opened up and modified for control use with ESPhome. for each garage door, the following is needed:
* 1 BC559 PNP transistor
* 1 10K ohm pullup resistor
* 1 1M ohm resistor for the base pin
These all go inside the shell for the remote and can be directly soldered to it. Keep in mind, this likely only fits with the larger, white remote shells like the one pictured.

![remote control modification](https://github.com/user-attachments/assets/71d5640e-401c-4cfa-b7e1-5797fa53c30a)
![image](https://github.com/user-attachments/assets/083f498e-e0d8-470b-9b31-54c3dcf33ad1)

In the images, the blue wires are for power to hardwire the remote power along with the ESP. The red and white wires are the control outputs, for controlling the doors.
To modify the controller
1. eject the button cell battery as that will no longer be needed
2. straddle a BC559 transistor onto the side of the board for each button you wish to control. The collector pin should sit on the button solder pad closest to the board edge, meanwhile the emitter pin should be soldered to the pad closest to the center. The middle pin of the transistor (the base) should go onto the back side of the board. 
![image](https://github.com/user-attachments/assets/7b7207c1-e919-486a-98a9-3766acdfdcf1)
3. Solder a 1 million ohm resistor to the base pin of the BC559. (You should probably trim the legs of all of these)
4. after the 1m ohm resistor, solder one side of a 10k resistor to the empty end, and the other side to the button cell battery shieldd
5. Solder a ground wire to the 0v pad on the rear of the remote board and a 3.3v wire to the top of the button cell battery receptacle.
6. In the junction between the two resistors, solder a wire and connect it to any esp GPIO. You can now control your garage!

It is fairly easy to drill a small hole in the top of the original remote shell so these wires can be routed to the ESP setup.

Now, 3D print the enclosure for the device, or make your own. Mine, which has a .blend and a .stl available to print, has room for the the necessary hardware for garage doors as well as a ws2812 LED and a hc-SR501 motion sensor and is designed around the ESP32-C3 supermini. This is an effective all-in-one design that seems to work well.

PLEASE NOTE: some ESP32-C3 superminis have bad antenna chips, I used one of those for this project and it turned out fine. Still, YMMV.

![image](https://github.com/user-attachments/assets/a2ec6939-e81a-44b9-bf19-83e13f4597ba)

Now, some basic reed switches can be plugged into the device through the holes in the sides. Make sure 1 pin is connected to ground, and the other to an IO pin. The reed switch should be placed, so that the circuit is closed when the garage door is closed. This will allow ESPhome and home assistant to detect whether the door is open or closed. It is a good idea to tape all your wires down so they don't get pulled out.

![1445471319204691348](https://github.com/user-attachments/assets/5cc22009-8197-4a14-86b0-8640498a046c)


Now, change the example yaml I provided so that it has the correct pins for the sensors/outputs on your device. The example has the configuration for two garage doors.
This device can now simply be powered via a usb-c power source. Ensure the device works properly before mounting it.
![431047512649017129](https://github.com/user-attachments/assets/54fef707-01d5-4d2b-b2cd-d9314ddc9b39)

For questions, feel free to open an issue.
