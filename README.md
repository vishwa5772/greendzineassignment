# greendzineassignment
#include <elapsedMillis.h>

// Define the analog pin connected to the LM35 temperature sensor
const int lm35Pin = A0;
// Define the pin connected to the onboard LED
const int ledPin = 13;

// Define intervals for LED blinking based on temperature
const int below30Interval = 250; // Blink every 250 milliseconds below 30 degrees Celsius
const int above30Interval = 500; // Blink every 500 milliseconds above 30 degrees Celsius

elapsedMillis ledTimer; // Timer for LED blinking

void setup() {
  pinMode(ledPin, OUTPUT); // Set the LED pin as an output
  Serial.begin(9600); // Begin serial communication for debugging (optional)
}

void loop() {
  int sensorValue = analogRead(lm35Pin); // Read the analog value from the LM35 temperature sensor

  float temperatureC = (sensorValue * 5.0 / 1024.0) * 100.0; // Convert the analog value to temperature in degrees Celsius

  Serial.print("Temperature: ");
  Serial.print(temperatureC);
  Serial.println(" C");

  // Check temperature conditions and control LED blinking
  if (temperatureC < 30.0) {
    blinkLED(below30Interval); // Blink LED every 250 milliseconds if temperature is below 30 degrees Celsius
  } else if (temperatureC > 30.0) {
    blinkLED(above30Interval); // Blink LED every 500 milliseconds if temperature is above 30 degrees Celsius
  }
}

// Function to blink the LED at specified intervals
void blinkLED(int interval) {
  if (ledTimer >= interval) {
    digitalWrite(ledPin, !digitalRead(ledPin)); // Toggle LED state
    ledTimer = 0; // Reset the timer
  }
}
