# Projeto de Previsão de vendas de 6 semanas  da  Rossmann com Machine Learning<br>

<div align="center">
<img src="https://user-images.githubusercontent.com/92799101/170358888-ae32b5bc-156f-4802-a41e-a7b5a88ccf7a.png" width="500px" />
</div>

<br><br>

**AVISO: É um projeto fictício inspirado no desafio "Rossmann Store Sales" publicado no kaggle** (https://www.kaggle.com/c/rossmann-store-sales), **mas com todas etapas de um projeto real.**<br>


## Um pouco sobre a rede Rossmann
 A história da empresa começa em 1972: Naquela época, Dirk Rossmann abriu a primeira drogaria self-service na Alemanha. Hoje, a Dirk Rossmann GmbH, com mais de  56.000 funcionários e 4.361 filiais, é uma das maiores redes de drogarias da Europa.
 
 ## Desafio de  negócio
 O diretor de vendas da Rossmann quer estimar o faturamento de cada loja nas próximas 6 semanas, com objetivo de identificar quais lojas teriam faturamento suficiente para realizar reformas em sua estrutura.<br>
 
 Com milhares de gerentes individuais prevendo vendas com base em seu contexto, a precisão dos resultados podem sofrer muitas variações, e isso prejudicaria na tomada de decisão do diretor.<br>
 
 Diante dessa situação o diretor pediu ao time de dados uma solução que venha fazer essa previsão de forma mais precisa, rápida e prática, podendo acessar de qualquer lugar com um simples smartphone<br>
 
 ## Sobre os dados
 
 Os dados foram disponibilizados pela empresa na plataforma Kaggle:<br><br>
 https://www.kaggle.com/c/rossmann-store-sales/data
 
 Abaixo segue a descrição para cada um dos 15 atributos:<br><br>
| **Atributos** |  **Descrição**  |
| ------------------- | ------------------- |
|  id | um Id que representa um (Store, Date) concatenado dentro do conjunto de teste |
|  Store |  um id único para cada loja |
|  Sales |  o volume de vendas em um determinado dia |
|  Customers |  o número de clientes em um determinado dia |
|  Open |  um indicador para saber se a loja estava aberta: 0 = fechada, 1 = aberta |
|  StateHoliday |  indica um feriado estadual. Normalmente todas as lojas, com poucas exceções, fecham nos feriados estaduais. Observe que todas as escolas fecham nos feriados e finais de semana. a = feriado, b = feriado da Páscoa, c = Natal, 0 = Nenhum |
| SchoolHoliday |  indica se (Store, Date) foi afetada pelo fechamento de escolas públicas |
|  StoreType |  diferencia entre 4 modelos de loja diferentes: a, b, c, d |
|  Assortment |  descreve um nível de sortimento: a = básico, b = extra, c = estendido |
|  CompetitionDistance |  distância em metros até a loja concorrente mais próxima |
|  CompetitionOpenSince[Month/Year] |  apresenta o ano e mês aproximados em que o concorrente mais próximo foi aberto |
|  Promo |  indica se uma loja está fazendo uma promoção naquele dia |
|  Promo2 |  Promo2 é uma promoção contínua e consecutiva para algumas lojas: 0 = a loja não está participando, 1 = a loja está participando |
|  Promo2Since[Year/Week] |  descreve o ano e a semana em que a loja começou a participar da Promo2 |
|  PromoInterval | descreve os intervalos consecutivos de início da promoção 2, nomeando os meses em que a promoção é iniciada novamente. Por exemplo. "Fev, maio, agosto, novembro" significa que cada rodada começa em fevereiro, maio, agosto, novembro de qualquer ano para aquela loja |

## Premissas do negócio
- Os dias em que as lojas foram fechadas foram retiradas da análise.
- Foram consideradas apenas lojas com valores de venda maior que 0.
- Para as lojas que não possuíam informações de 'Competition Distance', foi considerado a maior distância observada no conjunto de dados.

## Planejamento da solução
O projeto foi criado através do método CRSIP-DM, aplicando os seguintes passos:<br><br>
<div align="center">
<img src="https://user-images.githubusercontent.com/92799101/170358376-c9fc93b0-8418-4be3-9838-b822638d472f.png" width="700px" />
</div>


#### Passo 01 - Questão de negócio:<br>
Recebimento do problema a ser resolvido. Qual a previsão de vendas de cada loja em 6 semanas? Para determinar quanto do budget vai para reformas das lojas.

#### Passo 02 - Entendimento do negócio:<br>
Entender se a questão de negócio levantada faz sentido para solucionar o problema.


#### Passo 03 - Coleta de Dados:<br>
No mundo real seria o passo onde fariamos consultas SQL e joins, mas nesse caso apenas fizemos um donwnload no Kaggle https://www.kaggle.com/c/rossmann-store-sales 

#### Passo 04 - Limpeza dos Dados:<br>
Nessa etapa foi realizado a descrição dos dados, feature engineering, seleção de features baseadas no negócio.

#### Passo 05 - Exploração dos Dados:<br>
Nessa etapa criamos um mapa metal de hipóteses par nos orientar na exploração dos Dados e encontrar insights, entender melhor a relevância das variáveis no aprendizado do modelo. Foram feitas analises univariadas, biváriadas e multivariadas, utilizando os dados numéricos e categóricos do conjunto.

#### Mapa mental:<br>
<div align="center">
<img src="https://user-images.githubusercontent.com/92799101/170358069-38ebd7a5-4de6-400c-938a-275794ef60f5.png" width="700px" />
</div>

#### Hipóteses Geradas:<br>
1. Lojas com maior sortimento devem vender mais
2. Lojas com concorrentes mais próximos devem vender menos
3. Lojas com concorrentes mais antigos devem vender mais
4. Lojas onde os produtos custam menos por mais tempo (promoções ativas) devem vender mais
5. Lojas com mais dias de promoção devem vender mais
6. Lojas com promoções mais estendidas devem vender mais
7. Lojas abertas no feriado de Natal devem vender mais
8. Lojas devem vender mais ao longo dos anos
9. Lojas devem vender mais no segundo semestre
10. As lojas devem vender mais após o dia 10 de cada mês
11. Lojas devem vender menos nos finais de semana
12. Lojas devem vender menos durante as férias escolares
13. Lojas que abrem aos domingos devem vender mais

#### Principais insights
**H1. Lojas com maior sortimentos deveriam vender mais.**<br>
FALSA Lojas com MAIOR SORTIMENTO vendem MENOS
<div align="center">
<img src="https://user-images.githubusercontent.com/92799101/170357722-9fd5f050-466c-4f18-a8b8-5d1f64d3d052.png" width="700px" />
</div><br>

**H2. Lojas com competidores mais proximos deverima vender menos.**<br>
FALSA Lojas com competidores MAIS PROXIMOS vendem MAIS
<div align="center">
<img src="https://user-images.githubusercontent.com/92799101/170357861-cb27012b-248a-4443-b663-6b85d21c2f7b.png" width="700px"/>
</div><br>

**H11. lojas deveriam vender menos aos finais de semana.**<br>
VERDADEIRA Lojas vendem menos aos finais de semana
<div align="center">
<img src="https://user-images.githubusercontent.com/92799101/170357539-aae2083e-c5ba-4c54-9227-f54473598112.png" width="700px" />
</div><br>

#### Passo 06 - Modelagem dos Dados:<br>
Nesta etapa, os dados foram preparados para o início das aplicações dos modelos de machine learning. Foram utilizadas técnicas de Rescaling e Transformation, através de encodings e nature transformation, e também o Boruta para selecionar os melhores atributos para treinar o modelo afim de obter uma melhor acurácia.

#### PASSO 07 - Machine Learning Modeling:<br>
Nesta etapa,foi relizado testes e treinamento em 5 modelos,Random Forest Regressor,XGBoost Regressor, Linear Regression - Lasso, Linear Regressor e Average Model.<br>
Usamos  o Average Model como base para compararmos os demais modelos  suas respctivas performance e escolha do melhor modelo.<br><br> 

| **Model Name** |  **MAE**  |  **MAPE**  |  **RMSE**  |
| ------------------- | ------------------- | ------------------- | ------------------- |
|  Random Forest Regressor | 679.559752 | 0.099934  | 1010.884194 |
|  XGBoost Regressor | 874.171929 | 0.126807 | 1287.707669 |
|  Linear Regression - Lasso | 1891.702083 | 0.289165  | 2744.462516 |
|  Linear Regressor | 1867.086951  | 0.292756 | 2671.056821  |
|  Average Model | 1354.800167 | 0.206441  | 1835.141019 |

Também foi aplicada a técnica de Cross Validation para garantir a performance real sobre os dados selecionados.<br><br>

| **Model Name** |  **MAE CV**  |  **MAPE CV**  |  **RMSE CV**  |
| ------------------- | ------------------- | ------------------- | ------------------- |
|  Random Forest Regressor | 838.34 +/- 218.54 | 0.12 +/- 0.02 | 1257.62 +/- 319.71 |
|  XGBoost Regressor | 1054.69 +/- 172.95 | 0.15 +/- 0.02 | 1521.43 +/- 238.54 |
|  Linear Regression - Lasso | 2116.39 +/- 341.51 | 0.29 +/- 0.01 | 3057.77 +/- 504.27 |
|  Linear Regressor | 2081.73 +/- 295.64 | 0.3 +/- 0.02 | 2952.53 +/- 468.38 |


A melhor performace encontrada foi do  Random Forest Regressor, porém escolhemos o modelo XGBoost Regressor. A razão dessa escolha é que o XGBoost é um modelo mais leve para operar em produção e não aparesenta diferença significativa de desempenho.

#### PASSO 08 - Avaliação do Algorítimo<br>
**Hyperparamenter Fine Tunning:**<br><br>
Com o algorítimo XGBoost escolhido na etapa anterior, foi realizada uma análise através do método Randon Search para escolher os melhores valores para cada parâmetro do modelo e encontrar a performance final do XGBoost.<br>

**Desempenho dos dados de teste:**<br>

| **Model Name** |  **MAE**  |  **MAPE**  |  **RMSE**  |
| ------------------- | ------------------- | ------------------- | ------------------- |
|  XGBoost Regressor | 661.845808 | 0.097704  | 951.379757|

**Tradução e interpretação de erros:**<br><br>
Nesta etapa o objetivo foi demonstrar o resultado do projeto, onde avaliamos a performance do modelo com viés de negócio, demonstando o resultado financeiro que pode-se esperar do modelo desenvolvido.<br>

| **Store** |  **Predictions**  |  **MAE**  |  **MAPE**  |  **days**  |  **Worst_scenario**  |  **best_scenario**  |
| ------------------- | ------------------- | ------------------- | ------------------- | ------------------- | ------------------- | ------------------ |
|  1 | 169305.70 | 307.78  | 0.07 | 37 | R$ 157.881,01 | R$ 180.730,40 |
|  2 | 182122.09 | 395.48  | 0.08 | 37 | R$ 167.491,11 | R$ 196.753,09 |
|  3 | 258817.89 | 538.91  | 0.08 | 37 | R$ 238.878,23 | R$ 278.757,55 |
|  4 | 338596.25 | 944.09  | 0.09 | 37 | R$ 303.664,96 | R$ 373.527,54 |
|  5 | 174173.37 | 388.33  | 0.09 | 37 | R$ 159.805,20 | R$ 188.541.55 |

#### PASSO 09 - Deploy do modelo em produção:<br>
Após a execução com sucesso do modelo, foi publicado em um ambiente de nuvem para outras pessoas ou serviços estarem consultando as previsões do modelo e poderem usar os resultados para tomadas de decisões. A plataforma em nuvem escolhida foi o Heroku (www.heroku.com).<br>

Abaixo temos a representação de todo o esquema em produção.<br>

<div align="center">
<img src="https://user-images.githubusercontent.com/92799101/170357095-3299e2a4-4d0e-42c3-99a1-656f86a51ab4.png" width="700px" />
</div><br>



#### PASSO 10 - Bot no Telegram:<br>
A etapa final do projeto foi criar um bot no aplicativo de mensagens Telegram, que possibilita consultar as previsões de cada loja de qualquer lugar e a qualquer momento, na demonstração abaixo as consultas foram realizadas através de um smartphone, aplicação essa que também relaizamos deploy na plataforma em nuvem Heroku.




 
