# Cubo-Interativo


| Componente       | Quantidade | Função |
|------------------|------------|--------|
| Módulo RC522     | 1          | Captura o UID das tags RFID. |
| Tags RFID        | 10         | Cada UID está vinculado a informações de uma árvore. |
| Display OLED     | 1          | Apresenta informações gerais sobre a árvore identificada. |
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
| ESP32            | 1          | Envia dados de temperatura, umidade e qualidade do ar para um broker MQTT. |

obs: ENS160 e AHT21 estão integrados em um único componente
