---
title: "Tarefa 4 sobre Inferencia Estatística"
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


## Sobre esses  slides
- Alguns problemas práticos de Inferência Estatística


--- &multitext
Carregue o conjunto de dados `mtcars` no pacote R `datasets`. Suponha que o conjunto de dados mtcars seja uma amostra aleatória. Calcule o MPG médio, $\bar x,$ desta amostra.

Você quer testar se o verdadeiro MPG é $\mu_0$ ou menor usando um
teste de nível de 5%. ($H_0 : \mu = \mu_0$ versus $H_a : \mu < \mu_0$).
Usando esse conjunto de dados e um teste Z:

1. . Com base no MPG médio da amostra $\bar x,$ e usando um teste Z: qual é o menor valor de $\mu_0$ que você rejeitaria (até duas casas decimais)?

*** .hint
Esta é uma inversão de um teste de hipótese unilateral. Ele produz limites confiança
. (Observe que a inversão de um teste de duas caudas produz intervalos de confiança.)
Pense na derivação do intervalo de confiança.

*** .explanation
queremos resolver
$$
\frac{\sqrt{n}(\bar{X} - \mu_0)}{s} = Z_{0.05}
$$
Ou $$\mu_0 = \bar{X} - Z_{0.05} s / \sqrt{n} = \bar{X} + Z_{0.95} s / \sqrt{n}$$ Note que o quantil é negativo.


```r
mn <- mean(mtcars$mpg)
s <- sd(mtcars$mpg)
z <- qnorm(.05)
mu0 <- mn - z * s / sqrt(nrow(mtcars))
```
Observe que é fácil tropeçar nesse problema com os sinais. Se você receber um valor menor que $\bar X$, então claramente está errado, já que você nunca rejeitaria por
$H_0:\mu = \mu_0$ versus $H_a : \mu < \mu_0$ se $\mu_0$ sendo menor que sua média observada.
Observe também que a resposta para "Qual é o maior valor para o qual você rejeitaria?" é
infinita.

<span class="answer">21.84</span<>


--- &multitext
Considere novamente o conjunto de dados `mtcars`. Use um teste t de dois grupos para testar
a hipótese de que os carros de 4 e 6 cilindradas têm o mesmo mpg. Usar
um teste bilateral com variâncias desiguais.

1. Você rejeita no nível de 5% (digite 0 para não, 1 para sim).
2. Qual é o valor P com 4 casas decimais expresso em proporção?


*** .hint
Use `t.test` com as opções `var.equal=FALSE`, `paired=FALSE`, `altnernative` como `two.sided`.

*** .explanation


```r
m4 <- mtcars$mpg[mtcars$cyl == 4]
m6 <- mtcars$mpg[mtcars$cyl == 6]
p <- t.test(m4, m6, paired = FALSE, alternative="two.sided", var.equal=FALSE)$p.value
```
A resposta para 1. é <span class="answer">1</span> <br>
A resposta para 2. é <span class="answer">4e-04</span>


--- &multitext
Uma amostra de 100 homens produziu um nível médio de PSA de 3,0 com um dp de 1,1. Qual é o conjunto completo de valores que um teste Z bilateral de 5% de $H_0 : \mu = \mu_0$
falharia em rejeitar a hipótese nula?

1. Insira o valor mais baixo com 2 casas decimais.
2. Insira o valor superior com 2 casas decimais.

*** .hint
Isso é equivalente ao intervalo de confiança.

*** .explanation
A resposta para  1 é
 <span class="answer">2.78</span><br>
A resposta para to 2 é <span class="answer">3.22</span>


--- &multitext
Você acredita que a moeda que está jogando é tendenciosa para a cara. Você obtém 55 caras de 100 viradas.

1. Qual é o valor de p relevante exato com 4 casas decimais (expresso como proporção)?
2. Você rejeitaria uma hipótese unilateral em $\alpha = .05$? (0 para não 1 para sim)?

*** .hint
Use `pbinom` para uma hipótese de que $p=.5$ veruss $p>.5$ onde $p$ é a probabilidade de sucesso binomial.

*** .explanation
Observe que você deve começar em 54, pois `lower.tail = FALSE` fornece estritamente o maior valor do que
probabilidades

```r
ans <- round(pbinom(54, prob = .5, size = 100, lower.tail = FALSE),4)
```
A resposta para 1 é <span class="answer">0.1841</span><br>
A resposta para 2 é <span class="answer">0</span><br>


--- &multitext

Um site web foi monitorado por um ano e recebeu 520 acessos por dia. Nos primeiros
30 dias do ano seguinte, o site recebeu 15.800 acessos. Supondo que os acessos da web
são Poisson.

1. Dê um valor P unilateral exato para a hipótese de que os acessos na web aumentaram este ano em relação ao ano passado com
quatro algarismos significativos (expresso como uma proporção).
2. O teste unilateral rejeita (0 para não 1 para sim)?


*** .hint
Considere usar `ppois` com $\lambda=520 * 30$. Observe que isso é quase exatamente gaussiano, de forma que você possa escapar do cálculo gaussiano.

*** .explanation
Este teste vem com a importante suposição de que os hits da web são um processo de Poisson.


```r
pv <- ppois(15800 - 1, lambda = 520 * 30, lower.tail = FALSE)
```

A resposta para 1 é <span class="answer">0.0553</span><br>
A resposta para 2 é <span class="answer">0</span><br>

Além disso, compare com a aproximação gaussiana onde $\hat \lambda  \sim N(\lambda, \lambda / t)$

```r
pnorm(15800 / 30, mean = 520, sd = sqrt(520 / 30), lower.tail = FALSE)
```

```
[1] 0.05465729
```
Enquanto $t\rightarrow \infty$ isso se torna mais gaussiano. A aproximação é muito boa para esse contexto.


--- &multitext

Suponha que em um teste AB, um esquema de publicidade tenha levado a uma média de 10 compras por dia para uma amostra de 100 dias, enquanto o outro levou a 11 compras por dia, também para uma amostra de 100 dias.
Assumindo um desvio padrão comum de 4 compras por dia.
Assumindo que os grupos são independentes e que os dias são iid, faça um teste Z de
equivalência.

1. Qual é o valor-P informado com 3 dígitos expresso em proporção?
2. Você rejeita o teste? (0 para não 1 para sim).

*** .hint
O erro padrão é 
$$
s \sqrt{\frac{1}{n_1} + \frac{1}{n_2}}
$$

*** .explanation

```r
m1 <- 10; m2 <- 11
n1 <- n2 <- 100
s <- 4
se <- s * sqrt(1 / n1 + 1 / n2)
ts <- (m2 - m1) / se
pv <- 2 * pnorm(-abs(ts))
```

A resposta para 1 é <span class="answer">0.077</span><br>
A resposta para 2 é <span class="answer">0</span>


--- &radio

Um intervalo de confiança para a média contém:

1. _Todos os valores da média hipotética para os quais falharíamos em rejeitar com
$\alpha = 1 - Conf. Nível$._
2. Todos os valores da média hipotética para os quais falharíamos em rejeitar com
$2 \alpha = 1 - Conf. Nível$.
3. Todos os valores da média hipotética para os quais rejeitaríamos com
$\alpha = 1 - Conf. Nível$.
4. Todos os valores da média hipotética para os quais rejeitaríamos com
$2 \alpha = 1 - Conf. Nível$.

*** .hint
Isto vem diretamente das notas. Observe que um intervalo de confiança fornece
valores de $\mu$ que são suportados pelos dados enquanto um teste rejeita
para valores de $\mu$ diferentes de $\mu_0$. 

*** .explanation
A única parte complicada disso é o 2. Observe que um intervalo de 95% corresponde
para um teste bilateral de nível de 5%. Então isso é $\alpha = 1 - Conf.Level$. A confusão é que
tanto para o teste bilateral quanto para o intervalo de confiança, é preciso calcular
$Z_{1 - \alpha / 2}$ (ou o quantil T relevante).


--- &multitext
Considere os dois problemas anteriores. Supondo que 10 compras por dia seja um valor nulo de referência,
que os dias são iid e que o desvio padrão é de 4 compras por dia. Suponha que você
planeje uma amostragem de 100 dias. Qual seria a potência para um 5% unilateral de
Teste Z de significância sendo que as compras por dia
aumentariam sob a alternativa de $\mu = 11$ de compra por dia?


1. Dê seu resultado com proporção de 3 casas decimais.

*** .hint
Sob $H_0$ $\bar X \sim N(10, .4)$. Sob $H_a$ $\bar X \sim N(11, .4)$. rejeitamos quando $\bar X \geq 10 + Z_{.95} .4$.


*** .explanation
A dica praticamente entrega.

```r
power <- pnorm(10 + qnorm(.95) * .4, mean = 11, sd = .4, lower.tail = FALSE)
```
A resposta é <span class="answer">0.804</span>


--- &multitext
Os pesquisadores gostariam de realizar um estudo de adultos saudáveis ​​para detectar uma perda média de volume cerebral de quatro anos de 0,01 mm3. Suponha que o desvio padrão da perda de volume de quatro anos nesta população seja de 0,04 mm3.

1. Qual é o tamanho de amostra necessário para o estudo para um teste unilateral de 5% versus uma hipótese nula de nenhuma perda de volume para atingir 80% de potência? (Sempre arredondar para cima)



*** .hint
Sob $H_0$ $\bar X$ is $N(0, .05 / \sqrt{n})$ e é $N(.01, .05 / \sqrt{n})$ under $H_a$. 
rejeitamos se 
$$
\bar X \geq  Z_{.95} s / sqrt{n}
$$ 
que tem probabilidade 0,05 abaixo de $H_0$. Sob $H_a$ tem probabilidade
$$
P\left( \frac{\bar X - 0.01}{s / \sqrt{n}} \geq  \frac{.01}{s / \sqrt{n}} + z_{.95} \right)
= P\left( Z \geq \frac{.01}{s / \sqrt{n}} + z_{.95}\right)
$$

*** .explanation
Olhando para a dica definimos
$$
\frac{.01}{s / \sqrt{n}} + z_{.95} = z_{.2}
$$
$$
n = \frac{(z_{.95} - z_{.2})^2 s^2}{.01^2} = \frac{ (z_{.95} + z_{.8})^2 s^2}{.01^2}
$$
So we get

```r
n <- (qnorm(.95) + qnorm(.8)) ^ 2 * .04 ^ 2 / .01^2
```
A resposta é <span class="answer">99</span>


--- &radio

Em um tribunal de justiça, sendo todas as coisas iguais, se por meio de apólice você exigir um
padrão de evidência para condenar as pessoas então

1. Pessoas menos culpadas serão condenadas.
2. _Mais inocentes serão condenados._
3. Mais inocentes não serão condenados.


*** .hint
Pense sobre isto.

*** .explanation
Se você precisar de menos provas para condenar, então você condenará mais pessoas, culpadas e
inocentes. Relacione essa propriedade de volta aos testes de hipóteses.


--- &multitext
Considere o conjunto de dados `mtcars`.

1. Dê o valor p para um teste t comparando MPG para carros de 6 e 8 cilindros assumindo variância igual, com proporção de 3 casas decimais.
2. Dê o valor P associado para um teste z.
3. Dê a estimativa de desvio padrão comum (agrupado) para MPG entre cilindros com 3 casas decimais.
4. O teste t rejeitaria no nível 0,05 bilateral (0 para não 1 para sim)?


*** .hint

```r
mpg8 <- mtcars$mpg[mtcars$cyl == 8]
mpg6 <- mtcars$mpg[mtcars$cyl == 6]
m8 <- mean(mpg8); m6 <- mean(mpg6)
s8 <- sd(mpg8); s6 <- sd(mpg6)
n8 <- length(mpg8); n6 <- length(mpg6)
```

*** .explanation

```r
p <- t.test(mpg8, mpg6, paired = FALSE, alternative="two.sided", var.equal=TRUE)$p.value
mixprob <- (n8 - 1) / (n8 + n6 - 2)
s <- sqrt(mixprob * s8 ^ 2  +  (1 - mixprob) * s6 ^ 2)
z <- (m8 - m6) / (s * sqrt(1 / n8 + 1 / n6))
pz <- 2 * pnorm(-abs(z))
## Hand calculating the T just to check
#2 * pt(-abs(z), df = n8 + n6 - 2)
```

1. <span class="answer">0</span> <br>
2. <span class="answer">0</span><br>
3. <span class="answer">2.27</span><br>
4. <span class="answer">1</span>


--- &radio
A correção Bonferonni controla isso

1. Taxa de descoberta falsa
2. _A taxa de erro familiar_
3. A taxa de rejeições verdadeiras
4. O número de rejeições verdadeiras

*** .hint
Isso é praticamente direto das notas

*** .explanation
A correção de Bonferonni é a correção clássica para a taxa de erro familiar.
