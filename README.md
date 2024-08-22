const int pinSensorD = A0;
const int pinSensorE = A1;

 const int pinMotorA1A = 5;
 const int pinMotorA1B = 6;
 const int pinMotorB1A = 9;
 const int pinMotorB1B = 10;

int velocidade = 255; // Define Velocidade

void setup() {
// Sensores
 pinMode(pinSensorD, INPUT); //Sensor Direito Entrada de Dados 
 pinMode(pinSensorE, INPUT);// Sensor Esquerdo Entrada de Dados

 pinMode(pinMotorA1B, OUTPUT);// Motor Esquerdo
 pinMode(pinMotorA1A, OUTPUT);
 pinMode(pinMotorB1B, OUTPUT); // Motor Direito
 pinMode(pinMotorB1A, OUTPUT);

}

void loop() {

  int estadoD = !digitalRead(pinSensorD); //  Leitura do Sensor Direito
  int estadoE = !digitalRead(pinSensorE); // Leitura do Sensor Esquerdo
    
  if(estadoD && estadoE){ // Seguir em Frente 
    analogWrite(pinMotorA1B,0);
    analogWrite(pinMotorB1B,0);
    digitalWrite(pinMotorA1A, HIGH);
    digitalWrite(pinMotorB1A, HIGH);
  } 
  if(!estadoD && !estadoE){ // Parar
    digitalWrite(pinMotorA1B,LOW);
    digitalWrite(pinMotorA1A,LOW);
    digitalWrite(pinMotorB1B,LOW);
    digitalWrite(pinMotorB1A,LOW);
  }
  if(!estadoD && estadoE){ // Virar para a Direita
    analogWrite(pinMotorA1B,0);
    digitalWrite(pinMotorA1A, HIGH);
    analogWrite(pinMotorB1B, velocidade);
    digitalWrite(pinMotorB1A, LOW);
    
  }

  if(estadoD && !estadoE){ // Virar para a Esquerda
    analogWrite(pinMotorB1B,0);
    digitalWrite(pinMotorB1A, HIGH);
    analogWrite(pinMotorA1B,velocidade);// girar no próprio eixo
    digitalWrite(pinMotorA1A, LOW);
    
  }
  delay(50);
  //Parar
     digitalWrite(pinMotorA1B,LOW);
   digitalWrite(pinMotorA1A,LOW);
   digitalWrite(pinMotorB1B,LOW);
   digitalWrite(pinMotorB1A,LOW);
   delay(500);// parar
     
}
