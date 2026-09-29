# Semana 1: Sistema Automatizado - Porta Automática

## 1. Objetivo e Classificação
* **Objetivo:** Controlar a abertura e o fecho de uma porta de acesso a um edifício de forma autónoma e segura, garantindo a passagem de peões sem necessidade de contacto físico.
* **Grau de Automação:** Automático. O sistema percebe as condições através de sensores, toma decisões e atua segundo uma lógica previamente definida, sem intervenção do operador.
* **Fronteira do Sistema:** O sistema engloba os sensores locais, o controlador lógico e o motor da porta. Pessoas a caminhar, variações de luz externa ou perdas de energia da rede elétrica pertencem ao ambiente (exterior à fronteira).

## 2. Entradas, Processamento e Saídas
* **Entradas:** Sensor de presença (deteta a aproximação) e Sensor de barreira infravermelha (deteta a área ocupada no limiar da porta).
* **Processamento (Controlador):** Avalia os sinais dos sensores; se houver aproximação E a porta estiver fechada, aciona a abertura. Inicia um temporizador e fecha a porta caso a área esteja livre.
* **Saídas:** Motor elétrico (comanda a tração mecânica para abrir ou fechar as folhas da porta).
* **Realimentação:** O estado atual da porta (posição aberta/fechada) e a informação de área livre ou ocupada (barreira) retornam ao controlador para interromper o movimento ou inverter a marcha, formando uma malha fechada.

## 3. Análise de Falhas e Comportamento Seguro
| Falha / Perturbação | Efeito | Deteção | Resposta Segura |
| :--- | :--- | :--- | :--- |
| **Pessoa parada na porta (Perturbação)** | Impede o fecho no tempo previsto | Barreira interrompida (incoerência temporal) | Interromper o fecho, reabrir a porta e reiniciar o temporizador |
| **Perda de energia elétrica (Falha)** | Paragem total do motor | Ausência de alimentação no circuito | Desacoplar o motor (estado mecânico seguro), permitindo abertura manual livre |
| **Sensor de presença inválido (Falha)** | A porta pode fechar inadvertidamente ou nunca abrir | Incoerência de sinal | Bloquear o fecho automático e manter a porta aberta até diagnóstico |

## 4. Casos de Teste e Resultados (Validação Funcional)
| Cenário | Entrada | Resposta Esperada | 
| :--- | :--- | :--- | 
| **Aproximação válida** | Sensor de presença ativado | Comandar abertura imediata da porta | 
| **Passagem concluída** | Área livre após temporização | Comandar o fecho suave da porta | 
| **Obstáculo durante fecho** | Barreira de infravermelhos interrompida | Parar imediatamente e comandar reabertura | 
| **Emergência / Falha** | Perda de energia total | Libertação mecânica dos trincos para empurrar |
