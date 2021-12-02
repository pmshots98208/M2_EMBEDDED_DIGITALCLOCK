# REPORT

# ABOUT 

Digital wall clocks are common items seen in almost every household, office, and industry. It is a common but essential household item that allows us to get our bearings and gives us a sense of the day we are spending. Buying a new wall clock will generally cost you a bit more money than you would initially expect since it is the basic habit of shopkeepers to dupe their customers. But luckily there is a simple way of making a digital wall clock. So in today’s tutorial, we are going to go over a step by step procedure on how to design a DIY Digital Wall Clock Using Arduino ATMega328p 8-Bit AVR MCU IC.

# REQUIREMENTS

1)	MCU IC	Microchip ATMega328p-1
2)	Arduino Uno Board	Rev3, 8KB - 	1
3)	Crystal Oscillator	16MHz - 	1
4)	IC Base	28 – pin -	1
5)	7 – segment display	common anode -	4
6)	Capacitors	22pF -	2
7)	Resistors	220 Ohm, -  1K	28
8)	LED	5mm, -  3.5V	1
9)	Header Pins	Female/male - 	2
10)	Soldering Iron	45W – 65W - 	1
11)	Soldering Wire with Flux	–	1
12)	Pushbutton	–	1
13)	Toggle switch	–	2
14)	Veroboard	–	1
15)	DC Battery with Clip	3.7V	1
16)	Jumper Wires	–	As per need


## HIGH LEVEL REQUIREMENT

1. Atmega328p
2. Board
3. Display
4. LED
5. Aurdino

## LOW LEVEL REQUIREMENTS

1. CAPACITOR
2. RESISTOR
3. BATTERY
4. SOLDERING WIRE
5. JUMPER WIRE


# SWOT ANALYSIS

S = Strengths
W = Weaknesses
O = Opportunities
T = Threats

![SWOT](https://miro.medium.com/max/1838/1*I1yH8jt-AHGw4Aw61d_FnQ.png)

# 4W's & 1H's

### WHO?

Those who want to use digital feature.

### WHAT?

Display system, it's not analog.

### WHEN?

When you wnat to know time.

### WHERE?

Anywhere, Everywhere.

### HOW?

By watching, this is only thing you need to do.


# DESIGN

### ATMega328p Pinout

![PIN DIAGRAM](https://user-images.githubusercontent.com/94250186/144028947-c5a58f69-96c0-411d-8741-744b543833d4.png)

### REPRESENTATION

![SIMPLE REPRESENTATIONS](https://www.electronics360.org/wp-content/uploads/2021/01/10-1.jpg)


### COMMON CATHODEN & COMMON ANODE

![COMMON CATHODE](https://www.digikey.com/maker-media/c367faff-2f5d-499b-8b49-c8aacf047184)


# BLOCK DIAGRAM

![BLOCK DIAGRAM](https://b3van8qm1o7ou9d3b48qdhsg-wpengine.netdna-ssl.com/wp-content/uploads/2019/07/Block-Diagram-Arduino-RTC-DS1307-Based-Digital-Clock-Alarm.png)


# SIMULATIONS


![SIMULATIONS](https://www.technicalmarket.in/wp-content/uploads/2019/03/LED-CLOCK-CIRCUIT-3-1024x698.jpg)



# BILL OF MATERILS


| S.NO. | MATERIAL | QUANTITY | PRICE(INR)|
|--------|:---------|:----------|:----------|
| 1 | MCU IC Microchip ATMega328p | 1 |800 |
| 2 | Crystal Oscillator 16MHz | 1 |80 |
| 3 | IC Base 28 – pin | 1 |80 |
| 4 | 7 – segment display common anode | 4 |520 |
| 5 | Capacitors 22pF  | 2 |20 |
| 6 | Header Pins Female/male   | 2 |160 |
| 7 | Soldering Iron 45W – 65W   | 1 |120|
| 8 |Soldering Iron 45W – 65W  | 1 |299|
| 9 |DC Battery with Clip 3.7V  | 1 |209|
| 9 |Jumper Wires | - |-|

# CODE

#if ARDUINO >= 100
#include <Arduino.h> 
#else
#include <WProgram.h> 
#endif

#include "TimeLib.h"

static tmElements_t tm;          // a cache of time elements
static time_t cacheTime;   // the time the cache was updated
static uint32_t syncInterval = 300;  // time sync will be attempted after this many seconds

void refreshCache(time_t t) {
  if (t != cacheTime) {
    breakTime(t, tm); 
    cacheTime = t; 
  }
}

int hour() { // the hour now 
  return hour(now()); 
}

int hour(time_t t) { // the hour for the given time
  refreshCache(t);
  return tm.Hour;  
}

int hourFormat12() { // the hour now in 12 hour format
  return hourFormat12(now()); 
}

int hourFormat12(time_t t) { // the hour for the given time in 12 hour format
  refreshCache(t);
  if( tm.Hour == 0 )
    return 12; // 12 midnight
  else if( tm.Hour  > 12)
    return tm.Hour - 12 ;
  else
    return tm.Hour ;
}

uint8_t isAM() { // returns true if time now is AM
  return !isPM(now()); 
}

uint8_t isAM(time_t t) { // returns true if given time is AM
  return !isPM(t);  
}

uint8_t isPM() { // returns true if PM
  return isPM(now()); 
}

uint8_t isPM(time_t t) { // returns true if PM
  return (hour(t) >= 12); 
}

int minute() {
  return minute(now()); 
}

int minute(time_t t) { // the minute for the given time
  refreshCache(t);
  return tm.Minute;  
}

int second() {
  return second(now()); 
}

int second(time_t t) {  // the second for the given time
  refreshCache(t);
  return tm.Second;
}

int day(){
  return(day(now())); 
}

int day(time_t t) { // the day for the given time (0-6)
  refreshCache(t);
  return tm.Day;
}

int weekday() {   // Sunday is day 1
  return  weekday(now()); 
}

int weekday(time_t t) {
  refreshCache(t);
  return tm.Wday;
}
   
int month(){
  return month(now()); 
}

int month(time_t t) {  // the month for the given time
  refreshCache(t);
  return tm.Month;
}

int year() {  // as in Processing, the full four digit year: (2009, 2010 etc) 
  return year(now()); 
}

int year(time_t t) { // the year for the given time
  refreshCache(t);
  return tmYearToCalendar(tm.Year);
}

/*============================================================================*/	
/* functions to convert to and from system time */
/* These are for interfacing with time serivces and are not normally needed in a sketch */

// leap year calulator expects year argument as years offset from 1970
#define LEAP_YEAR(Y)     ( ((1970+(Y))>0) && !((1970+(Y))%4) && ( ((1970+(Y))%100) || !((1970+(Y))%400) ) )

static  const uint8_t monthDays[]={31,28,31,30,31,30,31,31,30,31,30,31}; // API starts months from 1, this array starts from 0
 
void breakTime(time_t timeInput, tmElements_t &tm){
// break the given time_t into time components
// this is a more compact version of the C library localtime function
// note that year is offset from 1970 !!!

  uint8_t year;
  uint8_t month, monthLength;
  uint32_t time;
  unsigned long days;

  time = (uint32_t)timeInput;
  tm.Second = time % 60;
  time /= 60; // now it is minutes
  tm.Minute = time % 60;
  time /= 60; // now it is hours
  tm.Hour = time % 24;
  time /= 24; // now it is days
  tm.Wday = ((time + 4) % 7) + 1;  // Sunday is day 1 
  
  year = 0;  
  days = 0;
  while((unsigned)(days += (LEAP_YEAR(year) ? 366 : 365)) <= time) {
    year++;
  }
  tm.Year = year; // year is offset from 1970 
  
  days -= LEAP_YEAR(year) ? 366 : 365;
  time  -= days; // now it is days in this year, starting at 0
  
  days=0;
  month=0;
  monthLength=0;
  for (month=0; month<12; month++) {
    if (month==1) { // february
      if (LEAP_YEAR(year)) {
        monthLength=29;
      } else {
        monthLength=28;
      }
    } else {
      monthLength = monthDays[month];
    }
    
    if (time >= monthLength) {
      time -= monthLength;
    } else {
        break;
    }
  }
  tm.Month = month + 1;  // jan is month 1  
  tm.Day = time + 1;     // day of month
}

time_t makeTime(const tmElements_t &tm){   
// assemble time elements into time_t 
// note year argument is offset from 1970 (see macros in time.h to convert to other formats)
// previous version used full four digit year (or digits since 2000),i.e. 2009 was 2009 or 9
  
  int i;
  uint32_t seconds;

  // seconds from 1970 till 1 jan 00:00:00 of the given year
  seconds= tm.Year*(SECS_PER_DAY * 365);
  for (i = 0; i < tm.Year; i++) {
    if (LEAP_YEAR(i)) {
      seconds +=  SECS_PER_DAY;   // add extra days for leap years
    }
  }
  
  // add days for this year, months start from 1
  for (i = 1; i < tm.Month; i++) {
    if ( (i == 2) && LEAP_YEAR(tm.Year)) { 
      seconds += SECS_PER_DAY * 29;
    } else {
      seconds += SECS_PER_DAY * monthDays[i-1];  //monthDay array starts from 0
    }
  }
  seconds+= (tm.Day-1) * SECS_PER_DAY;
  seconds+= tm.Hour * SECS_PER_HOUR;
  seconds+= tm.Minute * SECS_PER_MIN;
  seconds+= tm.Second;
  return (time_t)seconds; 
}
/*=====================================================*/	
/* Low level system time functions  */

static uint32_t sysTime = 0;
static uint32_t prevMillis = 0;
static uint32_t nextSyncTime = 0;
static timeStatus_t Status = timeNotSet;

getExternalTime getTimePtr;  // pointer to external sync function
//setExternalTime setTimePtr; // not used in this version

#ifdef TIME_DRIFT_INFO   // define this to get drift data
time_t sysUnsyncedTime = 0; // the time sysTime unadjusted by sync  
#endif


time_t now() {
	// calculate number of seconds passed since last call to now()
  while (millis() - prevMillis >= 1000) {
		// millis() and prevMillis are both unsigned ints thus the subtraction will always be the absolute value of the difference
    sysTime++;
    prevMillis += 1000;	
#ifdef TIME_DRIFT_INFO
    sysUnsyncedTime++; // this can be compared to the synced time to measure long term drift     
#endif
  }
  if (nextSyncTime <= sysTime) {
    if (getTimePtr != 0) {
      time_t t = getTimePtr();
      if (t != 0) {
        setTime(t);
      } else {
        nextSyncTime = sysTime + syncInterval;
        Status = (Status == timeNotSet) ?  timeNotSet : timeNeedsSync;
      }
    }
  }  
  return (time_t)sysTime;
}

void setTime(time_t t) { 
#ifdef TIME_DRIFT_INFO
 if(sysUnsyncedTime == 0) 
   sysUnsyncedTime = t;   // store the time of the first call to set a valid Time   
#endif

  sysTime = (uint32_t)t;  
  nextSyncTime = (uint32_t)t + syncInterval;
  Status = timeSet;
  prevMillis = millis();  // restart counting from now (thanks to Korman for this fix)
} 

void setTime(int hr,int min,int sec,int dy, int mnth, int yr){
 // year can be given as full four digit year or two digts (2010 or 10 for 2010);  
 //it is converted to years since 1970
  if( yr > 99)
      yr = yr - 1970;
  else
      yr += 30;  
  tm.Year = yr;
  tm.Month = mnth;
  tm.Day = dy;
  tm.Hour = hr;
  tm.Minute = min;
  tm.Second = sec;
  setTime(makeTime(tm));
}

void adjustTime(long adjustment) {
  sysTime += adjustment;
}

// indicates if time has been set and recently synchronized
timeStatus_t timeStatus() {
  now(); // required to actually update the status
  return Status;
}

void setSyncProvider( getExternalTime getTimeFunction){
  getTimePtr = getTimeFunction;  
  nextSyncTime = sysTime;
  now(); // this will sync the clock
}

void setSyncInterval(time_t interval){ // set the number of seconds between re-sync
  syncInterval = (uint32_t)interval;
  nextSyncTime = sysTime + syncInterval;
}




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


### The five components of a data communication network are:
1. Data
2. Sender
3. Receiver
4. Transmission Medium
5. Protocol

# SOURCE CODE

The code for the microcontroller section is written in embedded C and compiled using AVR-GCC (WinAVR) .
Hex code is  uploaded into Atmega328p with AVRDUDE using USBasp Programmer. 

### Asynchronous Communication:

The asynchronous communication there is no need for any clock line.

In some cases the sender and receiver agree upon some predefined clock period and generate their own clock pules and use them for extracting the information from the bit stream and in others the sender sends the data at a fixed rate and the receiver has the ability to measure the duration of each pulse to determine the length of each bit.

### Synchronous Communication:

In the synchronous type, one of the devices indulging in the communication has to generate the clock pulse and source it to the other devices in the the bus.

Typically the device that generated the clock is called the Master and it starts the conversation. The clock pulse sent out by the master is used by the slaves to determine the length of each bit in the coming data stream.

# Hardware Connection Setup  

We are using a 32 pin TQFP version of the ATmega328p microcontroller .If you are using the 28 pin DIP version,please make sure that the pin numbers  match by referring to the data sheet of ATmega328p.

TXD of ATmega328 is connected to RXD of USB to Serial Converter THEN, RXD of ATmega328 is connected to TXD of USB to Serial Converter.

In our case we are using the 8N1 setup ie 

1. 1 Start Bit
2. 8 Data Bits
3. No Parity 
4. 1 Stop Bit

### USART

USART Control and Status Register 0 B or UCSR0B contains the bits for configuring the USART as Transmitter,Receiver or Both.

1. Enabling TXEN0 bit configures USART as  Transmitter
2. Enabling RXEN0 bit configures USART as Receiver 


![USART](https://binaryupdates.com/wp-content/uploads/FRAME-DATABITS-USART.jpg)

![USART](https://binaryupdates.com/wp-content/uploads/FRAME-DATABITS-USART.jpg)




# IMAGES


![DGM](https://www.technicalmarket.in/wp-content/uploads/2019/03/LED-CLOCK-CIRCUIT-3-1024x698.jpg)







![DISPLAY](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcR6yM1PhLwxlAqd4R3o2liTgLKCtaozEumghw&usqp=CAU)







![AVR](https://lh3.googleusercontent.com/proxy/jv2I3kzxfXvTPK1UzLg071n03vdzzcOgWx2Uk7GBd-IR2NPmMebBrSIupw0bFzaSR4e6dXQQOgtcOH67HaKCrGehbJ63D_N_QNFU7L0)


