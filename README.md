# Projeto de Previsão de vendas de 6 semanas  da  Rossmann com Machine Learning

#### AVISO: É um projeto fictício inspirado no desafio "Rossmann Store Sales" publicado no kaggle ( https://www.kaggle.com/c/rossmann-store-sales ), mas com todas etapas de um projeto real.

<div align="center">
<img src="https://scontent.fmii9-1.fna.fbcdn.net/v/t39.30808-6/281752562_2782332161913359_4956668997691908172_n.jpg?stp=dst-jpg_p180x540&_nc_cat=101&ccb=1-6&_nc_sid=730e14&_nc_eui2=AeF3uxQDYsB7gur594DLOIyLL6yRbmKVkYUvrJFuYpWRhXiG_NLPg3A7ii1PUajpWkoL4TfmiXhHL6HBC5hi2HgU&_nc_ohc=EBP4vETnUjIAX_bw-RK&tn=nzFSmjrCcyH-qWlv&_nc_ht=scontent.fmii9-1.fna&oh=00_AT9g9u4Pl2IT1mOi305c4C2XLsLzHtQ6weJxA2KSax4l6A&oe=628A7F21" width="400px" />
</div>

<br><br>
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
<img src="https://scontent.fmii9-1.fna.fbcdn.net/v/t39.30808-6/282036074_2782292678583974_2011897632509970238_n.jpg?stp=dst-jpg_p180x540&_nc_cat=106&ccb=1-6&_nc_sid=730e14&_nc_eui2=AeEm8bgQ4EUSmR4cJ2EMFr5g-bO6dlGkCSH5s7p2UaQJIQ0yKVjaKcgkOb1d86ynTG7rdxZgEv29CEiT4YKOSDKd&_nc_ohc=amE1GHrA-YgAX8N35iH&_nc_ht=scontent.fmii9-1.fna&oh=00_AT-Qa65Vxlx2WSboLgIEkV9PJGtOQe_V8MREOcIQA0O6Qg&oe=62898432" width="600px" />
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
<img src="https://scontent.fmii9-1.fna.fbcdn.net/v/t39.30808-6/283080931_2785058198307422_9043376111299872483_n.jpg?_nc_cat=108&ccb=1-7&_nc_sid=730e14&_nc_eui2=AeHeU4R7QXnpRlPfWXg0KJDjz0IVfB14DK7PQhV8HXgMroTg8F1HTI_Rk8gKHjaA-HdN8Pp_1uHW5VMvHQqZU-_r&_nc_ohc=uCXjCfb8lk8AX9VVu9d&_nc_oc=AQnUts2joWdO_2p6sy-kjNC02jYe_dh3CtZrmoFlIo_5_-rABffS4QlPD2L_hryd4EKnzKigYZvTzyc6f5SUyprI&_nc_ht=scontent.fmii9-1.fna&oh=00_AT9bLQtKQNDl7lHE_ygB4hIwwyVs_oJ8HbUhToap5zvTxA&oe=628E5B34" width="800px" />
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
<img src="https://scontent.fmii9-1.fna.fbcdn.net/v/t39.30808-6/283478631_2788066764673232_2140441876371134275_n.jpg?_nc_cat=100&ccb=1-7&_nc_sid=730e14&_nc_eui2=AeFQxdMf7AUgB4GcL9ZFjqP4gvEJInh6yL2C8QkieHrIvbtyuhUUp7Ay-gz2Bdpw-gTh6vSWKhI5Ap2clC4i7L5s&_nc_ohc=2xlQytIL-k8AX-QbFTL&_nc_ht=scontent.fmii9-1.fna&oh=00_AT_qCg8YgmVsURd_Lr8WuMLRGqsPscWofKI0xj34Gpgsnw&oe=62927D36" width="800px" />
</div><br>

**H2. Lojas com competidores mais proximos deverima vender menos.**<br>
FALSA Lojas com competidores MAIS PROXIMOS vendem MAIS
<div align="center">
<img src="https://scontent.fmii9-1.fna.fbcdn.net/v/t39.30808-6/283284880_2788066781339897_2737432107462859078_n.jpg?_nc_cat=100&ccb=1-7&_nc_sid=730e14&_nc_eui2=AeG7L5u-oVxX-ciDBLUUsoskqjMsObsDq3iqMyw5uwOreCP3IzUsU6R3zJCjts5eeXfb4tqgADc_UOwa4pTrfDhh&_nc_ohc=6Gd4G3KgHBYAX9ACB9V&tn=nzFSmjrCcyH-qWlv&_nc_ht=scontent.fmii9-1.fna&oh=00_AT8bkixui7uwk2SI5k2yC2E1z1VzydRbDZB-enPNBVGMUw&oe=6291C411" width="800px"/>
</div><br>

**H11. lojas deveriam vender menos aos finais de semana.**<br>
VERDADEIRA Lojas vendem menos aos finais de semana
<div align="center">
<img src="https://scontent.fmii9-1.fna.fbcdn.net/v/t39.30808-6/282580899_2788066784673230_7967619590883472596_n.jpg?_nc_cat=100&ccb=1-7&_nc_sid=730e14&_nc_eui2=AeHUgTuEiOErm_kahRVC-u_I-EOU-6g7ujP4Q5T7qDu6M_6a1inRJcD2owbjyovLjes8uKPyMBIuG-PsD0pwtzRk&_nc_ohc=UsEbaJAdMIsAX-SsKd8&_nc_ht=scontent.fmii9-1.fna&oh=00_AT8C6Nf1LEur6nYjAqubdSn3tC68AdIlDwPmPEg-TE-oeQ&oe=629293FE" width="800px" />
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
<img src="https://scontent.fmii9-1.fna.fbcdn.net/v/t39.30808-6/283674553_2789064747906767_7987155453759978199_n.jpg?_nc_cat=101&ccb=1-7&_nc_sid=730e14&_nc_ohc=P7Me25iEX3AAX-l1Zxj&_nc_ht=scontent.fmii9-1.fna&oh=00_AT83CasiGCGB04byEJNYNoaqdoAGgJe93Vj72mk6_HdBOQ&oe=6292E97E" width="800px" />
</div><br>



#### PASSO 10 - Bot do Telegram:<br>
A etapa final do projeto foi criar um bot no aplicativo de mensagens Telegram, que possibilita consultar as previsões de qualquer lugar e a qualquer momento, aplicação que também relaizdo deploy na plataforma em nuvem Heroku.


 
