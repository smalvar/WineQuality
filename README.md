# WineQuality
Resolução do desafio da Cognitivo.ai


O presente problema se refere aos dados de vinhos portugueses "Vinho Verde", que possuem variantes de vinho branco e tinto. Devido a questões de privacidade, apenas variáveis físico-químicas (input) e sensoriais (output) estão disponíveis. As variáveis presentes são:

 > 1. Acidez fixa: quantidade de ácidos envolvidos no vinho que são fixos ou não voláteis.
   
 > 2. Acidez volátil: a quantidade de ácido acético no vinho, que em níveis muito altos pode levar a um sabor desagradável.

 > 3. Ácido cítrico: encontrado em pequenas quantidades, o ácido cítrico pode adicionar 'frescura' e sabor aos vinhos
 
 > 4. Açúcar residual: a quantidade de açúcar restante após a fermentação. É raro encontrar vinhos com menos de 1 grama / litro e vinhos com mais de 45 gramas / litro são considerados doces.
  
 > 5. Cloretos: a quantidade de sal no vinho
 
 > 6. Dióxido de enxofre livre: a forma livre de SO2 existe em equilíbrio entre o SO2 molecular (como um gás dissolvido) e o íon bissulfito; impede o crescimento microbiano e a oxidação do vinho.

> 7. Dióxido de enxofre total: quantidade de formas livres e ligadas de S02; em baixas concentrações, o SO2 é principalmente indetectável no vinho, mas em concentrações livres de SO2 acima de 50 ppm, o SO2 se torna evidente no nariz e no sabor do vinho.

> 8. Densidade: a densidade é próxima a da água, dependendo da porcentagem de álcool e açúcar.

> 9. pH: descreve como um vinho é ácido ou básico em uma escala de 0 (muito ácido) a 14 (muito básico); a maioria dos vinhos tem entre 3-4 na escala de pH.

> 10. Sulfatos: aditivo para vinho que pode contribuir para os níveis de gás dióxido de enxofre (S02), que atua como antimicrobiano e antioxidante.

> 11. Álcool: o percentual de teor alcoólico do vinho



## a. Como foi a definição da sua estratégia de modelagem?

O trabalho é efetuado considerando 4 etapas principais: 
1. Limpeza de dados;
2. Análise exploratória;
3. Modelagem;
4. Comparação.

Dentro dessas etapas, algumas subrotinas são extremamente importantes:
1. Limpeza de dados:
   - Identificação de outliers;
   - Utilização do método Z-score para remoção dos outliers;
   - Binarização do atributo "type": variável dummy.
2. Análise exploratória:
   - Criação de outra coluna como categoria da avaliação: bom, regular e ruim;
   - Análise de correlação;
   - Análise em pairplot das principais variáveis;
   - Análise em violin plot das principais variáveis em relação à qualidade.
3. Modelagem:
   - Separar 20% dos dados para serem usados como dados de validação e 80% para treino;
   - Aplicar normalizador StandardScaler;
   - Testar técnicas de regressão que considero mais adequadas:
     - DecisionTreeRegressor
     - KNeighborsRegressor
     - RandomForestRegressor
     - DecisionTreeRegressor
4. Comparação:
   - Comparação da acurácia de teste e treinamento de cada modelo;
   - Cálculo do F1-score 'ponderado'.

## b. Como foi definida a função de custo utilizada?

Utilizei a função de custo entropia, comumente usada em classes, uma vez que a Gini normalmente deve ser usada em atributos contínuos. Isso é uma informação importante, pois como essa opção é mais custosa computacionalmente (pois utiliza transformação logarítmica), é comum que o índice Gini seja usado de foma inadequada em todas as aplicações. Caso as classes fossem muito desbalanceadas, teríamos que utilizar outra metodologia. Mais informações podem ser encontradas no trabalho de Elena Raileanu e Kilian Stoffel, *Theoretical comparison between the Gini Index andInformation Gain criteria* (https://www.unine.ch/files/live/sites/imi/files/shared/documents/papers/Gini_index_fulltext.pdf).

## c. Qual foi o critério utilizado na seleção do modelo final?

Ao contrário das classificações binárias, as quais funções de erro comum ou matriz confusão simples são usadas, no caso de um problema de várias classes, temos de utilizar outras métricas. Neste caso, escolhi utilizar as acurácias nos dados de teste e também o F1-score ponderado (não confundir com o F1-score e problemas com target binário).

## d. Qual foi o critério utilizado para validação do modelo? Por que escolheu utilizar este método?

Utilizei dois critérios: validação cruzada e RMSE.

- RMSE: Essa é uma excelente métrica para modelos de regressão, além de ser muito fácil de interpretar. A Raiz Quadrada do Erro Quadrático Médio — ou simplesmente RMSE em inglês — nada mais é que a diferença entre o valor que foi previsto pelo seu modelo e o valor real que foi observado.
- Validação cruzada: Cross-Validation — ou Validação Cruzada — é uma técnica que visa entender como seu modelo generaliza, ou seja, como ele se comporta quando vai prever um dado que nunca viu. Então criamos diferentes conjuntos de treino e teste e treinamos o modelo e ter certeza de que ele está performando bem. Nesse caso, ao invés de usarmos apenas um conjunto de teste para validar nosso modelo, utilizaremos N outros a partir dos mesmos dados. Utilizei o método K-Fold.

A junção desses dois nos permite obter o melhor conjunto de validação paa um problema de regressão multivariável.

## e. Quais evidências você possui de que seu modelo é suficientemente bom?

Realizei um teste com um conjunto de testes e os valores previstos foram idênticos aos valores target. Pelas métricas apresentadas, observa-se que na maior parte dos casos, o modelo irá acerca todas as entradas. Em alguns casos, poderá errar a classificação de 1 ou 2 vinhos em todo o connjunto. 

É importante ressaltar que esses testes foram feitos anteriormente com o conjunto de dados sujo, ou seja, com os outliers. O melhor resultado obtido nesse caso havia sido uma acurácia de 60%. Isso ressalta a importância de uma correta limpeza dos dados.
