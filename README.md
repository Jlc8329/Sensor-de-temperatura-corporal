# 🌡️ Monitoramento de Temperatura com ESP32, DHT22 e MQTT  
### Projeto para ODS 3 – Saúde e Bem-Estar

Este projeto demonstra um sistema de **monitoramento de temperatura corporal** usando **ESP32**, **sensor DHT22**, **MQTT**, e simulação completa no **Wokwi**.

Ele detecta automaticamente **febre**, aciona um **LED de alerta** e envia os dados para um **broker MQTT**, onde podem ser visualizados em tempo real via MQTT Explorer.

---

## 🎥 Demonstração em Vídeo  
▶️ **Assista na íntegra no YouTube:**  
https://youtu.be/0hQQ7PWKaec

---

# 🩺 Objetivo (ODS 3 – Saúde e Bem-estar)

O projeto busca auxiliar ambientes hospitalares e clínicas através de um sistema simples, barato e eficiente para:

- Monitorar temperatura de pacientes à distância  
- Detectar febre automaticamente  
- Enviar alertas e dados para a nuvem  
- Permitir visualização em dashboards MQTT  

---

# ⚙️ Tecnologias Utilizadas

- **ESP32**  
- **Sensor DHT22 (Temperatura e Umidade)**  
- **MQTT (test.mosquitto.org)**  
- **MQTT Explorer (visualização gráfica)**  
- **Wokwi (simulação online)**  
- **Arduino C++**

---

# 🔌 Circuito – Diagrama (Wokwi)

Imagem do circuito utilizado:

![Circuito ESP32 + DHT22 + LED]

<img width="404" height="372" alt="image" src="https://github.com/user-attachments/assets/c06f318b-bc76-4ffe-bb56-46296d9b6b80" />


---

# 🖥️ Simulação no Wokwi

O Wokwi permite simular todo o projeto sem hardware físico.  
No DHT22, a temperatura pode ser ajustada manualmente para simular febre.

Exemplo da simulação em execução:

![Simulação Wokwi]

<img width="812" height="923" alt="image" src="https://github.com/user-attachments/assets/6f677816-b1c5-4e7e-971f-cd47f1e4bbd4" />


---

# 📡 Publicação MQTT em Tempo Real

Os dados enviados ao broker podem ser visualizados no MQTT Explorer:

![MQTT Explorer]
<img width="1280" height="780" alt="image" src="https://github.com/user-attachments/assets/dfd0904c-c51c-4067-9aa7-aa0f7feb224b" />


---

# 📂 Arquivos do Projeto

Este repositório contém:

README.md
sketch.ino
diagram.json


---

# 🧠 Lógica de Funcionamento

1. O ESP32 conecta ao WiFi  
2. Lê a temperatura do DHT22  
3. Publica o valor no tópico MQTT:  

gustavo10290057/paciente/temperatura

4. Se a temperatura > 37.5°C → LED acende + mensagem de **FEBRE DETECTADA**  
5. MQTT Explorer exibe valores e gráficos em tempo real  

---

# ▶️ Como Executar no Wokwi

1. Abra o Wokwi: https://wokwi.com  
2. Cole o código do arquivo `sketch.ino`  
3. Substitua o `diagram.json` pelo deste repositório  
4. Clique em **Play**  
5. Ajuste a temperatura no sensor DHT22 para simular febre

---

# 👨‍💻 Autor

Projeto desenvolvido por **Gustavo Henrique Cardoso**  
Estudante da Universidade Presbiteriana Mackenzie.

