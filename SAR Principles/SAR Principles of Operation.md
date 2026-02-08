SAR é uma plataforma de movimento, seja uma aeronave, satélite, drone, avião etc. que tem uma antena instalada e que envia pulsos eletromagnéticos, mais em concreto [[Chirp Signals]].

Agora temos que receber os pulsos, que sofrem alterações por causa do terreno. Então temos um [[Listening Time]], que é o tempo que a antena ouve os ecos do sinal.  
![[Pasted image 20260209015543.png]]

Sendo uma plataforma de movimento em 3 dimensões e não tendo um sítio de partida definido temos que definir estas "variáveis" todas:
- Azimuth --> É a direção de movimento (basicamente para a frente e para trás)
- Slant Range --> distância da posição inicial ao chão
- Ground Range --> é a distancia do chão ao eixo x?
- Swath Width --> largura do que o nosso Radar consegue ver

Em relação ao movimento assume-se velocidade constante, e a posição, relativa ao chão e com eixos criados.
- $(x,y,z) = (x_0,0,\Delta h)$ --> posição inicial do radar 
- $r(t) = \sqrt{r_{0}^2 + (vt)²} \approx r_0 + \frac{(vt)²}{2r_0}, \frac{vt}{r_0} << 1$ --> aproximação da posição do radar em relação ao chão #duvidas  