---
title: "Tarefa sobre Inferencia Estatística"
author: "Design by Brian Caffo - Instrutor David Prata - UFT " 
subtitle: (Use setas para navegar)
output:
  html_document:
    df_print: paged
  pdf_document: default
  word_document: default
framework: io2012
highlighter: highlight.js
hitheme: tomorrow
widgets:
- mathjax
- quiz
- bootstrap
mode: selfcontained
job: David
---


## Sobre esses slides
- Estes são alguns problemas práticos para o Questionário de Inferência Estatística 1
- Eles foram criados usando slidify interativo que você aprenderá Criar produtos de dados


--- &radio

Considere epidemias de gripe para famílias heterossexuais com dois pais. Suponha que a probabilidade seja de 15% de que pelo menos um dos pais tenha contraído a doença. A probabilidade de que o pai tenha contraído a gripe é de 10% enquanto que a mãe contraiu a doença é de 9%. Qual é a probabilidade de que ambos contraia gripe como a porcentagem de um número inteiro?
[veja uma solução no vídeo](https://www.youtube.com/watch?v=CvnmoCuIN08&index=1&list=PLpl-gQkQivXhHOcVeU3bSJg78zaDYbP9L)

1. 15%
2. 10%
3. 9%
4. _4%_

*** .hint
$A = Father$, $P(A) = .10$, $B = Mother$, $P(B) = .09$
$P(A\cup B) = .15$,

*** .explanation
$P(A\cup B) = P(A) + P(B) - P(AB)$ thus
$$.15 = .10 + .09 - P(AB)$$

```r
.10 + .09 - .15
```

```
[1] 0.04
```

---  &radio

Uma variável aleatória, $X$, é uniforme, uma caixa de $0$ a $1$ de altura $1$. (Para que sua densidade seja $f(x) = 1$ para $0\leq x \leq 1$.) Qual é sua mediana expressa com duas casas decimais?
[Veja a solução no vídeo](https://www.youtube.com/watch?v=UXcarD-1xAM&index=2&list=PLpl-gQkQivXhHOcVeU3bSJg78zaDYbP9L)</p>

1. 1.00
2. 0.75
3. _0.50_
4. 0.25

*** .hint
A mediana é o ponto em que 50% da densidade fica abaixo dela.

*** .explanation
Esta densidade parece uma caixa. Então, observe que $P(X \leq x) = largura\vezes altura = x$.
Queremos $.5 = P(X\leq x) = x$.

--- &radio

Você está jogando um jogo com um amigo onde você joga uma moeda e se der cara você dá a ela $ X$ dólares e se der coroa ela te dá $Y$ dólares. A probabilidade de a moeda sair cara é $d$. Qual é o seu rendimento esperado? [Assista a uma solução em vídeo.](https://www.youtube.com/watch?v=5J88Zq0q81o&list=PLpl-gQkQivXhHOcVeU3bSJg78zaDYbP9L&index=3)

1. _$-X \frac{d}{1 + d} + Y \frac{1}{1+d} $_
2. $X \frac{d}{1 + d} + Y \frac{1}{1+d} $
3. $X \frac{d}{1 + d} - Y \frac{1}{1+d} $
4. $-X \frac{d}{1 + d} - Y \frac{1}{1+d} $

*** .hint
As chances que você perde em uma determinada rodada são dadas por $p / (1 - p) = d$ o que implica
onde $p = d / (1 + d)$.

*** .explanation
Você perde $X$ com probabilidade $p = d/(1 +d)$ e ganha $Y$ com probabilidade $1-p = 1/(1 + d)$. Então sua resposta é 
$$
-X \frac{d}{1 + d} + Y \frac{1}{1+d}
$$

--- &radio
Uma variável aleatória assume o valor -4 com probabilidade 0,2 e 1 com probabilidade 0,8. O que
é a variância desta variável aleatória? [Veja a solução no vídeo.](https://www.youtube.com/watch?v=Em-xJeQO1rc&index=4&list=PLpl-gQkQivXhHOcVeU3bSJg78zaDYbP9L)

1. 0
2. _4_
3. 8
4. 16

*** .hint
This random variable has mean 0. The variance would be given by $E[X^2]$ then.

*** .explanation
$$E[X] = 0$$
$$
Var(X) = E[X^2] = (-4)^2 * .2 + (1)^2 * .8
$$

```r
-4 * .2 + 1 * .8
```

```
[1] 0
```

```r
(-4)^2 * .2 + (1)^2 * .8
```

```
[1] 4
```


--- &radio
Se $\bar X$ e $\bar Y$ são compostos por $n$ iid variáveis ​​aleatórias decorrentes de distribuições
tendo significa $\mu_x$ e $\mu_y$, respectivamente e variância comum $\sigma^2$
qual é a variância $\bar X - \bar Y$? [Assista a um vídeo da solução deste problema.](https://www.youtube.com/watch?v=7zJhPzX6jns&list=PLpl-gQkQivXhHOcVeU3bSJg78zaDYbP9L&index=5)

1. 0
2. _$2\sigma^2/n$_
3. $\mu_x - \mu_y$
4. $2\sigma^2$

*** .hint
Remember that $Var(\bar X) = Var(\bar Y) = \sigma^2 / n$.

*** .explanation
$$
Var(\bar X - \bar Y) = Var(\bar X) + Var(\bar Y) = \sigma^2 / n + \sigma^2 / n
$$

--- &radio
Seja $X$ uma variável aleatória com desvio padrão $\sigma$. O que pode
ser dito sobre $X /\sigma$? [Assista a um vídeo da solução deste problema.](https://www.youtube.com/watch?v=0WUj18_BUPA&list=PLpl-gQkQivXhHOcVeU3bSJg78zaDYbP9L&index=6)

1. Nothing
2. _It must have variance 1._
3. It must have mean 0.
4. It must have variance 0.

*** .hint
$Var(aX) = a^2 Var(X)$

*** .explanation
$$Var(X / \sigma) = Var(X) / \sigma^2 = 1$$


--- &radio
Se uma densidade contínua que nunca toca o eixo horizontal é simétrica em relação a zero, podemos dizer que sua mediana associada é zero? [Assista a uma solução em vídeo.](https://www.youtube.com/watch?v=sn48CGH_TXI&list=PLpl-gQkQivXhHOcVeU3bSJg78zaDYbP9L&index=7)

1. _Yes_
2. No.
3. It can not be determined given the information given.

*** .explanation
Este é um problema surpreendentemente difícil. A explicação fácil é que 50% da probabilidade
está abaixo de 0 e 50% está acima, então sim. No entanto, é baseado na densidade não sendo
uma linha plana em 0 em torno de 0. É por isso que a ressalva de que ela nunca toca o eixo horizontal
é importante.


--- &radio

Considere a seguinte pmf dada em R

```r
p <- c(.1, .2, .3, .4)
x <- 2 : 5
```
Qual é a variância expressa com 1 casa decimal? [Assista a uma solução para este problema.](https://www.youtube.com/watch?v=sn48CGH_TXI&list=PLpl-gQkQivXhHOcVeU3bSJg78zaDYbP9L&index=7)

1. _1.0_
2. 4.0
3. 6.0
4. 17.0

*** .hint
A variância é $E[X^2] - E[X]^2$

*** .explanation

```r
sum(x ^ 2 * p) - sum(x * p) ^ 2
```

```
[1] 1
```
