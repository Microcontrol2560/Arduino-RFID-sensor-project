//RFID
#include <SPI.h>
#include <MFRC522.h>
#include <Servo.h>
 
 
#define SS_PIN 10 //RFID SDA pin
#define RST_PIN 9 //RFID reset pin
#define LED_B 4 //blue LED pin
#define LED_R 5 //red LED pin
#define BUZZER 2 //buzzer pin
MFRC522 mfrc522(SS_PIN, RST_PIN);   // Create MFRC522 instance.
Servo myServo; //servo name, the usual

//RFID uses the MFRC522 module
  
void setup() {

  Serial.begin(9600); // Initiate a serial communication
  SPI.begin();   // Initiate SPI bus
  mfrc522.PCD_Init(); // Initiate MFRC522 senser
  myServo.attach(3); //servo moved
  myServo.write(0); //servo start position
  pinMode(LED_B, OUTPUT);
  pinMode(LED_R, OUTPUT);
  pinMode(BUZZER, OUTPUT);
  noTone(BUZZER);
  Serial.println("PUT YOUR TAG/CARD TO THE SCANNER");
  Serial.println();
  

}
void loop() 
{
 
  
  if ( !mfrc522.PICC_IsNewCardPresent()) {// Look for new cards
    return;
  }
 
  if ( !mfrc522.PICC_ReadCardSerial()) { // Select one of the cards
    return;
  }
  
  Serial.print("UID tag :");//Show UID on serial monitor, get UID from Sketch 1[DumpINFO]
  String content= "";
  byte letter;
  for (byte i = 0; i < mfrc522.uid.size; i++) {
     Serial.print(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " ");
     Serial.print(mfrc522.uid.uidByte[i], HEX);
     content.concat(String(mfrc522.uid.uidByte[i] < 0x10 ? " 0" : " "));
     content.concat(String(mfrc522.uid.uidByte[i], HEX));
  }
  Serial.println();
  Serial.print("Message : ");
  content.toUpperCase();
  if (content.substring(1) == "29 5D 48 C1") //change here the UID of the card/cards that you want to give access here, use the DumpINFO sketch
  {
    Serial.println("Authorized access");
    Serial.print("CARD IS VALID, PLEASE ENTER");//change it to what you want
    delay(500);
    digitalWrite(LED_B, HIGH);
    tone(BUZZER, 500);
    delay(300);
    noTone(BUZZER);
    myServo.write(180);
    delay(5000);

    myServo.write(0);
    digitalWrite(LED_B, LOW);
  }
 
 else   {
    Serial.println(" Access denied");
    Serial.print("***REPORTED***");//change it to what you want
    digitalWrite(LED_R, HIGH);
    tone(BUZZER, 300);
    delay(5000);
    digitalWrite(LED_R, LOW);
    noTone(BUZZER);
  }
} 
