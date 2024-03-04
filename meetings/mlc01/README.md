# Introdução a Machine Learning
### Vítor Fróis, Miller Anacleto e Gabriel Merlin
## Introdução
### Uma breve história
Há muito tempo a humanidade flerta com a possibilidade de uma máquina que replicasse o comportamento humano. 
Nesse contexto diversas peças de cultura contam como a Inteligência Artificial conviveria com os humanos, 
como Robocop e Eu, Robô.

Ainda na época que a IA começou a se desenvolver, diversos cientistas buscaram produzir seus próprios autônomos.
Turing, em 1953, lançou um paper contando como desenvolver uma máquina que jogasse xadrez.
Ainda assim, programar esse tipo de comportamento pode ser muito difícil.

![venn](https://github.com/icmc-data/ml-study-group/assets/46361092/6002603a-1711-4cee-abf6-09de81523f2f)

Foi nessa situação que o Aprendizado de Máquina (ou Machine Learning) cresceu. Com o intuito de rapidamente replicar o comportamento 
humano sem explicitamente programar, o ML utiliza a Ciência de Dados para alcançar a meta.

> _“Machine Learning: the field of study that gives computer the ability to
> learn without being explicitly programmed.”_ - Arthur Samuel, 1959

> _“A computer programming is said to learn from experience E with respect to some task T
> and some performance measure P if its performance on T, measured by P, improves with E.”_ - Tom Mitchell, 1998

De forma simplificada, a frase de Tom diz que queremos aproximar uma função $g(x)$ utilizando uma $f(x)$. 
E para isso, utilizamos um conjunto de dados que nos permite aproximar _bem o suficiente_ a função $g(x)$.

### Categorias 
![ml_tasks](https://github.com/icmc-data/ml-study-group/assets/46361092/5148cd7a-984d-4090-8a80-2e5e71d760e1)

ML é uma área muito ampla e infelizmente não iríamos conseguir abordar todos os tópicos. 
Assim, vamos focar nos mais tradicionais modelos e exemplos.

### A Engenharia de Machine Learning
![image](https://github.com/icmc-data/ml-study-group/assets/46361092/544faf65-ea28-4236-8399-f315e2f78ead)

Entretanto, ainda que estejamos estudando uma parte de ML, todo o processo para fazer uma aplicação envolve
desde a retirada dos dados até a visualização. De forma simplificada, essas tarefas juntas formam o campo da 
Ciência de Dados.

## Fundamentos de ML
### Conjunto de Dados
**Dataset** é o termo em inglês para conjunto de dados. Esses são os dados completos que estaremos utilizando
para treinar, testar e validar um modelo.

### Características (Features)
Features ou características são as expressões dos dados, valores numéricos vetorizados que melhor representam cada conjunto de treinamento.

![iris](https://github.com/icmc-data/ml-study-group/assets/46361092/d5ad0a30-8602-43ea-b37a-488fc9b706db)

No Dataset Iris, as características foram extraídas com antecedência: tamanho das sépalas e das pétalas. Cada um desses dados é rotulado com a flor correspondente: Iris Setosa, Iris Virginica e Iris Versicolor.

Vamos ver detalhes sobre a extração de características mais a fundo ao longo do grupo de estudos, então não se preocupem.

### Treino e Teste
Quando treinamos um modelo de ML, esperamos que ao apresentar novos dados, ele possua a capacidade de generalizar.

Vamos exemplificar: 
- treinamos um modelo para identificar se dadas imagens são de cachorro
- ao apresentar uma nova imagem de cachorro, esperamos que o modelo retorne um resultado positivo

Nem sempre possuímos a imagem que desejamos testar. Assim, é necessário separar o Dataset original entre treino e teste.
Dessa forma, o modelo será treinado nos **dados de treino** e então será testado nos **dados de teste**.

### Erro
O erro é uma forma de medir quão bem um modelo performou.

### Viés e Variância
Após o treinamento, um modelo pode apresentar um grande **viés**. Isso significa que ele consegue generalizar bem novos dados. 

De forma contrária, o modelo também pode apresentar grande **variância** (e baixo viés). Nesse caso, ele se adapta bem 
aos dados de treinamento mas não possui a flexibilidade necessária para generalizar em dados de teste.

O fenômeno de alta variância indica que o modelo **_overfittou_** (do inglês, _overfitting_) e pode ser visualizado na curva azul da imagem abaixo.

![overfitting](https://github.com/icmc-data/ml-study-group/assets/46361092/217c43c6-a640-4a51-9f6d-6c99e9c8b1b1)

### Validação Cruzada
É difícil afirmar qual a melhor forma de executar a partição do nosso Dataset entre treino e teste. 
Nesse cenário, a validação cruzada é uma técnica para superar esse problema na base da força bruta. 
Essa técnica 'quebra' o Dataset em $n$ partes e realiza $n$ iterações de treinamento com os pedaços para treinar e testar o modelo.

No final, o erro do modelo será a média aritmética de cada um das $n$ iterações de treinamento.

![image](https://github.com/icmc-data/ml-study-group/assets/46361092/d7b9f1c3-c9b1-4327-8667-56644fadef4a)


## Referências
- [Patrick Winston - Introduction to Learning](https://www.youtube.com/watch?v=09mb78oiPkA&list=PLUl4u3cNGP63gFHB6xb-kVBiQHYe_4hSi&index=11)
- [Statquest - Intro a ML](https://www.youtube.com/watch?v=Gv9_4yMHFhI)
- [Statquest - Viés e Variância](https://www.youtube.com/watch?v=EuBBz3bI-aA)
- [Statquest - Validação Cruzada](https://www.youtube.com/watch?v=fSytzGwwBVw)
- Slides do Diego Furtado
