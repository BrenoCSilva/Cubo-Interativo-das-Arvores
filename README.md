
# Descrição do Protótipo

Trabalho desenvolvido na disciplina Projeto Integrado à Computação I, sob a orientação do professor Vinícius Fernandes Soares Mota, em parceria com o curso de Arquitetura e Urbanismo, representado pela professora Marcela Almeida. O projeto tem como objetivo a criação de um cubo interativo que exibe informações sobre árvores previamente selecionadas e coleta dados ambientais do entorno, como a temperatura e a qualidade do ar. Cada face do cubo apresenta uma categoria específica de informações, como porte da árvore, floração, frutificação, dados do ambiente e dados gerais.

## Disposição das Informações  

Cada face do cubo interativo apresenta uma categoria específica de informações:  

- **Face 1:** Informações gerais da árvore (Nome, origem, bioma e copa).  
- **Face 2:** Porte da árvore (pequeno, médio, grande).  
- **Face 3:** Dados ambientais (temperatura e qualidade do ar).  
- **Face 4:** Floração (indicação de presença e meses de floração).  
- **Face 5:** Frutificação (indicação de presença e meses de frutificação).  
- **Face 6:** Face cega - Sem informações, utilizada para apoio.  
 
# Componentes

| Componente       | Quantidade | Função |
|------------------|------------|--------|
| Módulo RC522     | 1          | Captura o UID das tags RFID. |
| Tags RFID        | 10         | Cada UID está vinculado a informações de uma árvore. |
| Display OLED SH1106 128x64    | 1          | Apresenta informações gerais sobre a árvore identificada. |
| Fita LED (3 segmentos)  | 1   | Indica o porte da árvore (pequeno, médio, grande). |
| Fita LED (10 segmentos) | 1   | Sinaliza se a árvore possui flor. |
| Fita LED (12 segmentos) | 1   | Apresenta os meses de floração. |
| Fita LED (1 segmento)  | 1   | Sinaliza se a árvore possui fruto. |
| Fita LED (12 segmentos) | 1   | Apresenta os meses de frutificação. |
| Botões            | 7         | Inicializam/desligam informações da face ou alternam os dados exibidos. |
| Fita LED (9 segmentos)  | 1   | Indica a temperatura do ambiente. |
| Fita LED (9 segmentos)  | 1   | Indica a qualidade do ar no ambiente. |
| Sensor ENS160     | 1         | Captura a qualidade do ar, CO₂ e compostos orgânicos voláteis (VOCs). |
| Sensor AHT21      | 1         | Mede temperatura e umidade do ambiente. |
| Arduino Mega     | 1          | Controla os sensores RFID, LEDs e botões, processando e exibindo informações sobre as árvores.        |
| ESP32            | 1          | Coleta dados dos sensores de temperatura e qualidade do ar e os envia para um broker MQTT. |
| PowerBank            | 1          | Alimentar o circuito e componentes. |

**Observação**: Os sensores ENS160 e AHT21 estão integrados em um único módulo.


# Processo de Montagem 

As faces do cubo foram cortadas utilizando uma máquina de corte automatizada, garantindo precisão nas dimensões e encaixes. Os componentes eletrônicos foram distribuídos de acordo com a funcionalidade de cada face e conectados ao Arduino Mega e ao ESP32 conforme necessário.

<div align="center">
<table>
 <tr>
   <td>
      <img src="imagens/arestas.jpeg" alt="Integracao 1" width="200px">
   </td>
    <td>
     <img src="imagens/corte.jpeg" alt="Integracao 1" width="200px">
   </td>
    <td>
     <img src="imagens/corte2.jpeg" alt="Integracao 1" width="200px">
   </td>
 </tr>
</table>
</div>

### Conexão do Módulo RC522 (Leitor RFID) ao Arduino Mega  

O módulo RC522 é responsável pela leitura das tags RFID que identificam as árvores cadastradas. Ele se comunica com o Arduino Mega por meio do protocolo SPI. Abaixo estão as conexões utilizadas:  
<div align="center">
<table>
  <tr>
    <td>
      <img src="imagens/RC522.jpeg" alt="Conexão RC522 com Arduino Mega" width="400px">
    </td>
    <td>
      <table>
        <tr><th>Pino do RC522</th><th>Pino do Arduino Mega</th></tr>
        <tr><td><b>3.3V</b></td><td><b>3.3V</b></td></tr>
        <tr><td><b>GND</b></td><td><b>GND</b></td></tr>
        <tr><td><b>RESET</b></td><td><b>Porta digital 5</b></td></tr>
        <tr><td><b>SDA</b></td><td><b>Porta digital 53</b></td></tr>
        <tr><td><b>SCL</b></td><td><b>Porta digital 52</b></td></tr>
        <tr><td><b>MOSI</b></td><td><b>Porta digital 51</b></td></tr>
        <tr><td><b>MISO</b></td><td><b>Porta digital 50</b></td></tr>
      </table>
    </td>
  </tr>
</table>
</div>

### Conexão do DISPLAY OLED (SH1106 128x64) ao Arduino Mega  

O display é responsável por apresentar as informações gerais cadastradas. Como nome, origem, bioma e copa. Ele se comunica com o Arduino Mega por meio do protocolo I2C. Abaixo estão as conexões utilizadas:  
<div align="center">
 <table>
 <tr>
   <td>
      <img src="imagens/displayOLED.jpeg" alt="Conexão DISPLAY com o Arduino Mega" width="400px">
   </td>
   <td>
      <table>
        <tr><th>Pino do Display Oled </th><th>Pino do Arduino Mega</th></tr>
        <tr><td><b>3.3V</b></td><td><b>3.3V</b></td></tr>
        <tr><td><b>GND</b></td><td><b>GND</b></td></tr>
        <tr><td><b>SDA</b></td><td><b>Porta digital 20</b></td></tr>
        <tr><td><b>SCL</b></td><td><b>Porta digital 21</b></td></tr>
      </table>
   </td>
 </tr>
</table>
</div>

### Distribuição de Tensão e Terra  

Como vários componentes começaram a utilizar as mesmas portas do Arduino, foi necessário organizar melhor as conexões. Para isso, utilizamos uma placa de fenolite, criando trilhas para as portas mais utilizadas:  

<div align="center">
<table>
 <tr>
   <td>
      <img src="imagens/plaquinha.png" alt=" placa de fenolite" width="400px">
   </td>
   <td>
      <img src="imagens/aranha1.jpeg" alt="Distribuição de trilhas na placa de fenolite" width="400px">
   </td>
   <td>
     <table>
        <tr><th>Porta</th><th>Cor</th></tr>
        <tr><td><b>GND</b></td><td>⚪ Branco</td></tr>
        <tr><td><b>5V</b></td><td>🔴 Vermelho</td></tr>
        <tr><td><b>3.3V</b></td><td>🟡 Amarelo</td></tr>
      </table>
   </td>
 </tr>
</table>
</div>

### Integração: Módulo RFID e Display OLED  

 Integração entre o **módulo RFID** e o **display OLED (SH1106 128x64)**, conectados ao **Arduino Mega**. O display foi configurado para exibir mensagens conforme a interação com o RFID.  

A imagem abaixo mostra a configuração do hardware, onde os componentes estão interligados por meio de uma placa de fenolite, responsável por distribuir as tensões corretamente.  

<div align="center">
  <img src="imagens/integrado1.jpeg" alt="Integração do módulo RFID com Display OLED" width="400px">
</div>

> **Mensagem no Display:** "Aproxime-se de uma árvore...!"  
> Essa mensagem é um indicativo de que o sistema está aguardando um cartão RFID.

# Conexão da Fita LED  

A imagem abaixo ilustra a configuração da conexão:  

<div align="center">
<table>
 <tr>
   <td>
      <img src="imagens/fitaled.jpeg" alt="Fita LED" width="350px">
   </td>
   <td>
     <table>
        <tr><th>ESP32</th><th>Fita LED</th></tr>
        <tr><td><b>GND</b></td><td>GND</td></tr>
        <tr><td><b>5V</b></td><td>5V</td></tr>
        <tr><td><b>Porta digital</b></td><td>Conexão de dados</td></tr>
      </table>
   </td>
 </tr>
</table>
</div>

---

## Integração: Fita LED e Módulo RFID  

A integração entre o **módulo RFID**, **Fita LED** e **botão de interação** é realizada utilizando um **Arduino Mega**.  

A imagem abaixo apresenta a configuração do hardware, onde os componentes estão conectados por meio de uma **placa de fenolite**, responsável por distribuir corretamente as tensões e conexões.  

O sistema funciona da seguinte forma:  
- Ao aproximar uma **tag RFID** do módulo, o botão permite a interação.  
- O LED verde acende caso a árvore vinculada ao UID contenha frutos, e vermelho caso contrário.  
- Outra Fita LED indica, em **amarelo**, os meses de frutificação. Na imagem, a configuração abrange os **12 meses do ano**.  

<div align="center">
<table>
 <tr>
   <td>
      <img src="imagens/FACE1e5-Integrada.jpeg" alt="Integracao 1" width="400px">
   </td>
   <td>
     <table>
        <tr><th>Arduino Mega</th><th>Placa de Fenolite</th></tr>
        <tr><td><b>GND</b></td><td>Trilha 1</td></tr>
        <tr><td><b>5V</b></td><td>Trilha 2</td></tr>
        <tr><td><b>3.3V</b></td><td>Trilha 3</td></tr>
      </table>
   </td>
     <td>
     <table>
        <tr><th>Componente</th><th>Conexão</th></tr>
        <tr><td><b>GND - Fita LED</b></td><td>Placa - Trilha 1</td></tr>
        <tr><td><b>Terminal 1 - GND Botão</b></td><td>Placa - Trilha 1</td></tr>
        <tr><td><b>GND - RC522</b></td><td>Placa - Trilha 1</td></tr>
        <tr><td><b>GND - Display</b></td><td>Placa - Trilha 1</td></tr>
        <tr><td><b>5V - Fita LED</b></td><td>Placa - Trilha 2</td></tr>
        <tr><td><b>3.3V - RC522</b></td><td>Placa - Trilha 3</td></tr>
        <tr><td><b>3.3V - Display</b></td><td>Placa - Trilha 3</td></tr>
        <tr><td><b>Terminal 2 - Botão</b></td><td>Porta digital</td></tr>
        <tr><td><b>Demais conexões do Display e RC522</b></td><td>Se repetem</td></tr>
      </table>
   </td>
 </tr>
</table>
</div>

---

## Integração: Fita LED, Módulo RFID e Display OLED  

Integração **módulo RFID**, **Display OLED (SH1106 128x64)**, **Fita LED** e **botões de interação**, todos conectados ao **Arduino Mega**.  

O link abaixo é um pequeno vídeo onde explico o funcionamento das **Faces 1 (Informações Gerais)** e **Face 5 (Frutificação)**, que estão integradas ao sistema.  

👉 [Acesse aqui a explicação detalhada](https://www.youtube.com/shorts/Pyn25ikelZ8)



# Processo de Montagem II e testes 

<div align="center">
<table>
 <tr>
   <td>
      <img src="imagens/FitaLED1.jpeg" alt="Integracao 1" width="200px">
   </td>
    <td>
     <img src="imagens/FitaLED2.jpeg" alt="Integracao 1" width="200px">
   </td>
    <td>
     <img src="imagens/teste1.jpeg" alt="Integracao 1" width="200px">
   </td>
   <td>
     <img src="imagens/corte-temp.jpeg" alt="Integracao 1" width="200px">
      <p>face 3 - Temperatua e Qualidade do Ar.</p>
   </td>
 </tr>
</table>
 <table>
 <tr>
   <td>
      <img src="imagens/teste.jpeg" alt="Integracao 1" width="200px">
       <p>Integração da face 4 - Floração.</p>
   </td>
    <td>
     <img src="imagens/teste2.jpeg" alt="Integracao 1" width="200px">
   </td>
    <td>
     <img src="imagens/porte.jpeg" alt="Integracao 1" width="200px">
     <p>face 2 - Porte</p>
   </td>
   <td>
     <img src="imagens/corte-temp.jpeg" alt="Integracao 1" width="200px">
   </td>
 </tr>
</table>
</div>


