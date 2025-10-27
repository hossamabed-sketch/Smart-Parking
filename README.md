// ------- Slot 1 -------
#define TRIG1 14
#define ECHO1 27
#define RED1 32
#define GREEN1 33

// ------- Slot 2 -------
#define TRIG2 25
#define ECHO2 26
#define RED2 18
#define GREEN2 19

// ------- Slot 3 -------
#define TRIG3 4
#define ECHO3 5
#define RED3 21
#define GREEN3 22

void setup() {
  Serial.begin(115200);

  // إعداد البنّات لكل حساسات و LEDات
  pinMode(TRIG1, OUTPUT);
  pinMode(ECHO1, INPUT);
  pinMode(RED1, OUTPUT);
  pinMode(GREEN1, OUTPUT);

  pinMode(TRIG2, OUTPUT);
  pinMode(ECHO2, INPUT);
  pinMode(RED2, OUTPUT);
  pinMode(GREEN2, OUTPUT);

  pinMode(TRIG3, OUTPUT);
  pinMode(ECHO3, INPUT);
  pinMode(RED3, OUTPUT);
  pinMode(GREEN3, OUTPUT);
}

void loop() {
  // قراءة كل حساس
  int d1 = readDistance(TRIG1, ECHO1);
  int d2 = readDistance(TRIG2, ECHO2);
  int d3 = readDistance(TRIG3, ECHO3);

  Serial.print("Slot 1: ");
  Serial.print(d1);
  Serial.print(" cm  |  Slot 2: ");
  Serial.print(d2);
  Serial.print(" cm  |  Slot 3: ");
  Serial.print(d3);
  Serial.println(" cm");

  // التحكم في LEDات حسب المسافة
  controlLEDs(d1, RED1, GREEN1);
  controlLEDs(d2, RED2, GREEN2);
  controlLEDs(d3, RED3, GREEN3);

  delay(1000);
}

// دالة لقياس المسافة من حساس معين
int readDistance(int trigPin, int echoPin) {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  long duration = pulseIn(echoPin, HIGH, 20000);
  int distance = duration * 0.034 / 2;
  return distance;
}

// دالة للتحكم في الليدات حسب المسافة
void controlLEDs(int distance, int redPin, int greenPin) {
  if (distance > 0 && distance < 10) {   // في عربية
    digitalWrite(redPin, HIGH);
    digitalWrite(greenPin, LOW);
  } else if (distance >= 10) {           // المكان فاضي
    digitalWrite(redPin, LOW);
    digitalWrite(greenPin, HIGH);
  } else { // لو مفيش قراءة
    digitalWrite(redPin, LOW);
    digitalWrite(greenPin, LOW);
  }
}
