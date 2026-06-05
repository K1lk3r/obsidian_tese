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
How does the algorithm work? No que é que ele pega para funcionar nos aspectos físicos da coisa.

First we need to understand the inputs of the algorithm ...(explicar como é que se obtém a phase history o vector).
The phase history is a big vector of data that is our main point of information so we can start making use of our algorithm and form the image. It's given by this expression (equação 5 do Gorham).

Where $A(f_k,\tau_n)$ is the amplitude of the signal related to the radar cross section (RCS é o quanto um objecto é detectado pelo radar quanto maior o valor mais detectável o objecto é) of the target meaning. This means that depending where our target is, closer or further, our amplitude is bigger or smaller respectively.
The phase (colocar a expressão da fase) depends on the frequency of each sample and the differential range given by (colocar a expressão do range diferencial). **Explicar o range diferencial**
The differential range is the distance between the target and the origin of the scene, meaning the "first location of the image/flight". So this means that for each signal, chirp signal, we have a vector of phase history. This vector has a size of K, where K is the number of frequencies that the chirp signal has. This adjacent to the number of pulses, the phase history is a massive matrix of size K frequencies per $N_p$
pulses. Why did I say in the beginning vector? Since we are trying for Real Time Processing the whole data is not immediately available, which means we only need to have a vector to store the data. Besides flattening a matrix to a vector is more optimal to access data. *Não gosto desta frase* 


A ifft aparece da simplificação das expressões porque sabemos que o  $f_k$ é o $f_1$ com um $\Delta f$ porque estamos no domínio digital. Desta simplificação aparece então a Transformada Inversa de Fourier da phase history     
![[Pasted image 20260601154956.png]]

![[Pasted image 20260601150232.png]]

Then we take this whole information and we apply an *(Inverse)* Fourier Transform, in this case since we are using digital signals we apply the fft (Fast Fourier Transform) to change the data into **something**
Proceed to explain the algorithm as it is in Gorham, posso usar o código de matlab para ajudar no pseudo código (Assim o relatório aumenta de tamanho)


Input: Range-compressed SAR data S(pulse_index, range_sample) Input: Radar trajectory positions R_p for each pulse Input: Output image grid P(x, y) with coordinates Output: Focused SAR Image I(x, y) Initialize I(x, y) = 0 for all pixels For each pixel (x, y) in grid P: For each pulse index n: 1. Get Radar Position: pos = R_p[n] 2. Calculate Slant Range: r_n = distance(pos, (x, y)) 3. Determine Range Sample Index: idx = r_n * (2 * bandwidth / speed_of_light) (Map physical range to discrete signal index) 4. Interpolate Signal Value: s_val = interpolate(S[n], idx) 5. Calculate Phase Compensation: phase = exp(-j * 4 * pi * frequency / c * r_n) 6. Accumulate Energy: I(x, y) = I(x, y) + (s_val * phase) Return I(x, y)


There have been other BP implementations explored, but this ones don't take into account the fact the use of chirp signals, meaning they skip the IFFT and FFTSHIFT part, this implementations simply take the first equation of backprojection and run them for every pulse, for each pixel, therefore getting O(n³). Since my approach is going to be with the fftshift and IFFT we get a more complex algorithm.
#### BackProjection in FPGA
*Referir de um  modo geral como são feitas as implementações na FPGA seja por HLS, ou uma implementação em vivado* 

There have been multiple implementations of the BackProjection Algorithm in FPGA devices, namely the AMD one (referir o paper da AMD), and they have left a lot of room for improvement, more on that later.
Since the goal of this work is to implement the new AI Engines that are powerful devices for accelerating basic operations (fazer mais pesquisa aqui e comentar bastante os AI engines). They also have a mode for DSP, meaning we can use them for Digital Signal Processing. With this we can conclude that the main goal is to use this AI Engines to Accelerate the maximum we can, and compare with an HLS implementation or even with the DSP Engines 


Copiar um bocado/ Ir buscar cenas que estão no paper/PIC2 da Helena.
#### Conclusions

## Preliminary work
Primeiro comecei por compreender o algoritmo, como funciona, o que são os seus inputs, outputs e depois como é originada a imagem. Para isto fui pesquisar várias implementações do algoritmo, de entre várias a mais citada é sempre a do Gorham... e portanto decidi basear a minha própria implementação do algoritmo nesta, em C uma vez que esta está feita em MatLab. Para isto usei o Gotcha como inputs de dados de SAR para processar, estando em ficheiros de binários MatLab, pensei em duas hipóteses ou ler os dados, de MatLab dentro da minha própria implementação ou converter os dados para ficheiros de binário normais.  
## Work Proposal


