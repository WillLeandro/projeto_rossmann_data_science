# Projeto de Previsão de vendas de 6 semanas  da  Rossmann com Machine Learning

#### AVISO: É um projeto fictício inspirado no desafio "Rossmann Store Sales" publicado no kaggle ( https://www.kaggle.com/c/rossmann-store-sales ), mas com todas etapas de um projeto real.

<div align="center">
<img src="https://www.cosmetic-business.com/media/mandant/globale-verfuegbare-Medien/News-Upload/CosmeticBusiness/2020/Mai/ROSSMANN_Zentrale_Logo.jpg" width="600px" />
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
O projeto foi criado através do método CRSIP-DM, aplicando os seguintes passos:<br>

#### Passo 01 - Descrição dos dados:<br>
Nesta etapa, o objetivo é entender o que os dados podem nos dizer, foi usado métricas estatísticas pada identificar outliers e também analisar méticas de estatístícas básicas como média, mediana, máximo, mínimo, range, skew, kurtosis e desvio padrão. Também foi realizado alguns ajustes em fetures do dataset como preenchimento de NA's por exmplo.

#### Passo 02 - Feature Engineering:<br>
Nesta etapa, foi criado um mapa metal para analisar o fenômeno, suas variáveis e os aspectos que impactam cada variável. A partir disso, foi derivado novos atributos com base nas variáveis originaispara descrever melhor o fenômeno que será modelado.

#### PASSO 03 - Filtragem de variáveis:<br>
Nesta etapa o objetivo foi filtrar linhas e excluir colunas que não são relevantes para o moddelo, como por exemplo desconsiderar os dias em que as lojas não estavam operando ou não relizaram vendas.

#### PASSO 04 - Análise Exploratória dos Dados:<br>
Nesta estpa o objetivo foi  explorar os dados para encontrar insigths, entender a relevância das várias para o aprendizado do modelo. Foi relizadas analises univariadas, biváriadas e multivariadas.

#### PASSO - 05 Preparação dos Dados:<br>
Nesta etapa, os dados foram preparados para o início das aplicações dos modelos de machine learning. Foi utilizadas técnicas de Rescaling e Transformation, através de encodings e nature transformation.

#### PASSO - 06 Seleção de Variáveis:<br>
Nesta etapa foi utilizado o Boruta para selecionar os melhores atributos para treinar o modelo afim de obter uma melhor acurácia.

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


 
