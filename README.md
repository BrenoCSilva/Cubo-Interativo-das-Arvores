
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

**Observação**: Os sensores ENS160 e AHT21 estão integrados em um único módulo.


# Processo de Montagem 

As faces do cubo foram cortadas utilizando uma máquina de corte automatizada, garantindo precisão nas dimensões e encaixes. Os componentes eletrônicos foram distribuídos de acordo com a funcionalidade de cada face e conectados ao Arduino Mega e ao ESP32 conforme necessário.



### Conexão do Módulo RC522 (Leitor RFID) ao Arduino Mega  

O módulo RC522 é responsável pela leitura das tags RFID que identificam as árvores cadastradas. Ele se comunica com o Arduino Mega por meio do protocolo SPI. Abaixo estão as conexões utilizadas:  
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

### Conexão do DISPLAY OLED (SH1106 128x64) ao Arduino Mega  

O display é responsável por apresentar as informações gerais da cadastradas. Como nome, origem, bioma e copa. Ele se comunica com o Arduino Mega por meio do protocolo I2C. Abaixo estão as conexões utilizadas:  
 <table>
 <tr>
   <td>
      <img src="imagens/displayOLED.jpeg" alt="Conexão DISPLAY com o Arduino Mega" style="width: 220px; margin-right: 30px;">
   </td>
   <td>
    <div> 
      <table>
        <tr><th>Pino do Display Oled </th><th>Pino do Arduino Mega</th></tr>
        <tr><td><b>3.3V</b></td><td><b>3.3V</b></td></tr>
        <tr><td><b>GND</b></td><td><b>GND</b></td></tr>
        <tr><td><b>SDA</b></td><td><b>Porta digital 20</b></td></tr>
        <tr><td><b>SCL</b></td><td><b>Porta digital 21</b></td></tr>
      </table>
    </div>
   </td>
 </tr>
</table>






