Monitor de Temperatura Corporal — IoT com ESP32 + MQTT
Universidade Presbiteriana Mackenzie
Projeto Final – Sistemas Embarcados / IoT
Sobre o Projeto

Este projeto apresenta um monitor de temperatura corporal baseado em IoT, utilizando um ESP32, o sensor LM35 (simulado), um atuador (LED vermelho) e comunicação com a internet via protocolo MQTT, conforme exigência acadêmica.

A solução realiza:

Medição contínua da temperatura corporal

Detecção automática de febre (> 37,5°C)

Acionamento de LED de alerta

Publicação das leituras em um broker MQTT

Recebimento de comandos MQTT para ligar/desligar o LED remotamente

Simulação completa no Wokwi, sem necessidade de hardware físico

Este projeto também atende aos objetivos da ODS 3 – Saúde e Bem-Estar, propondo uma solução acessível para monitoramento remoto de pacientes.

🛠️ Tecnologias Utilizadas

ESP32 DevKit V1 (simulado no Wokwi)

MQTT – Broker test.mosquitto.org

MQTT Explorer para visualização

Arduino IDE

Wokwi Simulator

Fritzing (diagrama do circuito)

Linguagem C/C++

🔧 Hardware Utilizado
✓ ESP32 DevKit V1
✓ Sensor LM35 (simulado no Wokwi)
✓ LED Vermelho + Resistor 220Ω
✓ Conexões por fios jumpers (simulados)
Diagrama do Circuito (Fritzing)

(Inserir imagem no GitHub)
/assets/diagrama_fritzing.png

Funcionamento do Sistema

O ESP32 realiza a leitura da temperatura (simulada).

Caso a temperatura seja maior que 37,5°C, o LED vermelho é acionado.

A leitura é publicada no tópico MQTT:

paciente/temperatura


O sistema também assina o tópico:

paciente/acao


O usuário pode enviar comandos:

"ON" → Liga o LED

"OFF" → Desliga o LED

O ESP32 responde com um acknowledge no tópico:

paciente/acao_ack

Tópicos MQTT Usados
Função	Tópico	Direção
Publicação da temperatura	paciente/temperatura	ESP32 → Broker
Comando para LED	paciente/acao	Cliente MQTT → ESP32
Retorno do comando	paciente/acao_ack	ESP32 → Cliente
Código Completo (Wokwi + MQTT + ESP32)

#include <WiFi.h>
#include <PubSubClient.h>

// WIFI WOKWI
const char* ssid = "Wokwi-GUEST";
const char* password = "";

// MQTT (Mosquitto)
const char* mqtt_server = "test.mosquitto.org";
const int mqtt_port = 1883;

// MQTT Topics
const char* temp_topic = "paciente/temperatura";
const char* cmd_topic  = "paciente/acao";
const char* ack_topic  = "paciente/acao_ack";

WiFiClient espClient;
PubSubClient client(espClient);

// LED externo no pino 13
int ledPin = 13;

void callback(char* topic, byte* payload, unsigned int length) {
  String msg = "";
  for (unsigned int i = 0; i < length; i++) {
    msg += (char)payload[i];
  }

  Serial.print("Comando recebido MQTT: ");
  Serial.println(msg);

  if (String(topic) == cmd_topic) {
    if (msg == "ON") {
      digitalWrite(ledPin, HIGH);
    } else if (msg == "OFF") {
      digitalWrite(ledPin, LOW);
    }
    client.publish(ack_topic, "ACK");
  }
}

void reconnect() {
  while (!client.connected()) {
    Serial.print("Conectando ao MQTT...");
    if (client.connect("ESP32_Wokwi")) {
      Serial.println("Conectado!");
      client.subscribe(cmd_topic);
    } else {
      Serial.print("Falhou rc=");
      Serial.print(client.state());
      delay(3000);
    }
  }
}

void setup() {
  Serial.begin(115200);
  pinMode(ledPin, OUTPUT);

  WiFi.begin(ssid, password);
  while (WiFi.status() != WL_CONNECTED) {
    delay(250);
    Serial.print(".");
  }
  Serial.println("WiFi conectado!");

  client.setServer(mqtt_server, mqtt_port);
  client.setCallback(callback);
}

void loop() {
  if (!client.connected()) reconnect();
  client.loop();

  float temp = random(350, 400) / 10.0;

  if (temp > 37.5) {
    digitalWrite(ledPin, HIGH);
  } else {
    digitalWrite(ledPin, LOW);
  }

  char msg[10];
  dtostrf(temp, 4, 2, msg);
  client.publish(temp_topic, msg);

  Serial.print("Temp publicada: ");
  Serial.println(msg);

  delay(3000);
}

Link para Simulação Wokwi
(coloque aqui o link do seu projeto Wokwi)
https://wokwi.com/projects/...

Resultados Obtidos

Comunicação funcional via MQTT

Gráfico de temperatura no MQTT Explorer

Resposta do LED em tempo real

Comandos remotos funcionando corretamente

(Incluir capturas do MQTT Explorer)
