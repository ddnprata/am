---
title       : Trabalho 2 para Estatística Inferencial
subtitle    : 
author      : Design by Brian Caffo
job         : Professor David Prata - UFT
framework   : io2012
highlighter : highlight.js  
hitheme     : tomorrow       
#url:
#    lib: ../../librariesNew #Remove new if using old slidify
#    assets: ../../assets
widgets     : [mathjax, quiz, bootstrap]
mode        : selfcontained # {standalone, draft}
---


## Sobre esses slides
- Estes são alguns problemas práticos para o Questionário de Inferência Estatística 1



--- &radio
A probabilidade de um manuscrito ser aceito em um periódico é de 12% (digamos). No entanto,
dado que uma revisão é solicitada, a probabilidade de que ela seja aceita
é 90%. É possível que a probabilidade de um manuscrito ter um pedido de revisão
seja de 20%?

1. Sim, isso é totalmente possível.
2. _Não, não é possível._
3. Não é possível responder a esta pergunta.

*** .hint
$A = accepted$, $B = revision$. $P(A) = .12$, $P(A | B) = .90$. $P(B) = .20$

*** .explanation
$P(A \cap B) = P(A | B) * P(B) = .9 \times .2 = .18$ isso é maior que
$P(A) = .12$, o que não é possível porque $A \cap B \subset A$.


--- &radio
Suponha que o número de acessos da Web a um determinado site seja aproximadamente normal distribuído com média de 100 acertos por dia e desvio padrão de 10 acertos por dia. Qual é a probabilidade de que um determinado dia tenha menos de 93 acertos por dia expressa como uma porcentagem para o ponto percentual mais próximo?

1. 76%
2. _24%_
3. 47%
4. 94%

*** .hint
Seja $X$ o número acessos por dia. queremos $P(X \leq 93)$ dado que
$X$ seja $N(100, 10^2)$.

*** .explanation

```r
round(pnorm(93, mean = 100, sd = 10) * 100)
```

```
[1] 24
```


--- &radio
Suponha que 5% dos projetos habitacionais tenham problemas com amianto. A sensibilidade de um teste
para amianto é de 93% e a especificidade é de 88%. Qual é a probabilidade de um
projeto habitacional não ter amianto dado um teste negativo expresso em porcentagem
para o ponto percentual mais próximo?

1. 0%
2. 5%
3. 10%
4. 20%
5. 50%
6. _100%_

*** .hint
$A = asbestos$, $T_+ = tests positive$, $T_- = tests negative$. 
$P(T_+ | A) = .93$, $P(T_- | A^c) = .88$, $P(A) = .05$.

*** .explanation
queremos
$$
P(A^c | T_-) = \frac{P(T_- | A^c) P(A^c)}{P(T_- | A^c) P(A^c) + P(T_- | A) P(A)}
$$

```r
(.88 * .95) / (.88 * .95 + .07 * .05)
```

```
[1] 0.9958309
```



---  &multitext
Suponha que o número de acessos da Web a um determinado site seja aproximadamente normal
distribuído com média de 100 acertos por dia e desvio padrão de 10 acertos por dia. 

1. O número de acessos da Web por dia representa o número para que apenas
5% dos dias tem mais acessos? Expresse sua resposta com 3 casas decimais.



*** .hint
Seja $X$ o número de acessos por dia. queremos $P(X \leq 93)$ dado que
$X$ é $N(100, 10^2)$.

*** .explanation
<span class="answer">116.449</span>

```r
round(qnorm(.95, mean = 100, sd = 10), 3)
```

```
[1] 116.449
```

```r
round(qnorm(.05, mean = 100, sd = 10, lower.tail = FALSE), 3)
```

```
[1] 116.449
```


---  &multitext
Suponha que o número de acessos da Web a um determinado site seja aproximadamente normal
distribuído com média de 100 acertos por dia e desvio padrão de 10 acertos por dia. Imagine tomar uma amostra aleatória de 50 dias. 

1. Qual seria o número de hits da web
para ser o ponto em que apenas 5% das médias de 50 dias de tráfego na web tenham mais acessos?
Expresse sua resposta com 3 casas decimais.

*** .hint
Seja $\bar X$ a média do número de hits por dia para 50 dias de amostras aleatórias.
$X$ é $N(100, 10^2 / 50)$.

*** .explanation
<span class="answer">102.326</span>
 

```r
round(qnorm(.95, mean = 100, sd = 10 / sqrt(50) ), 3)
```

```
[1] 102.326
```

```r
round(qnorm(.05, mean = 100, sd = 10 / sqrt(50), lower.tail = FALSE), 3)
```

```
[1] 102.326
```

--- &multitext

Você não acredita que seu amigo possa distinguir um bom vinho de um barato. Assumindo
que você está certo, em um teste cego onde você randomiza 6 variedades pareadas (Merlot,
Chianti, ...) de vinhos baratos e caros

1. qual é a mudança para obter 5 ou 6 certos expressos em porcentagem
de uma casa decimal?

*** .hint
Seja $p=.5$ e $X$ binomial

*** .explanation

<span class="answer">89.1</span>


```r
round(pbinom(4, prob = .5, size = 6, lower.tail = TRUE) * 100, 1)
```

```
[1] 89.1
```

--- &multitext

Considere uma distribuição uniforme. Se fôssemos amostrar 100 sorteios de um
uma distribuição uniforme (que tem média 0,5 e variância 1/12)
e pegar a sua média, $\bar X$

1. qual é a probabilidade aproximada de ficar tão grande quanto 0,51 ou maior expresso com 3 casas decimais?

*** .hint
Use o teorema do limite central que diz $\bar X \sim N(\mu, \sigma^2/n)$

*** .explanation

<span class="answer"> 0.365</span>


```r
round(pnorm(.51, mean = 0.5, sd = sqrt(1 / 12 / 100), lower.tail = FALSE), 3)
```

```
[1] 0.365
```


--- &multitext

Se você jogar dez dados padrão, tirar sua média, então repita este processo várias vezes e construa um histograma,

1. em que seria centrado?


*** .hint
$E[X_i] = E[\bar X]$ where $\bar X = \frac{1}{n}\sum_{i=1}^n X_i$

*** .explanation


A resposta será <span class="answer">3,5</span> uma vez que a média da
distribuição amostral dos sorteios do iid será a média populacional que o
sorteios individuais foram retirados.

--- &multitext

Se você jogar dez dados padrão, tirar sua média, então repita este processo várias vezes e construa um histograma,

1. qual seria sua variância expressa com 3 casas decimais?

*** .hint
$$Var(\bar X) = \sigma^2 /n$$

*** .explanation
A resposta será <span class="answer">0</span>
uma vez que a variância da distribuição amostral da média é $\sigma^2/12$
e a variância de uma jogada de dado é


```r
mean((1 : 6 - 3.5)^2)
```

```
[1] 2.916667
```

--- &multitext
O número de acessos da web a um site é Poisson com média de 16,5 por dia.

1. Qual é a probabilidade de obter 20 ou menos em 2 dias expressa
como uma porcentagem com uma casa decimal?

*** .hint
Seka $X$ o número de hits em 2 dias então $X \sim Poisson(2\lambda)$

*** .explanation
<span class="answer">1</span>


```r
round(ppois(20, lambda = 16.5 * 2) * 100, 1)
```

```
[1] 1
```


