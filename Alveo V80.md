 ##  CIPS

The processing system (PS), platform management controller (PMC), and CCIX PCIe module (CPM) modules are grouped together and configured using the control, interface, and processing system (CIPS) IP core. The PS contains the APUs, RPUs, and peripherals (I2C, UART, SPI, etc.). It shares the DDRMC with the PL via the NoC. The PMC is responsible for boot and configuration management, power management, reliability and safety functions, dynamic function eXchange (DFX), life cycle management and I/O peripherals. The CPM provides the primary interfaces for designs, such as AVED, following the server system methodology. It has hardened connections to the NoC which is used to access the DDR and other hardened IP. The CIPS configuration is described below. All settings differing from the default settings are indicated in the GUI captures below.


Aqui sei que existem 3 modulos principais APU  o processador normal RPU o real time processador e PMC acho que é a programming manager and controller 


## Control, Interface and Processing System (CIPS)

O Control, Interface and Processing System (CIPS) constitui o subsistema responsável pelo controlo e gestão do dispositivo Versal Adaptive SoC. Este bloco integra processadores de propósito geral, controladores de periféricos, interfaces de comunicação externas e mecanismos de configuração do sistema, funcionando como ponto central de coordenação dos restantes recursos computacionais.

**The CIPS, Control, Interface and Processing Systems, forms the subsystem responsible for the control and management of the Versal Adaptive SoC. This block integrates General Purpose processors, Peripheral Controls, External Communication Interface, System Configuration Mechanisms, working as a central coordination point for the remainder of computational resources.

O CIPS inclui um conjunto de processadores Arm Cortex-A72 de 64 bits destinados à execução de sistemas operativos e aplicações de elevado nível, bem como processadores Arm Cortex-R5F concebidos para tarefas determinísticas e de tempo real. Esta combinação permite separar funções de controlo, gestão de recursos e execução de aplicações das tarefas computacionalmente intensivas executadas na lógica programável e nos AI Engines.

**CIPS includes a set of ARM Cortex-A72 processors of 64 bits, destined to the execution of Operating Systems, and High Level applications. It also includes an ARM Cortex-R5F, designed for deterministic and Real-Time tasks. This combination allows for the separation of control functions, Resource Management and Application execution of computational heavy tasks executed in Programming Logic and AI Engines.**

Além das unidades de processamento, o CIPS disponibiliza um conjunto abrangente de interfaces de comunicação que permitem a integração do dispositivo com sistemas externos e com os restantes blocos internos da arquitetura. Estas interfaces incluem controladores PCI Express, Ethernet, UART, SPI, I2C, GPIO e mecanismos de acesso à memória externa.

**Besides the Processing Units CIPS offers a set of broad communication interfaces that allows the integration of the device (Alveo V80) with External Systems and the remaining internal blocks of the architecture. This interfaces include PCI Express Controlers, Ethernet, UART, SPI, I2C, GPIO and External memory access mechanisms.**

O CIPS é também responsável pelo processo de arranque (\textit{boot}), configuração do dispositivo e gestão dos recursos de segurança. Durante a inicialização do sistema, este subsistema coordena a configuração da lógica programável, dos AI Engines e dos restantes componentes da plataforma.

**CIPS is also responsible for boot process, device configuration and security resource management. During System initialization, this subsystem coordinates the Programming Logic configuration, AI Engines and the rest of the platform components.   **

\paragraph{Application Processing Unit}



A Application Processing Unit (APU) é composta por dois processadores Arm Cortex-A72 de 64 bits que executam sistemas operativos como Linux ou aplicações bare-metal. Estes processadores são normalmente responsáveis pela gestão de tarefas de elevado nível, controlo da aplicação e coordenação da execução dos aceleradores implementados no dispositivo.

The APU -- Aplications Processing Unit is composed of two ARM Cortex-A72 64 bits processors that execute Operating Systems like Linux or Bare Metal Applications. This Processors are normally responsible for high level task management, application control and the coordination of the execution of accelerators implemented in the device. 

The Cortex-A72 posses multi-level cache memory and complex software execution support allowing the Versal to work as an autonumous computational system without the need of an external processor.  

Os Cortex-A72 possuem memória cache multinível e suporte para execução de software complexo, permitindo que o Versal funcione como um sistema computacional autónomo sem necessidade de um processador externo.

\paragraph{Real-Time Processing Unit}

A Real-Time Processing Unit (RPU) integra dois processadores Arm Cortex-R5F concebidos para aplicações críticas em termos temporais. Estes núcleos podem operar de forma independente ou em modo lockstep para aumentar a tolerância a falhas.

As aplicações típicas incluem controlo industrial, monitorização do sistema, gestão de comunicações e execução de tarefas com requisitos rigorosos de latência.

**The RPU - Real-Time Processing Unit integrates two ARM Cortex-R5F processors designed for critical applications in terms of time. This cores can operate independently or in lockstep mode to raise fault tolerance. 
The typical applications  include industrial control, system monitoring, communication management and task execution with rigorous latency requisites. **

\paragraph{Interfaces de Comunicação}

O CIPS disponibiliza diversas interfaces de comunicação que permitem a integração da plataforma em sistemas heterogéneos.

A interface PCI Express constitui uma das principais formas de comunicação entre a placa Alveo V80 e o sistema hospedeiro. Esta interface permite transferências de dados de elevada largura de banda entre a memória do servidor e os aceleradores implementados no dispositivo.

Para aplicações de rede, o dispositivo suporta interfaces Ethernet de elevada velocidade, possibilitando a receção e transmissão direta de fluxos de dados sem necessidade de processamento intermédio pelo processador principal.

Adicionalmente, encontram-se disponíveis interfaces UART, SPI e I2C destinadas à configuração, depuração e comunicação com periféricos externos. Estas interfaces são frequentemente utilizadas durante as fases de desenvolvimento e integração do sistema.

\paragraph{Integração com a Network-on-Chip}

O acesso aos recursos computacionais e de memória do dispositivo é realizado através da Network-on-Chip (NoC). O CIPS comunica com a lógica programável, os AI Engines e os controladores de memória através desta infraestrutura de interligação de elevada largura de banda.

A utilização da NoC elimina muitos dos estrangulamentos associados às arquiteturas FPGA tradicionais, permitindo que os processadores acedam eficientemente aos dados armazenados na memória HBM e coordenem a execução dos aceleradores distribuídos pelo dispositivo.

No contexto desta dissertação, o CIPS desempenha principalmente funções de orquestração e controlo da aplicação. Os processadores Arm são responsáveis pela configuração dos aceleradores, gestão das transferências de dados e coordenação da execução, enquanto as operações computacionalmente mais exigentes são executadas na lógica programável e nos AI Engines. Esta separação permite explorar eficientemente a heterogeneidade da arquitetura Versal, reservando os recursos especializados para as etapas críticas do algoritmo de Backprojection.
###### APU


###### RPU
###### PMC

\subsection{AMD Alveo V80 Accelerator Card}

A AMD Alveo V80 é uma placa aceleradora para centros de dados baseada no dispositivo AMD Versal HBM XCV80 Adaptive SoC. Foi desenvolvida para aplicações intensivas em memória e computação, incluindo High Performance Computing (HPC), processamento de sinais, análise de dados, redes de comunicação e aplicações de inteligência artificial.

A placa integra diferentes tipos de recursos computacionais num único dispositivo heterogéneo, combinando processadores Arm, lógica reconfigurável FPGA, uma rede interna de comunicação (Network-on-Chip), motores especializados de computação vetorial denominados AI Engines e memória de elevada largura de banda (HBM2e). Esta arquitetura permite adaptar o hardware à aplicação e explorar elevados níveis de paralelismo. A Alveo V80 disponibiliza aproximadamente 32 GB de memória HBM2e com uma largura de banda superior a 800 GB/s, constituindo uma plataforma adequada para aplicações limitadas pelo acesso à memória.

The AMD Alveo V80 is an accelerator for data center based on the AMD device Versal HBM XCV80 Adaptive Soc. It was developed for intensive, memory apps and computations including High Performance Computing (HPC), Signal Processing, Data Analysis, Network Communication and AI applications.

The board integrates several types of computational resources in a single heterogeneous device, combinig ARM processors, Reconfigurable Logic (FPGA), an internal communication Network (Network-on-Chip (NoC)), Engines specialized in vectorial computation named AI Engines and High Memory Bandwidth (HBM2e). This architecture allows the hardware to adapt to the application and explore high level of parallelism. The Alveo V80 offers more or less 32 GB of memory HBM2e with a bandwidth that can surpass of 800 GB/s , allowing for memory bound applications.


\subsubsection{Processing System}

O Processing System (PS) corresponde à componente de processamento convencional do Versal Adaptive SoC. Esta região integra processadores Arm Cortex-A72 de 64 bits destinados à execução de sistemas operativos e aplicações de controlo, bem como processadores Arm Cortex-R5 para tarefas de tempo real.

O PS é normalmente responsável pela configuração do sistema, gestão da comunicação entre os diferentes blocos do dispositivo e coordenação das tarefas executadas pelos restantes recursos computacionais. Desta forma, o processamento de controlo permanece separado das operações intensivas em computação implementadas na lógica programável e nos AI Engines.

The Processing System corresponds to the componet of conventional processing of the Versal Adaptive SoC. This region integrates ARM Cortex-A72 64 bit processor, destined to operating systems and control application execution. It also has ARM Cortex-R5  processor for Real-Time Processing tasks.

## PL (programming logic)
Falar só um pouco dos valores de BRAM LUT's DSP's, se bem que não sei bem o que tem de DSP porque existem DSP's engines na placa também.


\subsubsection{Programmable Logic (PL)}

A Programmable Logic (PL) corresponde à região de lógica reconfigurável do dispositivo Versal Adaptive SoC. Esta componente herda as principais características das arquiteturas FPGA tradicionais, permitindo a implementação de circuitos digitais personalizados adaptados aos requisitos específicos da aplicação.

Ao contrário dos processadores convencionais, que executam sequencialmente instruções armazenadas em memória, a lógica programável permite criar arquiteturas dedicadas onde múltiplas operações são executadas em paralelo. Esta abordagem possibilita atingir elevados níveis de desempenho e eficiência energética em aplicações de processamento intensivo.

Na arquitetura Versal, a Programmable Logic funciona em conjunto com o Control, Interface and Processing System (CIPS), os AI Engines e a Network-on-Chip (NoC), constituindo um dos principais recursos computacionais disponíveis para aceleração de algoritmos.

Programmable Logic 

## AI Engines
Os AI engines são compostos por uma rede de AI Tiles em que cada Tile tem uma memória própria e estão ligadas com as dos Tiles adjacentes com uma pequena nuance em que a memória estiver à esquerda do Tile esta não está ligada com a Memória à direita (com uma imagem fica mais claro).  

Os AI Tiles são simplesmente processadores com vários blocos de processamento que se especializam em AI, corre a 1 GHz e é um chip que usa um ISA, ou seja é um processador que usa instruções como um processador normal.

Estes AI Tiles permitem operações com scalar e com vetores tendo a opção de se fazer as operações com floating ou fixed point. Tendo em conta que existem blocos específicos para cada tipo de operação o (**REVER OS BLOCOS E DESCREVE-LOS**)

As memorias dos tiles estão conetadas em rede adjacentemente, no entanto também tem uma conexão por AXI-Stream, em que um tile tenha feito um processamento e quer passar a outro que está no outro lado do engine, eles podem partilhar esses dados a partir do AXI-Stream, em que os dados são partilhados por stream (broadcast). 

## NoC (Network on Chip)
Isto é o que permite estes sistemas todos comunicarem entre si, e com o IO. (I think)


## Use cases
The capabilities of the V80 mean it is ideal for memory-bound compute applications. These applications include genomics, astrophysics, and, of course, networking, such as packet monitoring, cybersecurity, and offloading computational storage, enabling CPU offload.