
Por passos o que o algoritmo faz?

## Step by step -- Paper/Math view

Começamos com $N_p$ pulsos -- **onde é que está representado no código** -- 


## Step by Step -- Código C/Matlab

### Parâmetros
#### Argumentos de entrada
- Image -> 2D array de complexos com tamanho BP_NPIX_Y x BP_NPIX_Y
- data    ->  É um array de tamanho N_RANGE_UPSAMPLED, é um array de complexos
	 o array em si é constante (ou seja ele existe sempre e não muda de sítio (se calhar um pouco irrelevante para o nosso caso mas seguimos em frente)) mas dá para alterar os seus valores.
- platpos -> array de posições com tamanho N_PULSES. Tem 3 elementos (x,y,z).
- ku -> uma constante de valor $2.0 \times M\_PI \times fc /Speed\_of\_light$ em que 
	- $M\_PI$ -> é o $\pi$ 
	- $fc$ -> é a carrier frequency
	- Speed of light (clown emoji)
- dR -> Range bin resolution
- dxdy -> Image pixel spacing
- z0 -> É zero serve para calcular o Z_diff que depois serve para calcular o R 
#### Parâmetros calculados
- R -> range da plataforma do pixel que estamos a tratar

## O que o Algoritmo faz
- Dois loops encadeados em $y$ e $x$ , ou seja percorremos os pixeis da imagem que queremos produzir
- Declaramos a variável *accum*  e calculamos $px = (- BP\_NPIX\_X / 2.0 + 5.0 + ix) * dxdy$ 
	- Em que BP_NPIX_X é o número de pixeis da largura da imagem a ser formada
	- ix é o iterador em X que vai até 1024 definido pelo programa e que temos de obter esta informação a partir dos dados dos pulsos (i guess)
	- dxdy Image pixel spacing
	- accum é do tipo complexo (incializado a zero as duas componentes)
1. Loop dos pixeis 
	- o valor do pixel está em complexo 
	- Em cada pixel da imagem percorremos o número total de pulsos para calcular o valor do pixel
	- Neste caso (medium size) a imagem é de 1024 x 1024
	- E calculamos py e px, para cada iteração, respetivamente
~~~ C
for (iy = 0; iy < BP_NPIX_Y; ++iy)
	py = (-BP_NPIX_Y/2.0 + 5.0 + iy) * dxdy
	for (ix = 0; ix < BP_NPIX_X; ++ix) 
		px = (-BP_NPIX_X/2.0 + 5.0 + ix) * dxdy
~~~
2. Loop dos pulsos
	- Em cada pixel percorremos os pulsos capturados
	- Inicializamos accum a zeros
~~~C
accum = 0; // accum é um valor complexo
for (p = 0; p < N_PULSES; ++p)
~~~ 
3. Calculo do R
	- Começamos por calcular xdiff, ydiff, zdiff 
	- E depois o R
~~~C

~~~