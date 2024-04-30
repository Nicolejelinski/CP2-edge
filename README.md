![logo png (2)](https://github.com/Nicolejelinski/CP2-edge/assets/143125546/baf46fa5-34cf-469c-b393-55838eb5bacb) 



# Sensor de Luminosidade, Umidade e Temperatura: Monitoramento Essencial para Vinícolas
Este projeto foi concebido para a Vinheria Agnello, visando monitorar as condições de armazenamento dos vinhos. Nossa meta é assegurar que a temperatura, umidade e luminosidade de determinado ambiente estejam ideais para preservar a qualidade dos produtos. Em caso de qualquer discrepância, o proprietário será prontamente notificado.

## Visão Geral
O Sensor de Monitoramento de Condições de Armazenamento é uma solução integrada desenvolvida para garantir a excelência no armazenamento dos vinhos produzidos pela Vinheria Agnello. Por meio de uma abordagem contínua e precisa, o sensor monitora a temperatura, umidade e luminosidade do ambiente de armazenamento, elementos críticos que influenciam diretamente na integridade e sabor dos vinhos.

## Funcionalidades Principais

- `Funcionalidade 1`: Monitoramento de umidade, luminosidade e temperatura
- `Funcionalidade 2`: Indicação Visual com LEDs
- `Funcionalidade 3`: Alerta sonoro acionado caso a luminosidade esteja fora do padrão necessário.
- `Funcionalidade 5`: Valores registrados e calculados a cada 10 ciclos para possibilitar a detecção de discrepâncias
- `Funcionalidade 4`: Mensagem no LCD indicando caso algum dos parâmetros esteja errado.



## Limites Estipulados
Os limites estipulados podem variar de acordo com as especificidades do ambiente de armazenamento de vinhos. No código fornecido, os limites são definidos, mas podem ser ajustados conforme necessário.

## Display LCD e Mensagens

O display LCD é utilizado neste projeto para fornecer informações visuais sobre as condições monitoradas e exibir mensagens de alerta. Aqui está como as informações são apresentadas no display:

- **Temperatura:** A temperatura atual é exibida no formato "T: XX°C", onde XX é o valor da temperatura em graus Celsius.

- **Umidade:** A umidade relativa do ar é exibida no formato "H: XX%", onde XX é o valor da umidade em percentagem.

- **Luminosidade:** A intensidade da luz ambiente é exibida no formato "L: XX%", onde XX é o valor da luminosidade em percentagem.

Além disso, o display também pode mostrar mensagens de alerta em caso de condições fora do esperado, como temperaturas extremas, umidade inadequada ou luminosidade excessiva. Para garantir uma boa legibilidade das mensagens, o display é atualizado a cada ciclo de leitura dos sensores, proporcionando uma monitoração contínua das condições ambientais.

*exemplo*
 ![mensagem exemplo](https://github.com/Nicolejelinski/CP2-edge/assets/143125546/b35036c4-d496-467d-8f5d-c26d2f78af0c) 


## Componentes necessários
| Componente    | Quantidade    |
| ------------- | ------------- |
| Arduino Uno R3  | 1 |
| Protoboard  | 1 
| Led verde  | 1  |
| Led vermelho | 1 |
| Led amarelo  | 1  |
| Buzzer  | 1  |
| LDR  | 1  |
| Resistor 220Ω | 3 |
| DHT11 | 1  |
| Potenciômetro  | 1 |
| Display LCD | 1 |

## Conexão dos Componentes
Conecte os componentes conforme o esquema de conexão fornecido no código-fonte.

## Utilização
Após a configuração e conexão dos componentes, abra o arquivo do código-fonte em um ambiente de desenvolvimento integrado para Arduino (como Arduino Uno), inicie o monitoramento executando o código no Arduino.

## Referências

- [Documentação oficial do Arduino](https://www.arduino.cc/)
- [Tutorial sobre DHT11 no Adafruit](https://learn.adafruit.com/dht)
- [Tutorial sobre o uso de LCD com Arduino no Arduino Project Hub](https://create.arduino.cc/projecthub/NickNiebles/how-to-connect-an-lcd-display-to-an-arduino-in-6-seconds-62eb2e)


## Autores
Projeto desenvolvido para a matéria de Edge Computing do Professor Fabio Cabrini, por: 
Felipe Genistretti Rodrigues;
Nicolle Pellegrino Jelinski;
Nicolas Aquino Borges;
Renan Simões Gonçalves;
Vitor Rivas Cardoso.

# Código
```
#include <DHT.h> // Inclui a biblioteca DHT para comunicação com o sensor de umidade e temperatura
#include <LiquidCrystal.h> // Inclui a biblioteca LiquidCrystal para comunicação com o display LCD

#define DHTPIN A0 // Define o pino ao qual o sensor DHT está conectado
#define DHTTYPE DHT11 // Define o tipo de sensor DHT

DHT dht(DHTPIN, DHTTYPE); // Cria uma instância do objeto DHT

// Define os pinos para o display LCD
const int rs = 7;
const int en = 6;
const int d4 = 12;
const int d5 = 10;
const int d6 = 9;
const int d7 = 8;

// Define os pinos para os LEDs e o buzzer
const int RED = 2;
const int YELLOW = 3;
const int GREEN = 4;
const int BUZZER = 11; // Mudei o pino para evitar conflito
const int Sensor = A1; // Mudei o pino para evitar conflito

LiquidCrystal lcd(rs, en, d4, d5, d6, d7); // Cria uma instância do objeto LiquidCrystal

// Define arrays de bytes para criar caracteres personalizados no LCD
byte name01[] = { B00000, B00000, B00000, B00000, B10000, B11000, B11100, B11110 };
byte name02[] = { B00000, B00000, B00000, B00000, B00010, B00110, B01110, B11110 };
byte name03[] = { B11100, B11000, B10000, B00000, B00000, B00000, B00000, B00000 };
byte name04[] = { B01110, B00110, B00010, B00000, B00000, B00000, B00000, B00000 };

byte name05[] = { B00000, B00000, B00000, B00000, B10000, B11000, B11100, B11110 };
byte name06[] = { B00000, B00000, B00000, B00000, B00001, B00011, B00111, B01111 };
byte name07[] = { B11100, B11000, B10000, B00000, B00000, B00000, B00000, B00000 };
byte name08[] = { B00111, B00011, B00001, B00000, B00000, B00000, B00000, B00000 };

byte name0x3[] = { B00000, B00000, B00000, B00000, B10000, B11000, B11100, B11110 };
byte name0x12[] = { B00000, B00000, B00000, B00000, B00001, B00011, B00111, B01111 };
byte name1x3[] = { B11100, B11000, B10000, B00000, B00000, B00000, B00000, B00000 };
byte name1x12[] = { B00111, B00011, B00001, B00000, B00000, B00000, B00000, B00000 };

void setup() {
  Serial.begin(9600); // Inicializa a comunicação serial com uma taxa de transmissão de 9600 bps

  dht.begin(); // Inicializa o sensor DHT

  lcd.begin(16, 2); // Inicializa o display LCD com 16 colunas e 2 linhas
  lcd.print("      WII9"); // Imprime uma mensagem inicial no LCD
  delay(2000); // Aguarda 2 segundos

  // Cria caracteres personalizados no LCD
  lcd.createChar(0, name01);
  lcd.setCursor(1, 0);
  lcd.write(byte(0));

  // (Os demais caracteres personalizados são criados da mesma maneira)

  delay(1200); // Aguarda 1,2 segundos

  // Configura os pinos como saídas ou entradas conforme necessário
  pinMode(RED, OUTPUT);
  pinMode(YELLOW, OUTPUT);
  pinMode(GREEN, OUTPUT);
  pinMode(BUZZER, OUTPUT);
  pinMode(Sensor, INPUT);
}

void loop() {
  int h_total = 0;  // Variável para armazenar a soma das leituras de umidade
  int t_total = 0;  // Variável para armazenar a soma das leituras de temperatura
  int i_total = 0;  // Variável para armazenar a soma das leituras de luminosidade

  int ciclo = 0; // Variável de controle do loop

  for (ciclo = 0; ciclo < 10; ciclo++) { // Realiza 10 ciclos de medição
    int h = dht.readHumidity(); // Lê a umidade do sensor DHT
    int t = dht.readTemperature(); // Lê a temperatura do sensor DHT
    int f = dht.readTemperature(true); // Lê a temperatura em Fahrenheit

    int sensorValue = analogRead(Sensor); // Lê o valor do sensor de luminosidade
    int i = map(sensorValue, 54, 974, 0, 100); // Mapeia o valor do sensor para uma faixa de 0 a 100

    h_total += h;
    t_total += t;
    i_total += i;

    // Exibição dos dados no LCD
    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print("T:");
    lcd.print(t);
    lcd.print("C H:");
    lcd.print(h);
    lcd.print("% L:");
    lcd.print(i);
    lcd.print("%");
    delay(1500);

    // Controle dos LEDs e do buzzer
    digitalWrite(GREEN, LOW);
    digitalWrite(YELLOW, LOW);
    digitalWrite(RED, LOW);
    digitalWrite(BUZZER, LOW);

    if (i < -3) {
      digitalWrite(GREEN, HIGH);
    } else if (i >= -3 && i <= -1) {
      digitalWrite(YELLOW, HIGH);

      // Exibição dos dados no LCD
      lcd.clear();
      lcd.setCursor(0, 0);
      lcd.print("Ambiente a meia");
      lcd.setCursor(0, 1);
      lcd.print("luz");
      delay(2000);

    } else {
      digitalWrite(RED, HIGH);
      digitalWrite(BUZZER, HIGH);

      // Exibição dos dados no LCD
      lcd.clear();
      lcd.setCursor(0, 0);
      lcd.print("Ambiente muito");
      lcd.setCursor(0, 1);
      lcd.print("claro");
      delay(2000);
    }

    if (t < 10) {
      // Exibição dos dados no LCD
      lcd.clear();
      lcd.setCursor(0, 0);
      lcd.print("Temperatura");
      lcd.setCursor(0, 1);
      lcd.print("baixa");
      delay(2000);
    }
    else if (t > 15) {
      // Exibição dos dados no LCD
      lcd.clear();
      lcd.setCursor(0, 0);
      lcd.print("Temperatura");
      lcd.setCursor(0, 1);
      lcd.print("alta");
      delay(2000);
    }

    if (h <= 50) {
      // Exibição dos dados no LCD
      lcd.clear();
      lcd.setCursor(0, 0);
      lcd.print("Umidade");
      lcd.setCursor(0, 1);
      lcd.print("baixa");
      delay(2000);
    }
    else if (h > 50 && h < 70) {
      // Exibição dos dados no LCD
      lcd.clear();
      lcd.setCursor(0, 0);
      lcd.print("Umidade OK");
      delay(2000);
    }
    else if (h >= 70) {
      // Exibição dos dados no LCD
      lcd.clear();
      lcd.setCursor(0, 0);
      lcd.print("Umidade");
      lcd.setCursor(0, 1);
      lcd.print("alta");
      delay(2000);
    }

    // Exibição dos dados do sensor DHT11 no monitor serial
    if (isnan(h) || isnan(t) || isnan(f)) {
      Serial.println(F("Failed to read from DHT sensor!"));
    }

    // Aguarda 2 segundos antes de repetir o loop
    delay(2000);
  }

  // Calcula a média dos valores
  int h_media = h_total / 10;
  int t_media = t_total / 10;
  int i_media = i_total / 10;

  // Exibe os valores médios no monitor serial
  Serial.print("Média de Temperatura: ");
  Serial.println(t_media);
  Serial.print("Média de Umidade: ");
  Serial.println(h_media);
  Serial.print("Média de Luz: ");
  Serial.println(i_media);

  // Exibição dos dados no LCD
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Media de 10 ciclos:");
  lcd.setCursor(0, 1);
  lcd.print("T:");
  lcd.print(t_media);
  lcd.print("C H:");
  lcd.print(h_media);
  lcd.print("% L:");
  lcd.print(i_media);
  lcd.println("%");
  delay(500);

  // Reinicia os totais para a próxima medição
  h_total = 0;
  t_total = 0;
  i_total = 0;

  // Aguarda 2 segundos antes de repetir o loop
  delay(2000);
}
```
