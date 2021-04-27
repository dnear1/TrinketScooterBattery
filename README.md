# TrinketScooterBattery
Use an Adafruit Trinket 3.3v ATTiny85 to wake up the Okai 36v 12.8ah Scooter batteries

Since it doesn't have USB-serial, the basic serial functions don't work.  But I was able to use a Software Serial library to create a TTL serial port on pins 0 and 2 to send out commands to wake up the Okai 36v 12.8ah scooter batteries commonly sold at jag35.com.

Pin 2 connects to the blue wire on the 5 pin connector that screws into the battery.  a >40v to 3.3v buck converter needs to be connected between the battery main output, with the 3.3v output powering the Trinket.  Add a switch between the battery and buck converter to disable the wakeup commands when the battery is not being used to reduce standby current consumption.
Pin 0 is not used in my code, but can be connected to the green wire on the battery connector, if you need to read back or act on the battery status.

I used Arduino 1.8.13 to upload code.  To recognize the Trinket, make sure you add the Adafruit Boards library that contains the Trinket AtTiny85 family.  Then select the Adafruit Trinket (ATTiny85 @ 8mhz) for the processor type and under Programmer, select USBTinyISP.
Immediately before uploading, press the reset button, then compile and upload.  If you press the button too early or if it takes too long to compile, Arduino may report that the Trinket wasn't found.. Just reset the trinket and try again.  

When the code uploads correctly, the builtin LED will flash 3 times as the code starts, then flash once every 3 seconds when it sends wakeup commands to the battery.  

I was able to verify and run this on a pair of these batteries in parallel (36v 25.6ah) as well as 4 batteries in parallel (36v 51.2ah) by tying pin 2 to all 4 blue wires.
