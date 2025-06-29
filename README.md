# 🌡️💧 Monitoramento de Temperatura e Umidade com ESP32 + DHT22 + ThingSpeak

Este projeto simula um sistema de IoT utilizando ESP32 e sensor DHT22 para leitura de temperatura e umidade. Os dados são enviados para a nuvem via ThingSpeak e exibidos em tempo real em gráficos públicos. O circuito foi desenvolvido e simulado no Wokwi.

## 📘 Contextualização do Problema

Ambientes como residências, estufas, data centers ou escritórios precisam de monitoramento constante de temperatura e umidade. Variações fora dos padrões podem causar desconforto, prejuízo a equipamentos ou danos à produção. Este projeto busca resolver esse problema por meio da automação e monitoramento remoto, simulando um sistema realista com baixo custo e alta aplicabilidade, utilizando ESP32, sensor DHT22 e ThingSpeak.

## 🧰 Tecnologias Utilizadas

- ESP32 (Wokwi)
- Sensor DHT22
- Bibliotecas: `DHTesp.h`, `ThingSpeak.h`, `WiFi.h`
- Plataforma de simulação: [Wokwi] (https://wokwi.com/projects/435126008849221633)
- Plataforma de nuvem: [ThingSpeak](https://thingspeak.com/channels/1881348)
- IDE Arduino

## 🔌 Diagrama do Circuito (Wokwi)
![Diagrama do circuito](assets/wokwi_circuito.png)

## 🖥️ Execução no Serial Monitor
![Serial Monitor](assets/serial_monitor.png)

## 📊 Visualização dos Dados no ThingSpeak
![Gráficos ThingSpeak](assets/thingspeak_graficos.png)

## ⚙️ Funcionamento

1. O ESP32 coleta dados do sensor DHT22 (temperatura e umidade).
2. A cada 10 segundos, os dados são enviados para a nuvem via ThingSpeak.
3. Os dados podem ser visualizados por qualquer pessoa em tempo real por meio de gráficos públicos.
4. Todo o sistema roda de forma simulada no Wokwi, o que elimina a necessidade de hardware físico.


## 🧠 Explicação Detalhada do Código

Abaixo está um resumo das principais partes do código utilizado no projeto, com explicações linha por linha:

### Bibliotecas Utilizadas

```cpp
#include <WiFi.h>           // Permite conectar o ESP32 ao Wi-Fi
#include "DHTesp.h"         // Controla o sensor DHT22 (temperatura e umidade)
#include "ThingSpeak.h"     // Responsável pelo envio dos dados para a nuvem (ThingSpeak)
```

### Variáveis de Configuração

```cpp
const int DHT_PIN = 15;
const char* WIFI_NAME = "Wokwi-GUEST";
const char* WIFI_PASSWORD = "";
const int myChannelNumber = 1881348;
const char* myApiKey = "0VT00L9VQJYCLBLI";
```

- Define o pino de leitura do sensor, as credenciais Wi-Fi e o canal da API do ThingSpeak.

### Inicialização no `setup()`

```cpp
Serial.begin(115200);
dhtSensor.setup(DHT_PIN, DHTesp::DHT22);
WiFi.begin(WIFI_NAME, WIFI_PASSWORD);
```

- Inicia a comunicação serial e conecta ao Wi-Fi.
- Aguarda a conexão para só depois continuar.
- Exibe o IP local (simulado no Wokwi).
- Inicializa a comunicação com a API do ThingSpeak.

### Loop Principal `loop()`

```cpp
TempAndHumidity data = dhtSensor.getTempAndHumidity();
ThingSpeak.setField(1, data.temperature);
ThingSpeak.setField(2, data.humidity);
```

- Lê os dados do sensor DHT22.
- Atribui os valores aos campos 1 (temperatura) e 2 (umidade) do canal ThingSpeak.

```cpp
int x = ThingSpeak.writeFields(myChannelNumber, myApiKey);
```

- Envia os dados para o canal na nuvem.
- Verifica se o envio foi bem-sucedido (resposta HTTP 200).

```cpp
Serial.println("Temp: ...");
Serial.println("Humidity: ...");
Serial.println("---");
```

- Imprime os dados no monitor serial para visualização local.

```cpp
delay(10000);
```

- Aguarda 10 segundos antes de repetir o processo.

---

## 🔗 Links Importantes

- [🔌 Simulação no Wokwi](https://wokwi.com/projects/435126008849221633)
- [📊 Canal público no ThingSpeak](https://thingspeak.com/channels/1881348)

## 🛠️ Instruções para Replicar

1. Acesse o link do Wokwi acima e clique em "Start Simulation".
2. Acompanhe os dados sendo impressos no Serial Monitor.
3. Acesse o canal do ThingSpeak e veja os gráficos atualizados.
4. Caso deseje usar seu próprio canal, altere as variáveis `myChannelNumber` e `myApiKey` no código.

## 🎥 Vídeo de Apresentação


---

Projeto desenvolvido para a disciplina **Introdução à Automação de Ambientes e Processos**.
**Integrantes:**<br>
Alice da Silva Marinho Gomes - CB3025772 <br>
Matheus Leandro Terra Luciano - CB3024881 <br>
Milena Costa de Andrade - CB3024881 <br>
Vinicius do Nascimento Ayres - CB3025675<br>
