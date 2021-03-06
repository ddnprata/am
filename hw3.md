---
title       : Trabalho 3 de Inferência Estatística
subtitle    : (Use the arrow keys to navigate)
author      : Design by Brian Caffo
job         : David Prata - UFT
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

- Estes são alguns problemas práticos para o Questionário de Inferência Estatística 3



--- &multitext
Carregue o conjunto de dados `mtcars` no pacote R `datasets`. Calcular um
Intervalo de confiança de 95% para o MPG mais próximo para a variável `mpg`.

1. Qual é o ponto final inferior do intervalo?
2. Qual é o ponto final superior do intervalo?

*** .hint
Faça `library(datasets)` e depois `data(mtcars)` para pegar os dados.
Considere `t.test` para os calculos. Você deve ter instalado o datasets package.


*** .explanation

```r
library(datasets); data(mtcars)
round(t.test(mtcars$mpg)$conf.int)
```

```
[1] 18 22
attr(,"conf.level")
[1] 0.95
```

<span class="answer">18</span>
<span class="answer">22</span>

--- &multitext
Suponha que o desvio padrão de 9 diferenças pareadas seja $ 1 $. Que valor teria que ser a diferença média para que o ponto final inferior de 95%
do intervalo de confiança t student chegue a zero?

1. Dê o número aqui com duas casas decimais

*** .hint
O intervalo t é $\bar x \pm t_{.975, 8} * s /\sqrt{n}$

*** .explanation
<span class="answer">0.77</span>

queremos $\bar x = t_{.975,8} * s / \sqrt{n}$

```r
round(qt(.975, df = 8) * 1 / 3, 2)
```

```
[1] 0.77
```


--- &radio
Um intervalo T de Student de grupo independente é usado em vez de
um intervalo T pareado quando:

1. As observações são pareadas entre os grupos.
2. _As observações entre os grupos são naturalmente consideradas estatisticamente independentes_
3. Contanto que você faça isso corretamente, qualquer uma está bem.
4. São necessários mais detalhes para responder a esta pergunta

*** .hint
Um intervalo pareado é para observações pareadas.

*** .explanation
Não podemos pareá-los se os grupos são independentes uns dos outros, bem como independentes entre si.


--- &multitext
Considere o conjunto de dados `mtcars`. Construa um intervalo T de 95% para MPG comparando
Carros de 4 a 6 cilindros (subtraindo na ordem de 4 - 6)
assumir uma variância constante.

1. Qual é o ponto final inferior do intervalo até 1 casa decimal?
2. Qual é o ponto final superior do intervalo até 1 casa decimal?

*** .hint
Use `t.test` com `var.equal=TRUE`

*** .explanation


```r
m4 <- mtcars$mpg[mtcars$cyl == 4]
m6 <- mtcars$mpg[mtcars$cyl == 6]
#this does 4 - 6
confint <- as.vector(t.test(m4, m6, var.equal = TRUE)$conf.int)
```

<span class="answer">3.2</span>
<span class="answer">10.7</span>


--- &radio
Se alguém apontasse uma arma para sua cabeça e dissesse "Seu intervalo de confiança
deve conter o que está estimando ou eu vou puxar o gatilho", qual
seria a coisa inteligente a fazer?

1. _Faça seu intervalo o mais amplo possível_
2. Faça o seu intervalo o menor possível
3. Ligue para as autoridades

*** .hint
oppsssss. Você não precisa de dica

*** .explanation
Este é apenas um exemplo do que acontece com os intervalos de confiança quando você
aumentar o nível de confiança. Você quer ter certeza em seu intervalo (ou seja,
tem um nível de confiança grande) e assim você aumentaria a largura do intervalo

--- &radio

Consulte a comparação de MPG para 4 versus 6 cilindros. O que você conclui?

1. O intervalo está acima de zero, sugerindo que 6 é melhor que 4 em termos de MPG
2. _O intervalo está acima de zero, sugerindo que 4 é melhor que 6 em termos de MPG_
3. O intervalo não diz nada sobre o teste de hipóteses; você tem que fazer o teste.
4. O intervalo contém 0 sugerindo nenhuma diferença.

*** .hint
Volte ao problema, considere as implicações do intervalo sendo
maior que 0, verifique novamente a ordem em que as coisas foram subtraídas e
certifique-se de que os resultados fazem sentido no contexto do problema.

*** .explanation
O intervalo foi realizado subtraindo 4 - 6 e ficou totalmente acima de zero.

--- &multitext
Suponha que 18 indivíduos obesos foram randomizados, 9 cada, para uma nova pílula de dieta e um placebo. Os índices de massa corporal (IMCs) dos indivíduos foram medidos na linha de base e novamente após terem recebido o tratamento ou placebo por quatro semanas. A diferença média do acompanhamento para a linha de base (acompanhamento - linha de base) foi de 3 kg/m2 para o grupo tratado e 1 kg/m2 para o grupo placebo. Os desvios padrão correspondentes das diferenças foram de 1,5 kg/m2 para o grupo de tratamento e 1,8 kg/m2 para o grupo placebo. O estudo visa responder se a mudança no IMC ao longo do período de quatro semanas parece diferir entre os grupos tratado e placebo.

1. Qual é a estimativa de variância agrupada? (com 2 casas decimais)


*** .hint
Os tamanhos das amostras são iguais, então a variância agrupada é a média das
variações individuais


*** .explanation

```r
n1 <- n2 <- 9
x1 <- -3  ##treated
x2 <- 1  ##placebo
s1 <- 1.5  ##treated
s2 <- 1.8  ##placebo
spsq <- ( (n1 - 1) * s1^2 + (n2 - 1) * s2^2) / (n1 + n2 - 2)
```
<span class="answer">2.74</span>


--- &radio
Para dados binomiais, a estimativa de máxima verossimilhança para a probabilidade de
um sucesso é

1. _A proporção de sucessos_
2. A proporção de falhas
3. Uma versão reduzida da proporção de sucessos
4. Uma versão reduzida da proporção de falhas

*** .hint
Reveja as notas sobre a probabilidade.

*** .explanation
A EMV para dados binomiais é sempre a proporção de sucessos.

--- &radio

A inferência bayesiana requer

1. Uma taxa de erro tipo I
2. Definindo seu nível de confiança
3. _Atribuindo uma distribuição de probabilidade anterior_
4. Avaliando as taxas de erro de frequência

*** .explanation
Todas as outras respostas discutem conceitos frequentistas. Todas as análises Bayesianas que exigem a definição de um prior.
