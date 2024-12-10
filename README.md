# SIH2024

#include <SoftwareSerial.h>

// Initialize Software Serial on pins 10 (RX) and 11 (TX)
SoftwareSerial sim(10, 11);

// Recipient phone number
String number = "+917745977908";

void setup() {
  delay(7000); // Wait for SIM800L to initialize and get a network signal
  Serial.begin(9600); // Start Serial Monitor for debugging
  sim.begin(9600); // Start communication with SIM800L
  Serial.println("System Initialized...");
}

void loop() {
  // Send the SMS
  SendMessage();
  
  // Wait before sending the next SMS (if loop is retained for multiple messages)
  while (true); // Remove this line if the message should be sent repeatedly
}

// Function to send an SMS
void SendMessage() {
  Serial.println("Sending SMS...");
  
  sim.println("AT+CMGF=1"); // Set the SIM800L to Text Mode
  delay(1000);

  sim.println("AT+CMGS=\"" + number + "\""); // Specify the recipient number
  delay(1000);

  sim.println("Hello, this is a test message from SIM800L!"); // SMS content
  delay(100);

  sim.println((char)26); // ASCII CTRL+Z to send the message
  delay(5000); // Wait for the SMS to be sent

  Serial.println("SMS Sent Successfully!");
}
