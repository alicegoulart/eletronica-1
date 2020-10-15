# Instituto Federal de Santa Catarina - Campus Florianópolis Departamento Acadêmico de Eletrônica Curso de Engenharia Eletrônica

Alunos:

* Alice Goulart de Oliveira
* Giovanna Liz Souza


## Objetivos
Integração dos blocos de uma fonte linear.

## Introdução
Neste roteiro iremos integrar os circuitos estudados anteriormente, para isso, revise os conceitos de reguladores LDO e tenha em mãos os roteiros anteriores.

### Parte 01

#### Considerando o circuito da figura 01 que representa uma fonte linear com regulador MOSFET, temos o seguinte problema: Qual relação entre a tensão de alimentação do ampop e a tensão de saída? O que devemos considerar para esse circuito operar como um LDO? Como obter as tensões de alimentação para o AmpOp (VCC e VEE)?

![primeiro bloco](/Imagens/parte5/figura1.JPG)

![primeiro bloco](/Imagens/logo.png)
##### Figura 1.

#### Circuito proposto (01) para a alimentação do AmpOp:

(colocar link da figura)
##### Figura 2.

####Utilizando o circuito dobrador de tensão, qual valor de VCC você obtém para um sinal Vin+ de 12Vrms? Quais problemas apresentam esse circuito? Podemos melhorar?

#### Circuito proposto (02) para a alimentação do AmpOp:

(colocar link da figura)
##### Figura 3.

#### Vamos projetar esse circuito?

Considere: AmpOp LM324, MOSFET IRF540, VOUT = 15V, IOUT = 1A, vin+ = 12Vrms, Vripple_pós_retificador = 1V, considere as quedas de tensão nos diodos de 0,7V.

Como é sabido, o ampop possui um limite de saturação, desta forma a tensão de saída do ampop está diretamente relacionada à tensão de alimentação. A tensão máxima de saída será um pouco menor que a tensão de alimentação  do ampop.

Se a intenção for que o circuito consiga operar como LDO, precisamos que a queda de tensão na saída seja baixa, como por exemplo entre 0,1V e 0,5 V. Além disto, a tensão de saída está diretamente ligada a tensão de referência e à relação dos resistores, ou seja :

Vou= Vref (1+ R1/R2)

Em relação ao ampop, precisamos extrair as características elétricas do DATASHEET, já para o amplificador LM324, a alimentação de ± 16V ou de 0 a 32Vcc. Para encontrar a tensão esperada foi utilizada a tipologia dobrador de tensão, desta forma a tensão será de:

VP= (2122^(½)) -(0,7) = 33,3 V

Para saber  qual tensão teremos para um sinal Vin+ de 12Vrms e utilizando o circuito dobrador, quais problemas tem o circuito e como podemos melhorá-lo precisamos inicialmente achar o capacitor para o circuito, considerando sua corrente de 0,5A apenas para alimentação dos ampop, além dos valores abaixo:

Vp=33, 3V   f= 60Hz   Vr= 10% de VP

(colocar link da figura)
##### Figura 4.

(colocar link da figura)
##### Figura 5.

É possível perceber que o valor obtido, Vr = 3,04 V, está um pouco abaixo do valor calculado, V r= 3,3 V. Desta forma, o circuito precisa ser melhorado para encontrar um valor de tensão mais constante, a fim de reduzir a tensão de ripper na entrada do ampop, já que este é o problema crucial.
	
Além disso, devemos ressaltar que a corrente de picos nos diodos, quando o circuito foi ligado, marca aproximadamente 15A, muito abaixo do valor do informado no DATASHEET do diodo, 30A. A importância disto se dá no caso de acontecer uma elevação excessiva dos capacitores, de forma com que a corrente de pico fique com um valor muito elevado, ficando sujeita a queima dos diodos.

(colocar link da figura)
##### Figura 6.

(colocar link da figura)
##### Figura 7.

Circuito Indicado (02) para a alimentação do Ampop:

(colocar link da figura)
##### Figura 8.

(colocar link da figura)
##### Figura 9.

Pode-se analisar que a tensão Vout tem um pequeno ripper na saída, cerca de 20uV. É  possível melhorar a alimentação do amplificador, incluindo um transistor com alto ganho e pequeno capacitor, deixando a tensão com ripper menor, incluir também um potenciômetro paralelamente com o D6, a fim de regular a fonte de 0 a 27V.

Também conseguimos esta melhora adicionando os capacitores, C2 e C3, com valor maior no dobrador de tensão, isto fará com que diminua o ripper notavelmente. Porém, com os valores aumentando gradativamente, o tempo para entrar em regime permanente aumenta do mesmo modo, ficando excessivamente alto.

### Parte 02

#### Calculando e dimensionando os componentes

a) Para o primeiro bloco (D1, D2 e C1) considere vin+ = 12Vrms, vripple_pós_retificador = 1V e I_carga  =  1,1A. (Vide roteiro 02)

b) Circuito referência de tensão zener (R1 e D3): Ver roteiro 03. Podemos melhorar esse circuito? Quais problemas podemos identificar nesta topologia?
Sugestão de melhoria:

(colocar link da figura)
##### Figura 10.

No qual o circuito com R1, R5, Q2 e Q3 é uma fonte de corrente constante para polarizar o diodo zener D3. Vamos projetar? 

(colocar link da figura)
##### Figura 11.

#### Podemos melhorar mais ainda? Que tal deixar essa fonte com valor ajustável? Como fazer isso?


c) Escolhendo o transistor M1 e calculando R2 e R3.

(colocar link da figura)
##### Figura 12.

(colocar link da figura)
##### Figura 13.

(colocar link da figura)
##### Figura 14.

Foi utilizado um Transistor 2AS1774.

(colocar link da figura)
##### Figura 15.

#### Adicionando um Resistor de 15 Ohm pra 1A.

(colocar link da figura)
##### Figura 16.

É possível fazer a verificação da corrente de saída, confirmando que ela é próxima a 1A e Vr cerca de 7,5 uV, analisando que a tensão RMS teve uma alteração quase nula com a inclusão de carga.

Os problemas cruciais da fonte de corrente do circuito são depender do hfe e das diferenças, pequenas, das características dos transistores, onde pode ter uma pequena alteração de tensão VCE.

Podemos melhorar o circuito usando um potenciômetro paralelamente com o diodo D3, permitindo um controle maior sobre a tensão de saída.

## Parte 03

#### Adicionando um circuito de proteção de sobre corrente ao regulador linear.

Primeiramente reflita e pesquise sobre o que é sobrecorrente? Quais os impactos neste circuito? O que deve fazer um circuito de proteção de sobrecorrente? O que é a proteção foldback?

Pesquise as topologias disponíveis, caso deseja-se fazer um circuito LDO,  o que devemos levar em consideração para o regulador?

Exemplo de circuito: (Vide roteiro 01) 

Segundo  o site GMaster Treinamentos sobrecorrente é a corrente elétrica onde valor ultrapassa o valor nominal suportável. Para condutores, o valor nominal é a capacidade máxima de condução de um valor de corrente medido em amperes. 

(colocar link da figura)
##### Figura 17.

A sobrecorrente neste circuito acarretará em queima de componentes, com possibilidade de ser transistores, diodos, resistores, transformador, já que foi feito para suportar um limite máximo de 2A, neste caso. Porém com a proteção de sobrecorrente, através de um circuito para proteção da fonte,  dificulta a queima. No caso de acontecer um curto circuito na saída da fonte ou até aumento na carga, a proteção feita diminuirá a tensão de saída, a fim de que não tenham falhas.

Um circuito de proteção de sobrecorrente precisa conseguir  atuar no momento que a corrente de saída é maior que a projetada para o circuito, sendo esta por curto circuito ou sobrecarga. Neste projeto em específico, a fonte foi planejada para 15W e 1 A, o limite é quando a corrente extrapola 1,2A. 

Segundo o site QA Stack  o foldback é um método usado em fontes de alimentação para protegê-las de situações atuais, como curto-circuito na saída com um fio ou conexão de muitos equipamentos à fonte de alimentação.Caso o intuito seja fazer um circuito LDO, devemos levar em consideração alguns fatores como colocar um capacitor de saída, projetar o circuito pensando na temperatura máxima dos componentes, colocar medidas de proteção como por exemplo um limitador de corrente.

### Referências

https://gmastertreinamentos.com/dicionario-de-eletrica-e-automacao/o-que-e-sobrecorrente/  
https://qastack.com.br/electronics/2931/what-is-foldback-short-circuit-protection-in-a-power-supply 

