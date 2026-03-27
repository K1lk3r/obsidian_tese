## PS (processing system)

Aqui sei que existem 3 modulos principais APU  o processador normal RPU o real time processador e PMC acho que é a programming manager and controller 
###### APU
###### RPU
###### PMC

## PL (programming logic)
Falar só um pouco dos valores de BRAM LUT's DSP's, se bem que não sei bem o que tem de DSP porque existem DSP's engines na placa também.
## AI Engines
Os AI engines são compostos por uma rede de AI Tiles em que cada Tile tem uma memória própria e estão ligadas com as dos Tiles adjacentes com uma pequena nuance em que a memória estiver à esquerda do Tile esta não está ligada com a Memória à direita (com uma imagem fica mais claro).  

Os AI Tiles são simplesmente processadores com vários blocos de processamento que se especializam em AI, corre a 1 GHz e é um chip que usa um ISA, ou seja é um processador que usa instruções como um processador normal.

Estes AI Tiles permitem operações com scalar e com vetores tendo a opção de se fazer as operações com floating ou fixed point. Tendo em conta que existem blocos específicos para cada tipo de operação o (**REVER OS BLOCOS E DESCREVE-LOS**)

As memorias dos tiles estão conetadas em rede adjacentemente, no entanto também tem uma conexão por AXI-Stream, em que um tile tenha feito um processamento e quer passar a outro que está no outro lado do engine, eles podem partilhar esses dados a partir do AXI-Stream, em que os dados são partilhados por stream (broadcast). 

## NoC (Network on Chip)
Isto é o que permite estes sistemas todos comunicarem entre si, e com o IO. (I think)