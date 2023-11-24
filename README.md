
Descrição do Problema de Saúde:

O problema de saúde abordado neste projeto está relacionado ao risco de doenças cardiovasculares devido à elevação da temperatura corporal. A alta temperatura do corpo pode indicar febres ou condições médicas que podem levar a complicações cardíacas. Manter um controle precoce da temperatura pode ser crucial para prevenir problemas de saúde graves, especialmente em ambientes onde as temperaturas elevadas podem representar um risco significativo.

Visão Geral da Solução Proposta:

A solução proposta é um "Sistema de Alerta Precoce para Prevenção de Doenças". O sistema utiliza um sensor de temperatura (no caso, o DHT22) conectado a um ESP32 para monitorar a temperatura corporal. Dois LEDs são empregados para fornecer feedback visual em tempo real. Um LED branco indica que a temperatura está dentro da faixa normal, enquanto um LED vermelho alerta quando a temperatura ultrapassa um limiar estabelecido.

Instruções para Configurar e Executar a Aplicação:

Componentes Necessários:

ESP32 (ou equivalente).
Sensor de temperatura DHT22.
LEDs (um branco e um vermelho).
Resistor de pull-up (aproximadamente 4.7k ohms).
Conexão à fonte de alimentação (USB para ESP32).
Montagem Física:

Conecte o DHT22 ao ESP32, utilizando os pinos corretos para VCC, GND e DATA.
Adicione um resistor de pull-up entre o pino DATA do DHT22 e o pino VCC.
Conecte os LEDs (branco e vermelho) aos pinos do ESP32 conforme especificado no código.
Configuração no Wokwi:

Utilize o simulador Wokwi para montar virtualmente o circuito, adicionando os componentes necessários.
Conecte os componentes virtualmente, seguindo as instruções de montagem física.
Código no Wokwi:

Copie o código fornecido para monitorar a temperatura usando o DHT22 e controlar os LEDs.
Ajuste o pino DHT_PIN no código se a conexão física for diferente.
Execução e Observação:

Inicie a simulação no Wokwi.
Observe o comportamento dos LEDs em resposta à temperatura simulada.
O LED branco deve permanecer aceso quando a temperatura está normal, e o LED vermelho deve acender quando a temperatura ultrapassar o limiar definido.
Este sistema oferece uma maneira eficaz de monitorar a temperatura corporal e alertar sobre possíveis problemas de saúde, permitindo a intervenção precoce para evitar complicações cardiovasculares.

link para o projeto no wowki - > https://wokwi.com/projects/382236359867078657

*CÓDIGO UTILIZADO LOGO ABAIXO*

#include <DHT.h>

#define DHT_PIN 16      // Pino ao qual o sensor DHT22 está conectado (pode ser alterado)
#define LED_PIN_RED 2    // Pino do LED vermelho
#define LED_PIN_WHITE 4  // Pino do LED branco
#define TEMPERATURE_THRESHOLD 37.5  // Limiar de temperatura para acender o LED vermelho

DHT dht(DHT_PIN, DHT22);

void setup() {
  Serial.begin(115200);
  pinMode(LED_PIN_RED, OUTPUT);
  pinMode(LED_PIN_WHITE, OUTPUT);

  dht.begin();
}

void loop() {
  float temperatura = dht.readTemperature();

  Serial.print("Temperatura Real: ");
  Serial.print(temperatura);
  Serial.println(" °C");

  // Atualiza a cor do LED com base na temperatura lida
  if (temperatura > TEMPERATURE_THRESHOLD) {
    // Temperatura alta - LED vermelho
    digitalWrite(LED_PIN_RED, HIGH);
    digitalWrite(LED_PIN_WHITE, LOW);
  } else {
    // Temperatura normal - LED branco
    digitalWrite(LED_PIN_RED, LOW);
    digitalWrite(LED_PIN_WHITE, HIGH);
  }

  delay(2000);  // Aguarda 2 segundos entre leituras
}






