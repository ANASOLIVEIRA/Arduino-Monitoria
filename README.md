# Arduino-Monitoria
1)	Grave no Esp 8266 o programa em C++ para funcionar o programa Blynk com seu celular, em seguida ligue um led na porta GPIO 3 para teste. (descreva os passos necessários para a execução desta questão)

Resposta: Descrição programa Blink. É uma plataforma simples para a integração do uso de placas embarcadas, no caso a placa ESP8266, com o celular. Pode ser utilizado conexão via Wi-Fi ou Bluetooth.
Passo 1) Endereçar a placa ESP8266 na IDE do Arduino.
![image](https://user-images.githubusercontent.com/61547619/125547674-7b32501d-badf-48bb-82bf-1e215cb822c4.png)
Passo 2) Conectar a placa ao celular, verificar se o celular enxerga a placa. Para questões de segurança o aplicativo Blynk gera um token de segurança. e esse token é colocado no código para haver a conectividade, esse token é enviado por email.
         
Passo 3) Criar ambiente no aplicativo. Como só é necessário ligar um led conectado a uma porta. A interface é bem simples.
     
Passo 4) Digitar o código na IDE Arduíno

```C++

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
