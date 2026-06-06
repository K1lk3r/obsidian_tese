##  CIPS

The processing system (PS), platform management controller (PMC), and CCIX PCIe module (CPM) modules are grouped together and configured using the control, interface, and processing system (CIPS) IP core. The PS contains the APUs, RPUs, and peripherals (I2C, UART, SPI, etc.). It shares the DDRMC with the PL via the NoC. The PMC is responsible for boot and configuration management, power management, reliability and safety functions, dynamic function eXchange (DFX), life cycle management and I/O peripherals. The CPM provides the primary interfaces for designs, such as AVED, following the server system methodology. It has hardened connections to the NoC which is used to access the DDR and other hardened IP. The CIPS configuration is described below. All settings differing from the default settings are indicated in the GUI captures below.


Aqui sei que existem 3 modulos principais APU  o processador normal RPU o real time processador e PMC acho que é a programming manager and controller 
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



## AI Engines
Os AI engines são compostos por uma rede de AI Tiles em que cada Tile tem uma memória própria e estão ligadas com as dos Tiles adjacentes com uma pequena nuance em que a memória estiver à esquerda do Tile esta não está ligada com a Memória à direita (com uma imagem fica mais claro).  

Os AI Tiles são simplesmente processadores com vários blocos de processamento que se especializam em AI, corre a 1 GHz e é um chip que usa um ISA, ou seja é um processador que usa instruções como um processador normal.

Estes AI Tiles permitem operações com scalar e com vetores tendo a opção de se fazer as operações com floating ou fixed point. Tendo em conta que existem blocos específicos para cada tipo de operação o (**REVER OS BLOCOS E DESCREVE-LOS**)

As memorias dos tiles estão conetadas em rede adjacentemente, no entanto também tem uma conexão por AXI-Stream, em que um tile tenha feito um processamento e quer passar a outro que está no outro lado do engine, eles podem partilhar esses dados a partir do AXI-Stream, em que os dados são partilhados por stream (broadcast). 

## NoC (Network on Chip)
Isto é o que permite estes sistemas todos comunicarem entre si, e com o IO. (I think)


## Use cases
The capabilities of the V80 mean it is ideal for memory-bound compute applications. These applications include genomics, astrophysics, and, of course, networking, such as packet monitoring, cybersecurity, and offloading computational storage, enabling CPU offload.