# 🌡️ Monitor de Temperatura Corporal com ESP32, LM35 e MQTT  
### Projeto baseado em IoT — Alinhado à ODS 3 (Saúde e Bem-Estar)

Este projeto apresenta um sistema IoT para monitoramento de temperatura corporal utilizando o sensor **LM35** (sensor oficial do projeto), o microcontrolador **ESP32**, e o protocolo **MQTT** para comunicação em rede.  
O objetivo é detectar febre de forma automática e enviar os dados em tempo real para um broker MQTT, permitindo acompanhamento remoto.

---

## ⚠️ Aviso Importante sobre a Simulação 

O sensor oficial do projeto é o **LM35**, utilizado para medir temperatura corporal real por contato com a pele.  
**Porém, o ambiente Wokwi NÃO possui o LM35**, e por isso:

> **O sensor DHT22 foi utilizado APENAS para a simulação**, com a finalidade de demonstrar o funcionamento do protótipo, leitura dos dados, comunicação MQTT e acionamento do atuador.

Toda a documentação, análise técnica, justificativa e funcionamento descritos no artigo são baseados no **LM35**, conforme solicitado pelo professor.

---

# 📡 Funcionalidades

- Leitura da temperatura corporal usando **LM35 (real)** ou **DHT22 (simulação)**  
- Identificação automática de febre (> 37.5 ºC)  
- Envio da temperatura ao broker MQTT  
- Acionamento de LED vermelho como alerta  
- Comunicação contínua via Wi-Fi  
- Publicação MQTT a cada 3 segundos  

---

# 🧰 Componentes Utilizados

### ✔ No protótipo real (documentação oficial)
- ESP32 DevKit V1  
- Sensor LM35 (analógico)  
- LED vermelho  
- Resistor 220 Ω  
- Protocolo MQTT (Mosquitto)


## 🎥 Demonstração em Vídeo  
▶️ **Assista na íntegra no YouTube:**  
[https://youtu.be/0hQQ7PWKaec](https://youtu.be/WZPJgj48b5E)

# 🔌 Circuito – Diagrama (Wokwi)
Imagem do circuito utilizado:

![Circuito ESP32 + DHT22 + LED]

<img width="404" height="372" alt="image" src="https://github.com/user-attachments/assets/021468ff-680a-4fe9-a211-acc04313327f" />

### ✔ Na simulação (Wokwi)
- ESP32  
- Sensor DHT22 (apenas para simular o LM35)  
- LED + resistor  
- Conexões virtuais equivalentes  

---

# 🔌 Ligações do LM35 (Protótipo Real)

| LM35 | ESP32 |
|------|-------|
| VCC  | 3.3V  |
| OUT  | GPIO34 (ADC) |
| GND  | GND |

---

# 🛠️ Código Fonte (Importante)

O código implementa:

- Leitura analógica do LM35  
- Leitura do DHT22 somente quando detectar que o código está rodando no Wokwi  
- Lógica automática para identificar qual sensor está ativo  
- Publicação MQTT  
- Acionamento do LED  

O arquivo `sketch.ino` já vem preparado com:

```cpp
// LM35 = sensor oficial
// DHT22 = apenas simulação no Wokwi
