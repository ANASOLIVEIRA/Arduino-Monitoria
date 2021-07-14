# Arduino-Monitoria
1)	Grave no Esp 8266 o programa em C++ para funcionar o programa Blynk com seu celular, em seguida ligue um led na porta GPIO 3 para teste. (descreva os passos necessários para a execução desta questão)

Descrição aplicativo Blink: É uma plataforma simples para a integração do uso de placas embarcadas, no caso a placa ESP8266, com o celular. Pode ser utilizado conexão via Wi-Fi ou Bluetooth.

Passo 1) Endereçar a placa ESP8266 na IDE do Arduino.

![image](https://user-images.githubusercontent.com/61547619/125547895-bf5d2efb-6bf7-47d0-9efb-afc7207b9069.png)

Passo 2) Conectar a placa ao celular, verificar se o celular enxerga a placa. Para questões de segurança o aplicativo Blynk gera um token de segurança. e esse token é colocado no código para haver a conectividade, esse token é enviado por email.

Declaração do device

![image](https://user-images.githubusercontent.com/61547619/125547847-fcc98ae5-2393-4f60-8cd2-746237dad658.png)

Definição de tipo de conexão

![image](https://user-images.githubusercontent.com/61547619/125547957-d56605e3-e796-4ba4-883d-e49feff3d808.png)

Email com o código de segurança:

![image](https://user-images.githubusercontent.com/61547619/125547869-ecf10b25-6043-41e8-b074-eaf111635682.png)

Passo 3) Criar ambiente no aplicativo. Como só é necessário ligar um led conectado a uma porta. A interface é bem simples.

Definição do pino conectado ao botão

![image](https://user-images.githubusercontent.com/61547619/125550496-7b6ea320-09fa-4f68-8b9b-70ac7b911300.png)

Interface

![image](https://user-images.githubusercontent.com/61547619/125557127-da67ba0d-8c2f-4bea-8449-5dde1cc0a02d.png)

Passo 4) Digitar o código na IDE Arduíno

```C++

#include <ESP8266_Lib.h> //Biblioteca ESP
#include <BlynkSimpleShieldEsp8266.h>
 
char auth[] = "c64df54088974b678574056d6eb9d7ff"; //Token enviado por email, passo 2
 
char ssid[] = "####"; //Nome da rede Wi-Fi
char pass[] = "####"; //Senha da rede Wi-Fi
 
ESP8266 wifi(&Serial);
 
void setup(){
  Serial.begin(9600); //Inicializa o serial begin, nomitor
  delay(1000); //Espera de 1 segundo, convertido em milisegundos
  Blynk.begin(auth, wifi, ssid, pass); //Inicia comunicação
}
 
void loop(){
  Blynk.run(); //INICIALIZA O BLYNK
}
#include <ESP8266_Lib.h> //Biblioteca ESP
#include <BlynkSimpleShieldEsp8266.h>
 
char auth[] = "c64df54088974b678574056d6eb9d7ff"; //Token enviado por email, passo 2
 
char ssid[] = "INTELBRAS"; //Nome da rede Wi-Fi
char pass[] = "647543ana"; //Senha da rede Wi-Fi
 
ESP8266 wifi(&Serial);
 
void setup(){
  Serial.begin(9600); //Inicializa o serial begin, nomitor
  delay(1000); //Espera de 1 segundo, convertido em milisegundos
  Blynk.begin(auth, wifi, ssid, pass); //Inicia comunicação
}
 
void loop(){
  Blynk.run(); //INICIALIZA O BLYNK
}

```
Passo 5) Testar projeto

2) Faça as ligações para conectar a placa Arduino com o Esp8266, 2 motores serão  acionados pelo Arduino que recebe o comando do Esp por meio de sua GPIO 0 e GPIO 2, O ESP 8266 é  ativado pelo Blynk com botões que acionam um( robô que ainda tem um ultra som mas não considera na programação) para frente direita e esquerda e parado . Faça a programação do Arduino e ESP8266 01 e do App Blink.

![image](https://user-images.githubusercontent.com/61547619/125557295-2b73ff2a-0bc9-49b6-9b20-67197b03b270.png)

Montagem do esquema

![image](https://user-images.githubusercontent.com/61547619/125557873-cd4950f8-5cf5-47d1-89ee-82788f05f35b.png)

Programação

```C++
Programa
#include <ESP8266_Lib.h> //Biblioteca ESP
#include <BlynkSimpleShieldEsp8266.h>
#include <AFMotor.h>

AF_DCMotor M1(1); //Declaração de qual a posição do motor no shield
AF_DCMotor M2(2); //Declaração de qual a posição do motor no shield

char auth[] = "c64df54088974b678574056d6eb9d7ff"; //Token enviado por email, passo 2
 
char ssid[] = "#####"; //Nome da rede Wi-Fi
char pass[] = "#####"; //Senha da rede Wi-Fi

#define botao1 0
#define botao2 2
int i=0;
int j=0;
void setup() 
{
  Serial.begin(9600); //Inicializa o serial begin, nomitor
  delay(1000); //Espera de 1 segundo, convertido em milisegundos
  Blynk.begin(auth, wifi, ssid, pass); //Inicia comunicação
  
  M1.setSpeed(0);//Controle do motor em PWM - Motor inicia parado
  M2.setSpeed(0);//Controle do motor em PWM - Motor inicia parado
  pinMode(botao1, INPUT);
  pinMode(botao2, INPUT);
}

void loop() 
{
  Blynk.run();
  botao1=digitalRead(botao);
  botao2=digitalRead(botao);
  
  if(botao1 == HIGH)
  {
    M1.setSpeed(0);
    M1.run(RELEASE);//Motor stop
    delay(500);
    M1.setSpeed(255);//Motor rotação máxima
    M1.run(FORWARD);//Set sentido horario
    i++;
    if(i == 2)
    {
      M1.setSpeed(0);
      M1.run(RELEASE);//Motor stop
      delay(500);
      M1.setSpeed(255);//Motor rotação máxima
      M1.run(BACKWARD);//Set sentido anti-horario
      i++;      
    }
        else if(i == 3)
    {
      M1.setSpeed(0);
      M1.run(RELEASE);//Motor stop     
    }    
  }

  if(botao2 == HIGH)
  {
    M1.setSpeed(0);
    M1.run(RELEASE);//Motor stop
    delay(500);
    M1.setSpeed(255);//Motor rotação máxima
    M1.run(FORWARD);//Set sentido horario
    j++;
    if(j == 2)
    {
      M1.setSpeed(0);
      M1.run(RELEASE);//Motor stop
      delay(500);
      M1.setSpeed(255);//Motor rotação máxima
      M1.run(BACKWARD);//Set sentido anti-horario
      j++;      
    }
        else if(j == 3)
    {
      M1.setSpeed(0);
      M1.run(RELEASE);//Motor stop     
    }    
  }
}

```



Aplicativo Blink

![image](https://user-images.githubusercontent.com/61547619/125557956-3f4e4999-ff45-429f-b759-4d0adeff297f.png)

3) Descreva o processo necessário para resetar e entrar no modo de gravação no microcontrolador esp8266 01.

Temos diversos métodos para a gravação do ESP8266-01.
Itens necessários:
1) 1- Chip FT232R
2) 2 botões push
3) 3 resistores 10k

Passo 1) Selecionar placa Generic ESP8266 Module

![image](https://user-images.githubusercontent.com/61547619/125558001-5e42fbd6-863c-4b0d-9cc6-c70443f1b25d.png)

Passo 2) Carregar o programa blink no exemplo da biblioteca ESP8266

Com esse programa iremos piscar o led azul do módulo ESP8266-01, na porta GPIO1 (TX)

![image](https://user-images.githubusercontent.com/61547619/125558265-6eb63d6a-208d-4039-9855-bcc9a66f6bed.png)

Passo 3) Estabelecer comunicação USB-Serial (Chip FT232)
ATENTAR PARA A ALIMENTAÇÃO DE 3,3V DO CHIP

Passo 4) Montagem do circuito

![image](https://user-images.githubusercontent.com/61547619/125558344-77358403-013f-4f43-9a18-12fa27bf822b.png)

Passo 5) Upload
Pressiona o botão que está na GPIO0 e um pulso no botão reset do ESP-01. Quando o led azul do ESP-01 indica que ele está em modo gravação. Aí podemos soltar o botão do GPIO0.
Depois compila o programa e envia para a placa.
Para indicar que o processo teve sucesso o led azul ficará piscando.

![image](https://user-images.githubusercontent.com/61547619/125558527-2016d8c9-1db0-4633-a255-b7e07db420bb.png)

4) Descreva o processo necessário para configurar a IDE Arduino para utilizar a placa Esp8266.

Para utilizar a placa ESP no ambiente do Arduino é necessário colocar o pacote de placas ESP9266. 
Primeiro ir em Preferências e adicionar o link para conseguir adicionar placas por meio do gerenciador de placas (URLs Adicionais para Gerenciadores de Placas). 

Link de placas utilizado: https://arduino.esp8266.com/stable/package_esp8266com_index.json
Após incluir o link clicar em OK.

![image](https://user-images.githubusercontent.com/61547619/125558753-87428d96-0162-40ca-8d52-d5bb113f3c61.png)

![image](https://user-images.githubusercontent.com/61547619/125558793-b778aa70-2198-47fc-9b6a-b5a942b0281d.png)

Pode ser feita de dois modos:

Método 1) Pode baixar essa biblioteca na internet, pesquisando biblioteca ESP8266 IDE Arduino, baixar e adicionar biblioteca, em formato .zip a IDE do Arduino.

![image](https://user-images.githubusercontent.com/61547619/125558913-2c3ad2da-5afa-4713-be0d-556a3cdcd36d.png)

Depois recomendo de clique em fechar a página da IDE, e abrir novamente. Selecionar a placa pelo caminho Ferramentas > Placa > ESP8266 Board (1.0.1) > Generic ESP8266 Module

![image](https://user-images.githubusercontent.com/61547619/125559116-2d6cd890-7d22-473f-9de3-3199921e772c.png)

Fim método 1

Método 2) Outro modo de fazer essa tarefa é pesquisar na própria IDE  a biblioteca.

![image](https://user-images.githubusercontent.com/61547619/125563299-a21a8448-95d7-4519-a0af-b50874191d80.png)

Pesquisar 8266

![image](https://user-images.githubusercontent.com/61547619/125563331-8a97ac0e-6a3b-48fe-a289-824bed4999d7.png)

Instalar o pacote

![image](https://user-images.githubusercontent.com/61547619/125563361-933fefa0-9320-437a-9f1a-7928022065d8.png)

Clicar em fechar. Depois recomendo de clique em fechar a página da IDE, e abrir novamente. Selecionar a placa pelo caminha Ferramentas > Placa > ESP8266 Board(1.0.1) > Generic ESP8266 Module

![image](https://user-images.githubusercontent.com/61547619/125563411-95fa7bb8-6922-49ab-bcc7-c4b365970c41.png)

Fim método 2

E já está habilitado o uso da placa ESP8266.
Importante endereçar corretamente qual porta USB o programa está sendo enviado. Em relação a outras configurações necessárias, como CPU Frequency ou Flash Size, essas vão mudar de acordo com a placa que estiver sendo utilizada. Mas essas informações serão colocadas somente uma vez.

![image](https://user-images.githubusercontent.com/61547619/125563585-3e5b0527-7a89-42b0-af7f-5b2161a14e83.png)

5) Quais as informações necessárias para a configurar o programa do blynk na IDE arduino.
Como explicado no exercício 1 é necessário ter:
-  Token: que é o código de segurança que permite a conexão da placa com o celular;

![image](https://user-images.githubusercontent.com/61547619/125563628-07037f94-3c32-4cd6-8e12-eef31d65d24f.png)

 
- Caso for conexão via Wi-Fi é necessário ter o nome da rede e a senha;

![image](https://user-images.githubusercontent.com/61547619/125563784-0a6d848c-55a0-49d2-9951-398f453ef30d.png)
