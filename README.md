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

#### Passo 06 - Modelagem dos Dados:<br>



+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

#### PASSO - 05 Preparação dos Dados:<br>
Nesta etapa, os dados foram preparados para o início das aplicações dos modelos de machine learning. Foi utilizadas técnicas de Rescaling e Transformation, através de encodings e nature transformation.

#### PASSO - 06 Seleção de Variáveis:<br>
***Também utilizamos o Boruta para selecionar os melhores atributos para treinar o modelo afim de obter uma melhor acurácia.

#### PASSO 07 - Machine Learning Modeling:<br>
Nesta etapa,foi relizado testes e treinamento em alguns modelos de machine learning, onde comparamos suas respctivas performance e escolha do melhor modelo. Também foi aplicada a técnica de Cross Validation para garantir a performance real sobre os dados selecionados.

#### PASSO 08 - Hyperparamenter Fine Tunning:<br>
Com o algorítimo XGBoost escolhido na etapa anterior, foi realizada uma análise través do método Randon Search para escolher os melhores valores para cada parâmetro do modelo. 

#### PASSO 09 - Tradução e interpretação de erros:<br>
Nesta etapa o objetivo foi demonstrar o resultado do projeto, onde avaliamos a performance do modelo com viés de negócio, demonstando o resultado financeiro que pode-se esperar do modelo desenvolvido.

#### PASSO 10 - Deploy do modelo em produção:<br>
Após a execução com sucesso do modelo, foi publicado em um ambiente de nuvem para outras pessoas ou serviços estarem consultando as previsões do modelo e poderem usar os resultados para tomadas de decisões. A plataforma em numvem escolhida foi o Heroku.

#### PASSO 11 - Bot do Telegram:<br>
A etapa final do projeto foi criar um bot no aplicativo de mensagens Telegram, que possibilita consultar as previsões de qualquer lugar e a qualquer momento, aplicação que também relaizdo deploy na plataforma em nuvem Heroku.


 
