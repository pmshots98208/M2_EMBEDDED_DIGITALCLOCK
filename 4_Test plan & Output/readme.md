
# STEPS TO DESIGN THE SYSTEM & TESTING


1) Solder the two 7 – segment display LEDs (to display hours) on the veroboard.

 
2) Solder the two separator LEDs (to display seconds) on the Veroboard.


3) After that, solder the remaining two 7 – segment displays (to display minutes) on the Veroboard.


4) Now solder the toggle switch on the veroboard to connect the four 7 – segment displays together.


5) After that, solder the remaining two pushbuttons on the Veroboard to set the hours and minutes respectively.


6) After that, solder the 28 – pin IC base on the veroboard.


7) Now connect the second toggle switch to control the power to the circuit.


8) Solder the A, B, F, G pin of all seven segment LEDs in parallel with each other using a 220 Ohm resistor. After that, Solder the E, D & C pin of all seven segment LEDs in parallel with each other using a 220 Ohm resistor.


9) Solder the +ve terminal of the seconds LEDs with a 1K resistor to the Vcc of the circuit and -ve pin with the GND of the circuit.


10) After that, solder two 22pF capacitors with a crystal oscillator connected in parallel between them. Join them between pin 9 & 10 of the IC.


11) After that, place your ATMega328p DIP in the Arduino IC socket and burn the code provided below


12) Connect the IC back to your clock circuit.


13) Power up and test the circuit.


# WORKING & TESTING

The working of this circuit is as follows. the 4 seven-segment LEDs comprise the hours and minutes dials of the clock while the 2 LEDs in the middle represent the second dial of the clock, blinking at every half a second. The operation of this clock is primarily dependent upon setting the appropriate clock cycle of the ATMega328p. In order to do that, connect two 22pF capacitors in parallel with a 16MHz crystal oscillator.


