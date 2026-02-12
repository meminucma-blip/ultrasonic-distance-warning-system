const int trigPin = 9;
const int echoPin = 10;
const int buzzer = 8;

const int green = 2;
const int yellow1 = 3;
const int yellow2 = 4;
const int red1 = 5;
const int red2 = 6;

long duration;
int distance;

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(buzzer, OUTPUT);

  pinMode(green, OUTPUT);
  pinMode(yellow1, OUTPUT);
  pinMode(yellow2, OUTPUT);
  pinMode(red1, OUTPUT);
  pinMode(red2, OUTPUT);

  Serial.begin(9600);
}

void loop() {

  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2;

  Serial.println(distance);

  // Hepsini kapat
  digitalWrite(green, LOW);
  digitalWrite(yellow1, LOW);
  digitalWrite(yellow2, LOW);
  digitalWrite(red1, LOW);
  digitalWrite(red2, LOW);

  if(distance > 30){
    digitalWrite(green, HIGH);
    noTone(buzzer);
  }
  else if(distance > 20){
    digitalWrite(green, HIGH);
    digitalWrite(yellow1, HIGH);
    tone(buzzer, 400);
  }
  else if(distance > 15){
    digitalWrite(green, HIGH);
    digitalWrite(yellow1, HIGH);
    digitalWrite(yellow2, HIGH);
    tone(buzzer, 800);
  }
  else if(distance > 10){
    digitalWrite(yellow1, HIGH);
    digitalWrite(yellow2, HIGH);
    digitalWrite(red1, HIGH);
    tone(buzzer, 1200);
  }
  else{
    digitalWrite(red1, HIGH);
    digitalWrite(red2, HIGH);
    tone(buzzer, 2000);
  }

  delay(100);
}

## 🔧 System Logic

- Distance > 30 cm → Green LED
- 20–30 cm → Yellow warning
- 10–20 cm → Red warning
- <10 cm → Critical alert + fast buzzer

## 💻 Technologies Used
- Arduino C++
- Ultrasonic Sensor (HC-SR04)
- Non-blocking millis() timing
