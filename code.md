# POC-Embedded-system-NE1-groupe-1

#include <LiquidCrystal.h>
#include <SoftwareSerial.h>

/*
the push button is connected to the pin 2 for a INPUT_PULLUP mode
the led is connected to the pin 4 with a resistance of 220Ω

//declaration of the variables
int pinBouton, pinLed;
boolean etatAllumage;
int pinBouton1, pinLed1;
boolean etatAllumage1;

SoftwareSerial BTserial(0,1); // RX | TX
LiquidCrystal lcd(12,11,5,4,3,2);

const int AOUTpin = A0;    // pin that the sensor is attached to arduino
const int DOUTpin=8; //The DOUT pin of the CO sensor goes into digital pin D8 of the arduino
int limit;
int value;

void setup()
{
  //initialisation des variables
  Serial.begin(9600);
  pinBouton = 7;
  pinLed = 6;
  etatAllumage=0;
  pinBouton1 = 10;
  pinLed1 = 9;
  etatAllumage1=0;
  
  //definition of the modes
  pinMode(pinBouton, INPUT_PULLUP);
  pinMode(pinLed, OUTPUT);
  pinMode(pinBouton1, INPUT_PULLUP);
  pinMode(pinLed1, OUTPUT);
  
  pinMode(DOUTpin,INPUT); //set the CO DOut pin as a an input to the arduino
  lcd.begin(16,2);
  BTserial.begin(9600);
}
void loop()
{
  Serial.print(etatAllumage);
    
    
  int CO = analogRead(AOUTpin);
  limit=digitalRead(DOUTpin);
  lcd.print("CO: ");
  lcd.print(CO);
  BTserial.print(CO);
  BTserial.print(";");
  //lcd.print(" ppm");
  delay(1000);
  lcd.clear();
  
  if(CO>=400)
  {
    lcd.setCursor(0,1);
    lcd.print("BAD");
  }
    if(CO<=400)
  {
    lcd.setCursor(0,1);
    lcd.print("OK");
    
  }
  lcd.setCursor(0,0);
  
  if (etatAllumage) //we test if etatAllumage is equal to 1
  {
    digitalWrite(pinLed, HIGH);   // turn the LED on (HIGH is the voltage level)
    delay(250);                       // wait for a second
    digitalWrite(pinLed, LOW);    // turn the LED off by making the voltage LOW
    delay(250);         
  }
  else 
  {
    digitalWrite(pinLed, LOW); //on éteint la LED
  }
  //lecture de l'état du bouton et stockage dans etatBouton
  boolean etatPinBouton = digitalRead(pinBouton);
  Serial.println(etatPinBouton);
  //test des conditions
  if (!etatPinBouton)//if button is pushed (so the pin indicates 0 ecause it is in mode INPUT_PULLUP)
  {
    if (etatAllumage) //if etatAllumage is equal to 1
    {
      etatAllumage=0; //we pass it to 0
    }
    else //sinon
    {
      etatAllumage=1; //we pass it to 1
    }
  }
  Serial.print(etatAllumage1);
  
  if (etatAllumage1) //we test if etatAllumage1 is equal to 1
  {
    digitalWrite(pinLed1, HIGH);   // turn the LED on (HIGH is the voltage level)
    delay(250);                       // wait for a second
    digitalWrite(pinLed1, LOW);    // turn the LED off by making the voltage LOW
    delay(250);         
  }
  else
  {
    digitalWrite(pinLed1, LOW); //we light off the led
  }
  //reading of the button's state and save it in etatBouton
  boolean etatPinBouton1 = digitalRead(pinBouton1);
  Serial.println(etatPinBouton1);
  //test of conditions
  if (!etatPinBouton1)//if button is pushed (so the pin indicates 0 ecause it is in mode INPUT_PULLUP)
  {
    if (etatAllumage1) //if etatAllumage1 is equal to 1
    {
      etatAllumage1=0; //we pass it to 0
    }
    else //sinon
    {
      etatAllumage1=1; //we pass it to 1
    }
  }
  delay(200);
}
