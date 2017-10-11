
//sensor

long tiempo;
  long distancia;

int trig = 2;
int eco = 8;
//boton

int estado = 0;
int entradaBoton = 4;
int salidaBoton = 3;

//focos

int diez = 7;
int veinte = 6;
int treinta = 5;

void setup() {
 Serial.begin(9600);
  pinMode(trig,OUTPUT);
  pinMode(eco,INPUT);
  
  pinMode(diez,OUTPUT);
  pinMode(veinte,OUTPUT);
  pinMode(treinta,OUTPUT);
  
  pinMode(3,OUTPUT);
  pinMode(4,INPUT);
}

void loop() {

  estado = digitalRead(4);
  digitalWrite(3,estado);


  digitalWrite(trig,LOW);
  delayMicroseconds(4);
  digitalWrite(trig,HIGH);
  delayMicroseconds(10);
  digitalWrite(trig,LOW);

  tiempo = pulseIn(eco,HIGH);
  distancia = tiempo/(29*2);


  delay(50);
  if(distancia <=10){
    analogWrite(diez,235);
    analogWrite(veinte,0);
    analogWrite(treinta,0);
    } else if(distancia >10 && distancia <=20){
    analogWrite(diez,0);
    analogWrite(veinte,255);
    analogWrite(treinta,0);
      
    } else if(distancia >20 && distancia <=30){
    analogWrite(diez,0);
    analogWrite(veinte,0);
    analogWrite(treinta,255); 
     }


}
