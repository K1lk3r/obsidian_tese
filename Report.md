## Introduction
## State of the art
#### Synthetic Aperture Radar
sar is a type of Radar technology used for two dimensional high resolution image creation or three dimensional recreation of landscapes. Regardless of weather condition or time of the day. Since it follows RADAR principles, emitting and recording echoes of an eletromagnetic wave weather conditions or time of the day do not have an impact in generating images. The synthetic aperture can be obtained through the movement of the Satellite or airship, as we want a higher resolution we cannot have an antenna that would match it, otherwise the antenna would have a big size that would not fit in a Satellite or airship. 

****Inserir Imagem e explicar a imagem de voo do SAR****


#### Ver o que está noutros documentos do sobre SAR e fazer o mesmo
##### Helena [[ARC20.pdf]]
Explica simplesmente o algoritmo como está no paper [[pritsker2015.pdf]] 
##### [[pritsker2015.pdf]]
O que está no background --> em relação a SAR em si, tem só que a aeronave envia ondas/sinais eletromagnéticos e recebe-os de volta, refere também que o cross range é mau e portanto com vários sinais dá para fazer a abertura sintética. E depois explica que se um swath 
#### BackProjection SAR
How does the algorithm work? No que é que ele pega para funcionar nos aspetos físicos da coisa.

First we need to understand the inputs of the algorithm ...(explicar como é que se obtem a phase history o vector).
The phase 


Then we take this whole information and we apply an *(Inverse)* Fourier Transform, in this case since we are using digital signals we apply the fft (Fast Fourier Transform) to change the data into **something**
Proceed to explain the algorithm as it is in Gorham, posso usar o código de matlab para ajudar no pseudo código (Assim o relatório aumenta de tamanho)

#### BackProjection in FPGA
*Referir de um  modo geral como são feitas as implementações na FPGA seja por HLS, ou uma implementação em vivado* 

There have been multiple implementations of the BackProjection Algorithm in FPGA devices, namely the AMD one (referir o paper da AMD), and they have left a lot of room for improvement, more on that later.
Since the goal of this work is to implement the new AI Engines that are powerful devices for accelerating basic operations (fazer mais pesquisa aqui e comentar bastante os AI engines). They also have a mode for DSP, meaning we can use them for Digital Signal Processing. With this we can conclude that the main goal is to use this AI Engines to Accelerate the maximum we can, and compare with an HLS implementation or even with the DSP Engines 


Copiar um bocado/ Ir buscar cenas que estão no paper/PIC2 da Helena.
#### Conclusions

## Preliminary work
Primeiro comecei por compreender o algoritmo, como funciona, o que são os seus inputs, outputs e depois como é originada a imagem. Para isto fui pesquisar várias implementações do algoritmo, de entre várias a mais citada é sempre a do Gorham... e portanto decidi basear a minha própria implementação do algoritmo nesta, em C uma vez que esta está feita em MatLab. Para isto usei o Gotcha como inputs de dados de SAR para processar, estando em ficheiros de binários MatLab, pensei em duas hipóteses ou ler os dados, de MatLab dentro da minha própria implementação ou converter os dados para ficheiros de binário normais.  
## Work Proposal


