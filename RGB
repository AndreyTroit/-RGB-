#include <VolAnalyzer.h>

#define MIC_PIN A1
#define CLAP_LVL 100
#define WINDOW_MIN 300
#define WINDOW_MAX 500
int BLU = 8;
int GRN = 9;
int RED = 10;


VolAnalyzer VA (MIC_PIN);

void setup(){
  Serial.begin(9600);
  pinMode(RED, INPUT);
  pinMode(RED, OUTPUT);
  pinMode(GRN, INPUT);
  pinMode(GRN, OUTPUT);
  pinMode(BLU, INPUT);
  pinMode(BLU, OUTPUT);
}

void loop(){
  static uint32_t timer = millis();
  static uint8_t counter = 0;

  if(VA.tick()){
    if(VA.pulse() && (VA.getMax() >= CLAP_LVL)){
      if((millis() - timer) >= WINDOW_MIN && (millis() - timer) <= WINDOW_MAX){
        counter++;
      } else counter = 0;
      timer = millis();
    }
    if(counter && (millis() - timer) >= WINDOW_MAX){
      Serial.println(counter + 1);
      if(counter == 1){
        digitalWrite(RED, !digitalRead(RED));
        digitalWrite(GRN, LOW);
        digitalWrite(BLU, LOW);
      }
      if(counter == 2){
        digitalWrite(RED, LOW);
        digitalWrite(GRN, !digitalRead(GRN));
        digitalWrite(BLU, LOW);
      }
      if(counter == 3){
        digitalWrite(RED, LOW);
        digitalWrite(GRN, LOW);
        digitalWrite(BLU, !digitalRead(BLU));
      }
      if(counter == 4){
        digitalWrite(RED, HIGH);
        digitalWrite(GRN, HIGH);
        digitalWrite(BLU, HIGH);
      }
      counter = 0;
    } 
  }
}
