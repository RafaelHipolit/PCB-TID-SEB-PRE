# Projeto de PCB da IC: Instrumentação para o Estudo de Efeitos de Radiação em Dispositivos Eletrônicos


## Resumo da IC
O avanço da microeletrônica e a constante aplicação de dispositivos semicondutores em ambientes críticos, como os cenários aeroespaciais e nucleares, têm intensificado a necessidade de qualificar componentes eletrônicos quanto à sua tolerância à radiação ionizante. Nesse contexto, a caracterização precisa dos danos provocados exige instrumentação científica capaz de avaliar tanto os efeitos acumulativos, resultantes da Dose Ionizante Total (TID), quanto as falhas estocásticas provocadas por Efeitos de Evento Único (SEE). O presente trabalho teve como objetivo projetar e desenvolver uma plataforma eletrônica integrada, no formato de Placa de Circuito Impresso (PCB), dedicada ao estudo e à caracterização dos efeitos de radiação ionizante em transistores MOSFET de potência. 
        
O circuito implementado foi estruturado em três blocos funcionais distintos: um circuito para monitoramento de TID conectado à plataforma PXI, um circuito protetivo contra Efeitos de Queima por Sobrecorrente (SEB) baseado na Técnica de Limitação de Corrente e um circuito auxiliar de pré-amplificação focado na Espectroscopia de Carga.  Para viabilizar o uso dinâmico da plataforma sem a necessidade de reconfigurações manuais, a alternância de conexão entre os blocos operacionais e o Dispositivo Sob Teste (DUT) foi estabelecida por meio do chaveamento de relés de potência. O projeto elétrico, o layout das camadas e o modelo 3D da PCB foram desenvolvidos e validados computacionalmente no software KiCad, confirmando que a topologia concebida cumpre os requisitos de instrumentação.

---

# Metodologia

As técnicas de medição de efeitos de radiação em transistores, como a
Técnica de Limitação de Corrente e Técnica de Espectroscopia de Carga,
necessitam de componentes e equipamentos que existem comercialmente e
são comumente encontradas em laboratórios de física nuclear. Entretanto,
devido à grande variedade de dispositivos eletrônicos necessários para
implementar as diferentes técnicas, não existe uma solução comercial
viável de propósito geral para qualificação de transistores sob efeitos
de radiação. Assim, percebe-se uma necessidade de desenvolver uma
plataforma integrada de testes suficientemente geral que atenda
simultaneamente às exigências específicas de ensaios de efeitos
estocásticos e acumulativos de radiação para uma ampla gama de
transistores.

Tendo esse contexto em mente, este projeto de pesquisa visa projetar uma
plataforma integrada, na forma de placa de circuito impresso (PCB -
*Printed Circuit Board*) que auxilie o estudo e caracterização dos
efeitos de radiação ionizante em dispositivos eletrônicos. A PCB a ser
elaborada deve focar em TID para efeitos acumulativos e SEE para efeitos
estocásticos. Para medição de SEE deve-se utilizar a Técnica de
Limitação de Corrente e Técnica de Espectroscopia de Carga.

O circuito projetado na PCB deve ser dividido em três blocos: Circuito
TID, Circuito SEB e Circuito Pré-Amplificador. Os três circuitos devem
ser integrados de forma que apenas um esteja conectado ao DUT por vez e
que a troca do circuito conectado ao DUT possa ser realizada
dinamicamente.

## Circuito TID

Esse circuito deve auxiliar na medição do efeito de TID. Para isso ele
deve conectar os terminais do DUT a uma SMU para monitoramento de
parâmetros do dispositivo. No caso desse projeto, a SMU será por meio da
plataforma modular PXI (*PCI eXtensions for Instrumentation*). Portanto,
a saída deste circuito deve obedecer a padronização de conexão com a
plataforma PXI. Tal padrão consiste de nove eletrodos de controle e
automação, que obedece o seguinte ordenamento sequencial:

-   Eletrodo positivo de porta (POS G).

-   Eletrodo negativo de porta (NEG G).

-   Eletrodo positivo de dreno (POS D).

-   Eletrodo negativo de dreno (NED G).

-   Eletrodo negativo de sensoriamento de dreno (NEG SD).

-   Eletrodo positivo de sensoriamento de dreno (POS SD).

-   Fonte DC (+5 V).

-   Fonte DC (+5 V).

-   Fonte DC (+5 V).

Em nosso contexto, os últimos três terminais de fonte DC +5 V são
utilizados para controle automatizado de relês de alta tensão.

## Circuito SEB

O Circuito SEB deve auxiliar a medição do Efeito Único de Queima por
Sobrecorrente. Para isso, ele deve implementar a Técnica de Limitação de
Corrente com um arranjo de resistores de proteção. A saída do circuito
deve disponibiliza os sinais transientes do DUT para instrumentos
externos de aquisição. O terminal de saída desse circuito deve possuir
impedância de 50para evitar reflexões em sistemas de aquisição
ultra-rápidos. Além disso, o sistema protetivo deve possibilitar a
seleção do resistor de proteção apropriado (10 k- 1 M) ao DUT, de forma
a assegurar a eficácia da técnica de limitação de corrente.

## Circuito Pré-Amplificador

O Circuito Pré-Amplificador deve auxiliar o arranjo da Técnica de
Espectroscopia de Carga por meio da implementação do Pré-Amplificador
Sensível à Carga presente nesta técnica. Sua saída deve apresentar
impedância de 50 ohms para casamento com sistemas de aquisição
ultra-rápidos. Para definir o ganho nominal de pré-amplificação de
aproximadamente 45 mV/MeV em sensores de silício, um capacitor de
retroalimentação de 1 pF foi escolhido. Para possibilitar a
discriminação de eventos distintos induzidos por partículas ionizantes a
taxas médias inferiores a $2 \times 10^{6}$ eventos/s, tipicamente
adotadas em testes dedicados com aceleradores de partículas, um resistor
de retroalimentação de 100 kfoi considerado.

## Integração dos circuitos

Os três circuitos devem ser integrados de forma que apenas um esteja
conectado ao DUT por vez. Para realizar essa alternância de conexão deve
ser utilizados relés de potência para conectar apenas um dos circuitos
por vez ao DUT. O controle desses relés deve ser por meio plataforma
PXI, utilizando a conexão implementada no Circuito TID.

## Conexão com o transistor DUT

Visando o propósito generalista da plataforma integrada de testes e
buscando maior praticidade na substituição de diferentes DUTs na
instrumentação proposta, optou-se por realizar a conexão entre o DUT e o
sistema por meio do acoplamento entre uma PCB-mãe (sistema) e uma
PCB-filha (DUT), através de barras de pinos torneados. A PCB-filha deve
passar os sinais de porta, dreno e fonte. O uso dessa arquitetura
modular justifica-se por sua disponibilidade prévia no Laboratório onde
este projeto é realizado, facilitando o uso de diferentes transistores
na PCB elaborada neste projeto.

# Resultados

Este capítulo descreve o projeto de PCB elaborada para atender ao
objetivos do presente trabalho.

## Esquemático da PCB

A Figura mostra o esquemático da PCB
elaborada no software KiCad.

![Esquemático da
PCB.](images/circuitoABC_schematic.pdf)

Esquemático da PCB.

Esquemático da
PCB.

### Configuração da interface PXI

Os 9 pinos que se conectam à interface PXI seguem a estrutura na PCB:

-   POS G: sinal de tensão do *gate-source* do transistor.

-   NEG G: sinal de terra.

-   POS D: sinal de tensão do *drain-source* do transistor.

-   NEG D: sinal de terra.

-   NEG SD: sinal de terra.

-   POS SD: sinal de tensão do *drain-source* do transistor.

-   +5V RELAY1: ativa o relé 1 com 5V.

-   +5V RELAY2: ativa o relé 2 com 5V.

-   +5V RELAY3: ativa o relé 3 com 5V.

### Arranjo de resistores de proteção

No circuito SEB, devido a diferentes possíveis necessidades de valor
para o resistor de proteção empregado na Técnica de Limitação de
Corrente, foi elaborado um arranjo de resistores de proteção. Neste
arranjo há espaço para 9 resistores de proteção.

A conexão do resistor RP1 ou dos demais resistores pode ser alterada
dinamicamente utilizando o relé 3. Os resistores RP2 até RP9 estão
conectados em paralelo, porém cada um pode ser desconectado manualmente
utilizando um jumper. Ademais, uma trilha para conexão sem resistor de
proteção está presente.

### Configuração dos relés

Foram utilizados 3 relés duplos, ou seja, 3 circuitos integrados nos
quais cada um contém 2 relés que são ativados simultaneamente. Os relés
1 e 2 realizam a troca de conexão dos circuitos com o DUT. O relé 3
realiza a troca de resistor de proteção dinamicamente. A tabela descreve
a configuração de cada relé.


|-------- |--------------------- |--------------------------------
|Relé 1   |Normalmente Aberto    |Conecta o porta e dreno do DUT ao Circuito TID                              
|         |Normalmente Fechado   |Conecta o porta e dreno do DUT ao Circuito SEB ou Pré-Amp.
|-------- |--------------------- |--------------------------------
|Relé 2   |Normalmente Aberto    |Conecta o porta e dreno do DUT ao Circuito Pré-Amplificador                               
|         |Normalmente Fechado   |Conecta o porta e dreno do DUT ao Circuito SEB
|-------- |--------------------- |--------------------------------
|Relé 3   |Normalmente Aberto    |Utiliza o resistores RP2 a RP9 como resistor de proteção                              
|         |Normalmente Fechado   |Utiliza o resistor RP1 como resistor de proteção
|         |                      |
|-------- |--------------------- |--------------------------------

  : Configuração de cada relé.
:::

## Layout da PCB

A Figura mostra o layout da PCB elaborada no
software KiCad. Na esquerda da PCB se encontra o Circuito SEB e Circuito
TID. Na borda da placa, encontram-se os conectores dos sinais de entrada
e saída do Circuito SEB. Em seguida é visível o arranjo de resistores de
proteção, os 3 relés e os pinos para conexão do Circuito TID com a
plataforma PXI. No centro da PCB encontram-se os pinos para conexão com
a PCB-filha e, portanto, conexão com o DUT. Na direita da PCB há o
Circuito Pré-Amplificador.

![Layout da camada inferior da PCB.](images/circuitoABC_layout_B_zoom.png)

Layout da camada inferior da PCB.

![Layout da camada superior da PCB](images/circuitoABC_layout_F_zoom.png)

Layout da camada superior da PCB


A Figura mostra o modelo 3D da PCB no software
KiCad, no qual é possível visualizar todos os componentes da placa e as
legendas impressas na camada de serigrafia (*silkscreen*) dos conectores
de entrada e saída dos sinais.

![Modelo 3D da PCB no software KiCad. Visualização da camada
inferior.](images/circuitoABC_3d.png)

Modelo 3D da PCB no software KiCad. Visualização da camada
inferior.
