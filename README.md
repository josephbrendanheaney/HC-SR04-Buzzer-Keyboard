# HC-SR04 AIR KEYBOARD
C# code for the Arduino IDE using the ultrasonic sensor and the buzzer to recreate the leftmost C to B inclusive white keys on a keyboard. Place the sensor directly to the left of where the 'air keyboard' will start.
// Joseph Heaney - Air keyboard finished with pulse echo sensor.
// Connected buzzer negative pin to ground rail with 220 ohm resistor. This gives a good, quieter volume.
// Joseph Heaney - Air keyboard finished with pulse echo sensor.
// Connected buzzer negative pin to ground rail with 220 ohm resistor. This gives a good, quieter volume.

const int trigPin = 5;
const int echoPin = 6;
const int buzzerPin = 3;

void setup()
{
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(buzzerPin, OUTPUT);
  Serial.begin(131); // D
}

void loop()
{
  long duration;
  int distance;
  int frequency;

  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  // Get the time duration until recieved and calculate distance.
  duration = pulseIn(echoPin, HIGH, 50000); // The code continues after 50 ms if no wave is recieved back.
  distance = duration * 0.0343 / 2; // Accurate speed of sound, but in room temp.

  // Approximate white key frequencies from C.
  if (distance <= 5)
  {
    frequency = 131;   
  } 
  else if (distance <= 10)
  {
    frequency = 147;
  } 
  else if (distance <= 15)
  {
    frequency = 165;
  } 
  else if (distance <= 20)
  {
    frequency = 175;
  } 
  else if (distance <= 25)
  {
    frequency = 196;
  } 
  else if (distance <= 30)
  {
    frequency = 220;
  } 
  else if (distance <= 35)
  {
    frequency = 247;
  } 
  else if (distance <= 40)
  {
    frequency = 262;
  }

  // Play the note with the buzzer.
  tone(buzzerPin, frequency);

  // Wait before next reading of distance and next tone.
  delay(60); // 60 recommended by manufacturer to avoid echo interference.
}
