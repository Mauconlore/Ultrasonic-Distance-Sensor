Este código controla um servo motor baseado na distância medida por um sensor ultrassônico. Vamos analisar cada parte:

Componentes Principais
Servo motor - Conectado ao pino 9

Sensor ultrassônico - Trigger no pino 10, Echo no pino 11

Funcionamento
Setup (Configuração Inicial)
cpp
Servo servo_9;

void setup()
{
  servo_9.attach(9, 500, 2500);
}
Inicializa o servo motor no pino 9, configurando os pulsos mínimos (500μs) e máximos (2500μs) para controle.

Loop Principal
cpp
void loop()
{
  butaostatus = 0.01723 * readUltrasonicDistance(10, 11);
  if (butaostatus < 60) {
    servo_9.write(90);
    delay(3000); // Wait for 3000 millisecond(s)
  }
  servo_9.write(0);
}
Medição de Distância:

Chama a função readUltrasonicDistance() para medir a distância

Multiplica por 0.01723 para converter o tempo de viagem do som em centímetros

Armazena o resultado em butaostatus

Lógica de Controle:

Se um objeto estiver a menos de 60cm (butaostatus < 60):

Move o servo para a posição 90 graus

Mantém por 3 segundos (3000ms)

Depois (ou se nenhum objeto estiver próximo), move o servo de volta para 0 graus

Função do Sensor Ultrassônico
cpp
long readUltrasonicDistance(int triggerPin, int echoPin)
{
  // Configuração do pulso de trigger
  digitalWrite(triggerPin, LOW);
  delayMicroseconds(2);
  digitalWrite(triggerPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(triggerPin, LOW);
  
  // Mede o tempo de eco
  return pulseIn(echoPin, HIGH);
}
Envia um pulso ultrassônico de 10μs

Mede o tempo que leva para o eco retornar

Retorna o tempo em microssegundos

Resumo do Comportamento
O sistema funciona como um "abre e fecha" automático baseado em proximidade:

Quando um objeto é detectado a menos de 60cm, o servo move para 90° (aberto)

Permanece aberto por 3 segundos

Retorna para 0° (fechado)

Repete continuamente esse processo

Típico uso poderia ser em uma porta automática, dispensador ou qualquer aplicação que precise responder à proximidade de objetos.

# Ultrasonic-Distance-Sensor
