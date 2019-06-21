/*
  2 dice 4-digit 7-segment Display

*/

int latchPin = 12;          // Pin connected to ST_CP of 74HC595（Pin12）
int clockPin = 13;          // Pin connected to SH_CP of 74HC595（Pin11）
int dataPin = 11;           // Pin connected to DS of 74HC595（Pin14）
int comPin[] = {7, 6, 5, 4};// Common pin (anode) of 4 digit 7-segment display
int buttonPin = 8;

// Define the encoding of characters 0-F of the common-anode 7-Segment Display
byte num[] = {0xc0, 0xf9, 0xa4, 0xb0, 0x99, 0x92, 0x82, 0xf8, 0x80, 0x90, 0x88, 0x83, 0xc6, 0xa1, 0x86, 0x8e};

void chooseCommon(byte com) {
  // Close all single 7-segment display
  for (int i = 0; i < 4; i++) {
    digitalWrite(comPin[i], LOW);
  }
  // Open the selected single 7-segment display
  digitalWrite(comPin[com], HIGH);
}

void writeData(int value) {
  // Make latchPin output low level
  digitalWrite(latchPin, LOW);
  // Send serial data to 74HC595
  shiftOut(dataPin, clockPin, LSBFIRST, value);
  // Make latchPin output high level, then 74HC595 will update the data to parallel output
  digitalWrite(latchPin, HIGH);
}

void setup() {
  // set pins to output
  pinMode(buttonPin, INPUT);
  pinMode(latchPin, OUTPUT);
  pinMode(clockPin, OUTPUT);
  pinMode(dataPin, OUTPUT);
  for (int i = 0; i < 4; i++) {
    pinMode(comPin[i], OUTPUT);
  }
}

int i = 0;
int j = 0;
void loop() {
  chooseCommon(1);
  writeData(num[i]);
  delay(1);
  writeData(0xff);
  chooseCommon(3);
  writeData(num[j]);
  delay(1);
  writeData(0xff);
  if(digitalRead(buttonPin) == LOW){
     i = random(1,7); 
     j = random(1,7);
  }

}
