```
int inp1 = 52;
int inp2 = 53;
int inp3 = 50;
int inp4 = 51;
int inp5 = 30;
int inp6 = 31;
int inp7 = 32;
int inp8 = 33;
int enb1 = 2;
int enb2 = 3;
int enb3 = 4;
int enb4 = 5;
int stby1 = 48;
int stby2 = 22;


int trig = 46;
int echo = 47;
int destince;
int right_destince;
int left_destince;
unsigned long travelTime;

unsigned long eventsTimes[100];
char movesTypes[100];


void setup() {
    for (byte i=50; i<54; i++) {
        pinMode(i, OUTPUT);
    }

    for (byte i=30; i<34; i++) {
        pinMode(i, OUTPUT);
    }

    for (byte i=2; i<6; i++) {
        pinMode(i, OUTPUT);
    }

    pinMode(trig, OUTPUT);
    pinMode(echo, INPUT);

    pinMode(stby1, OUTPUT);
    pinMode(stby2, OUTPUT);
    digitalWrite(stby1, HIGH);
    digitalWrite(stby2, HIGH);

    Serial.begin(9600);
}

void moveForward() {
    digitalWrite(inp1, HIGH);
    digitalWrite(inp2, LOW); // down right
    digitalWrite(inp3, LOW);
    digitalWrite(inp4, HIGH); // up right
    digitalWrite(inp5, HIGH);
    digitalWrite(inp6, LOW); // up left
    digitalWrite(inp7, HIGH);
    digitalWrite(inp8, LOW); // down left

    analogWrite(enb1, 200);
    analogWrite(enb2, 200);
    analogWrite(enb3, 200);
    analogWrite(enb4, 200);
}

void moveBackward() {
    digitalWrite(inp1, LOW);
    digitalWrite(inp2, HIGH);
    digitalWrite(inp3, HIGH);
    digitalWrite(inp4, LOW);
    digitalWrite(inp5, LOW);
    digitalWrite(inp6, HIGH);
    digitalWrite(inp7, LOW);
    digitalWrite(inp8, HIGH);

    analogWrite(enb1, 200);
    analogWrite(enb2, 200);
    analogWrite(enb3, 200);
    analogWrite(enb4, 200);
}

void turnLeft() {
    digitalWrite(inp1, HIGH);
    digitalWrite(inp2, LOW);
    digitalWrite(inp3, HIGH);
    digitalWrite(inp4, LOW);
    digitalWrite(inp5, HIGH);
    digitalWrite(inp6, LOW);
    digitalWrite(inp7, LOW);
    digitalWrite(inp8, HIGH);

    analogWrite(enb1, 200);
    analogWrite(enb2, 200);
    analogWrite(enb3, 200);
    analogWrite(enb4, 200);
}

void turnRight() {
    digitalWrite(inp1, LOW);
    digitalWrite(inp2, HIGH);
    digitalWrite(inp3, LOW);
    digitalWrite(inp4, HIGH);
    digitalWrite(inp5, LOW);
    digitalWrite(inp6, HIGH);
    digitalWrite(inp7, HIGH);
    digitalWrite(inp8, LOW);

    analogWrite(enb1, 200);
    analogWrite(enb2, 200);
    analogWrite(enb3, 200);
    analogWrite(enb4, 200);
}

void stop() {
  for (byte i=200; i>0; i-=20) {
    analogWrite(enb1, i);
    analogWrite(enb2, i);
    analogWrite(enb3, i);
    analogWrite(enb4, i);
    delay(60);
  }
}

void loop() {
  digitalWrite(trig, LOW);
  delayMicroseconds(10);
  digitalWrite(trig, HIGH);
  delayMicroseconds(10);
  digitalWrite(trig, LOW);

  travelTime = pulseIn(echo, HIGH);
  destince = (travelTime / 2) * 0.0343;

  if (destince<20) {
    moveBackward();
    delay(800);
    stop();

    turnRight();
    delay(1000);
    stop();
    
    digitalWrite(trig, HIGH);
    delayMicroseconds(10);
    digitalWrite(trig, LOW);
    travelTime = pulseIn(echo, HIGH);
    right_destince = (travelTime / 2) * 0.0343;

    turnLeft();
    delay(2000);
    stop();

    digitalWrite(trig, HIGH);
    delayMicroseconds(10);
    digitalWrite(trig, LOW);
    travelTime = pulseIn(echo, HIGH);
    left_destince = (travelTime / 2) * 0.0343;

    if (right_destince > left_destince) {
      
    }

    else if (left_destince == right_destince) {
      turnLeft();
      delay(1700);
      stop();
    }
  }

  moveForward();
  delay(30);
}

```
