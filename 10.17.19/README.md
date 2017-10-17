# Arduino mini midterm

Our assignment was to create anything we wanted using the Arduino. I decided to use a plant as a "sensor" and have it output messages to the user.



## Video

[![Preview](video.png)](https://vimeo.com/238677426)

## Code

``` #include <LiquidCrystal.h>
#define min(a,b) (a<b?a:b)
     
const int numReadings = 10;
LiquidCrystal lcd(1, 2, 4, 5, 6, 7);
int readings[numReadings];      // the readings from the analog input
int readIndex = 0;              // the index of the current reading
int total = 0;                  // the running total
int average = 0;                // the average

int inputPin = A0;
boolean isTouching = false;

unsigned long previousMillis = 0;
long interval = 4000;

int numTouched = 0;

const char * responses[] = {
    "dun touch plz",
    "stop it",
    "stop it bitch",
    "i said",
    "STOP",
    "BRUH",
    "GET A LIFE YO",
    "I AM ON EDGE",
    "BETCH",
    "STOOOOP",
    "NOOOOOOW",
    "ouch that hurt!!",
    "STOP TOUCHING",
    "BROOOO",
    "GODDAMN",
    "U DON'T LISTEN",
    "do you even care",
   
    "BETCH",
    "STOOOOP",
    "NOOOOOOW",
    "SERIOUSLY DUDE",
    "I'M GONNA FREAK",
    "anyway",
    "bruh",
    "stop touching",
    "RUDE",
    ".............",
    
    
};

void setup() {
  // set up the LCD's number of columns and rows:
  lcd.begin(16, 2);

   digitalWrite(8, HIGH);
   // initialize all the readings to 0:
  for (int thisReading = 0; thisReading < numReadings; thisReading++) {
    readings[thisReading] = 0;
     
  }
}

void loop() {
   unsigned long currentMillis = millis();
   
  // subtract the last reading:
  total = total - readings[readIndex];
  // read from the sensor:
  readings[readIndex] = analogRead(inputPin);
  // add the reading to the total:
  total = total + readings[readIndex];
  // advance to the next position in the array:
  readIndex = readIndex + 1;

  // if we're at the end of the array...
  if (readIndex >= numReadings) {
    // ...wrap around to the beginning:
    readIndex = 0;
  }
 ;
  // calculate the average:
  average = total / numReadings;
  // send it to the computer as ASCII digits
  lcd.setCursor(0, 1);

  
 if(average<30 && !isTouching){
   
   numTouched++;

  // previousMillis = currentMillis;
   
   isTouching = true;

   
   
    lcd.clear();

    if(numTouched > 130) {
      lcd.setCursor(16,0);
      lcd.autoscroll();
     // char scream[] = "holy shIIIIIIIIT STOP";
      char scream[] = "holy shIIIIIIIIT STOP";
      for(int i = 0; i< sizeof(scream)/sizeof(char); i++) {
        lcd.print(scream[i]);
        delay(400);
      }
      lcd.noAutoscroll();
      lcd.clear();
      numTouched = 0;
    } else {
      lcd.print(responses[min(26,numTouched/5)]);
     // previousMillis = currentMillis;
    }
   // lcd.print(numTouched);
     
 
 } else if(average>=30 && isTouching){
   isTouching = false;
/*
   if(currentMillis - previousMillis > interval) {
    previousMillis = currentMillis;
    lcd.clear();
    lcd.print("ok cool");
    
   }*/
   // lcd.clear();
   //lcd.print("not touching");
 }
 
} ```


