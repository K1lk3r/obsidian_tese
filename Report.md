## Introduction
## State of the art
#### Synthetic Aperture Radar
sar is a type of Radar technology used for two dimensional high resolution image creation or three dimensional recreation of landscapes. Regardless of weather condition or time of the day. Since it follows RADAR principles, emitting and recording echoes of an eletromagnetic wave weather conditions or time of the day do not have an impact in generating images. The synthetic aperture can be obtained through the movement of the Satellite or airship, as we want a higher resolution we cannot have an antenna that would match it, otherwise the antenna would have a big size that would not fit in a Satellite or airship. 

****Inserir Imagem e explicar a imagem de voo do SAR****

After receiving the echoes of the signals sent by the antenna, we need to process them so the final image can be built. There are many ways of doing this, it can be processed in real time, with a DSP, ASIC or even a MicroController, it can be transmitted and processed, or saved and be processed afterwards. With the goal of this work we are going to use an ALVEO V80 and its properties.

There are multiple algorithms that can convert raw SAR data into images, the picked one is the BackProjection algorithm since it is very simple and can be parallelised very easily. 

#### Ver o que está noutros documentos do sobre SAR e fazer o mesmo
##### Helena [[ARC20.pdf]]
Explica simplesmente o algoritmo como está no paper [[pritsker2015.pdf]] 
##### [[pritsker2015.pdf]]
O que está no background --> em relação a SAR em si, tem só que a aeronave envia ondas/sinais eletromagnéticos e recebe-os de volta, refere também que o cross range é mau e portanto com vários sinais dá para fazer a abertura sintética. E depois explica que se um swath 
#### BackProjection SAR
How does the algorithm work? No que é que ele pega para funcionar nos aspetos físicos da coisa.

#### BackProjection in FPGA
#### Conclusions

## Preliminary work
## Work Proposal
