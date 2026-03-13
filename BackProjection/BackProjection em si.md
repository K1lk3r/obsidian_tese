
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
- dR -> Range bin resolution (o que é isto na prática)
- dxdy -> Image pixel spacing (same o que é isto na prática)
- z0 -> É zero serve para calcular o Z_diff que depois serve para calcular o R 
#### Parâmetros calculados
- R -> range da plataforma do pixel que estamos a tratar
- Bin --> não sei bem o que é


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
3. Calculo do R e do Bin
	- Começamos por calcular xdiff, ydiff, zdiff 
	- E depois o R
~~~C
	const double xdiff = platpos[p].x - px;
	const double ydiff = platpos[p].y - py;
	const double zdiff = platpos[p].z - z0;
	const double R = sqrt(
		xdiff*xdiff + ydiff*ydiff + zdiff*zdiff);
	/* convert to a range bin index */
	const double bin = (R-R0)*dR_inv;
~~~
4.  Condição do bin
	- Depois de calcular o R e o bin temos a condição
	- temos de verificar se o bin é maior que 0 e menor que N_RANGE_UPSAMPLED-2
~~~ C
	if (bin >= 0 && bin <= N_RANGE_UPSAMPLED-2)
~~~
5. Soma ponderada para os valores dos pixeis
	- Então agora começamos por fazer as contas a sério
	- calculamos o bin_floor (para aceder ao vetor por inteiro e não com float/double)
	- calculamos o w que é no fundo o que faz disto uma soma ponderada
	- Calculamos a sample interpolada de cada pulso (base do expoente complexo)
	- o match filter (o expoente do valor complexo)
	- que depois é somado no accum
~~~ C
		complex sample, matched_filter, prod;
		/* interpolation range is [bin_floor, bin_floor+1] */
		const int bin_floor = (int) bin;
		/* interpolation weight */
		const float w = (float) (bin - (double) bin_floor);
		/* linearly interpolate to obtain a sample at bin */
		sample.re = (1.0f-w)*data[p][bin_floor].re + w*data[p][bin_floor+1].re;
		sample.im = (1.0f-w)*data[p][bin_floor].im + w*data[p][bin_floor+1].im;
		/* compute the complex exponential for the matched filter */
		matched_filter.re = cos(2.0 * ku * R);
		matched_filter.im = sin(2.0 * ku * R);
		/* scale the interpolated sample by the matched filter */
		prod = cmult(sample, matched_filter);
		/* accumulate this pulse's contribution into the pixel */
		accum.re += prod.re;
		accum.im += prod.im;
~~~