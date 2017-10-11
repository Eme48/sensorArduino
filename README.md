

//sensor

long tiempo;
float distancia;
int trig = 2;
int eco = 8;

//boton 
int enable = 4;
int estado;

//leds
int near = 7;
int medium = 6;
int far = 5;

void setup() {
  
  //sensor
  pinMode(trig,OUTPUT);
  pinMode(eco,INPUT);
  
  //leds
  pinMode(near, OUTPUT);
  pinMode(medium, OUTPUT);
  pinMode(far, OUTPUT);
  
  //Boton
  pinMode(enable,INPUT_PULLUP);
  estado = 0;
  
  Serial.begin(9600);
}

void loop() {

  int estado = digitalRead(enable);
  Serial.println(estado);
  if(estado == LOW){
    digitalWrite(trig, LOW);
    delayMicroseconds(4);
    digitalWrite(trig,HIGH);
    delayMicroseconds(10);
    digitalWrite(trig,LOW);

    tiempo = (pulseIn(eco,HIGH)/2);
    distancia = float(tiempo * 0.0343);

    
    delay(50);
    if(distancia <= 10){
      analogWrite(near, 255);
      analogWrite(medium,0);
      analogWrite(far,0);
    } else if(distancia >10 && distancia <=20){
      analogWrite(near,0);
      analogWrite(medium,255);
      analogWrite(far,0);
      
    } else if(distancia >20 && distancia <=30){
      analogWrite(near,0);
      analogWrite(medium,0);
      analogWrite(far,255);
 }
} else {
  analogWrite(near,0);
  analogWrite(medium,0);
  analogWrite(far,0);
}
}
