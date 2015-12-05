//First Week: Figured out how to sense moisture with the steel nails code below. I had an issue initally setting the state to my string. I initally had it as a boolean not a string. 

const int analogInPin = A0;  // Analog input pin that the potentiometer is attached to
const int analogOutPin = 9; // Analog output pin that the LED is attached to

int sensorValue = 0;        // value read from the pot
int outputValue = 0;
String state = "NEEDS WATER";
void setup() {
  // initialize serial communications at 9600 bps:
  Serial.begin(9600);
  pinMode(analogOutPin, INPUT);
void loop() 
sensorValue = analogRead(analogInPin);
  // map it to the range of the analog out:
  outputValue = map(sensorValue, 0, 1023, 0, 1023);
  // change the analog out value:
  if (outputValue < 1 && state.equals("WATERED"))
  {
    state = "NEEDS WATER";
    }
  }
  if (outputValue >= 1 && state.equals("NEEDS WATER")) {
    state = "WATERED" ;
  }

  // print the results to the serial monitor:
  Serial.print("sensor = " );
  Serial.println(outputValue);
  Serial.println(state);


  // wait 2 milliseconds before the next loop
  // for the analog-to-digital converter to settle
  // after the last reading:
  delay(150);
}

//Week 2: I was Asbsent in chicago for thanksgiving no work done this week. 
Week 3: Brought in LED strips and figured out how to control them with the UNO. I needed transistors to restrict the voltage to the LEDS. 
I cut together code I found online to fade in and out the colors. After this was done I changed the code so I only used BLUE and GREEN.
I made the LEDS always BLUE on high but the green would fade in and out depending on the moisture of the soil. 


const int analogInPin = A0;  // Analog input pin that the potentiometer is attached to
const int analogOutPin = 9; // Analog output pin that the LED is attached to

int sensorValue = 0;        // value read from the pot
int outputValue = 0;
String state = "NEEDS WATER";
#define REDPIN 5
#define GREENPIN 5
#define BLUEPIN 6

#define FADESPEED 20     // make this higher to slow down

void setup() {
  // initialize serial communications at 9600 bps:
  Serial.begin(9600);
  pinMode(analogOutPin, INPUT);
  pinMode(REDPIN, OUTPUT);
  pinMode(GREENPIN, OUTPUT);
  pinMode(BLUEPIN, OUTPUT);
}

void loop() {
  int r, g, b;
  analogWrite(GREENPIN, 255);
  // read the analog in value:
  sensorValue = analogRead(analogInPin);
  // map it to the range of the analog out:
  outputValue = map(sensorValue, 0, 1023, 0, 1023);
  // change the analog out value:
  if (outputValue < 1 && state.equals("WATERED"))
  {
    state = "NEEDS WATER";
    for (b = 0; b < 255; b++) {
      analogWrite(BLUEPIN, b);
      delay(FADESPEED);
      
    }
  }
  if (outputValue >= 1 && state.equals("NEEDS WATER")) {
    state = "WATERED" ;
    // fade from yellow to green
    for (b = 255; b > 0; b--) {
      analogWrite(BLUEPIN, b);
      delay(FADESPEED);
    }
  }

  // print the results to the serial monitor:
  Serial.print("sensor = " );
  Serial.println(outputValue);
  Serial.println(state);


  // wait 2 milliseconds before the next loop
  // for the analog-to-digital converter to settle
  // after the last reading:
  delay(150);
}
Week 4: All hell breaks loose. Anarchy in the streets. Millions dead. Temboo system for sending emails or texts is terrible. I got the wifi shield to work but could never make the Arduino send an email or text even tried making a separate twitter for my plants. Nothing worked. The wifi shield would boot up and connect correctly but no emails or texts would be sent from the Arduino. 
no hope left. tell my mother I loved her. ☠
