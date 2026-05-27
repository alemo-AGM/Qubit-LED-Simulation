//code for quantum computer simulation

//declaring pins used on nano
const int latch =3;
const int clock =5;
const int data = 7; //data pin
const int potent = 1; //potentiometer

int delayTime; //delay between qubyte changes
int potVal; //value of potentiometer

int letterOutputs[4]; //record bytes of every output in set

int randomLetter(){
  //should return # 65-77 inclusive
  //-->represents an uppercase letter in ASCII
  return random(65, 77);
}

void updateRegisters(){
  digitalWrite(latch, LOW);

  //send to 4 shift registers
  for (int i = 0; i<4; i++){
    int currentLetter = randomLetter();
    shiftOut(data, clock, MSBFIRST, currentLetter);
    //sends to last register first, pushes byte of the letter
    letterOutputs[i] = currentLetter;
  }
  digitalWrite(latch, HIGH);
  printOutput();
}


void printOutput(){
  //(char)letterOutput[i] sends back the letter
  for (int i = 3; i>=0; i--){
    int curIndex = (char)letterOutputs[i];
    Serial.print(curIndex);
  }
  Serial.println("**********");
  int letterOutput[4]; //reset array for next set
}

void setup() {
  pinMode(latch, OUTPUT);
  pinMode(clock, OUTPUT);
  pinMode(data, OUTPUT);
  pinMode(potent, INPUT);
  Serial.begin(9600);
}

void loop() {
  updateRegisters();

  //get potentiometer reading then map it onto delay value
  potVal = analogRead(potent);
  delayTime = map(potVal, 0 ,1023, 50, 1000);
  delay(delayTime);

}
