# Descrição do Projeto
Este projeto teve como objetivo prever o churn de clientes em uma empresa de telecomunicações. O churn representa a perda de clientes, e o foco principal do projeto é identificar quais clientes estão propensos a cancelar os serviços, permitindo à empresa agir de maneira proativa para reter esses clientes.

O objetivo é atingir um ROC-AUC mínimo de 0.75

# Estrutura do Projeto

## Bibliotecas
Scikit-learn, XGBoost, LightGBM, CatBoost, Pandas, Numpy, Matplotlib, Seaborn, Shap

## Preparação dos Dados
Visualização dos DataFrames, entendimento dos dados, tratamento de dados ausentes, conversão de tipos de dados, concatenação dos DataFrames e criação da coluna 'churn' como target.

## AED
Divisão dos dados em numéricos, categóricos e temporais para a realização de um estudo aprofundado sobre cada um deles;

Realização do estudo da distribuição dos dados em cada característica, além da proporção de churn em cada uma das opções disponíveis nas diferentes categorias;

Comparações de grupos de clientes (idosos vs Não-Idosos);

Distribuições e Estatísticas Descritivas de cada variável numérica;

Verificação de outliers;

Comparação de médias de clientes 'Churn' com clientes 'Não-Churn';

Análise de dados temporais, realizando um estudo sobre as tendências e sazonalidade de cada categoria através da criação de colunas que permitissem o conhecimento de tempo de contrato;

## Feature Engineering
Através dos estudos realizados na etapa de AED, foram criadas diversas colunas (características) relevantes que contribuem para um bom resultado de predição dos modelos.

Foi possível criar 14 novas colunas, sendo que a maioria delas contribuiu significativamente com os resultados dos modelos, o que pode ser verificado no 'Feature importance';

Remoção de algumas colunas desnecessárias, como algumas colunas de dados tipo datetime e outras que não tem relação direta com o churn, como 'ID' e 'Gender' (o que foi verificado durante o AED);

## Divisão dos Dados
Dados foram divididos com 80% para o conjunto de treinamento e 20% para o conjunto de testes;

## Clusterização
Foi realizada clusterização para a criação de grupos de clientes, buscando-se conhecer similaridades entre eles, com intuito de identificar grupos com mais propenção ao churn;

Antes de utilizar o modelo KMeans, foi realizado um estudo sobre a contribuição das variáveis originais para o modelo e, desta forma, foram selecionadas somente as características que contribuíssem de forma relevante. Para este estudo foi utilizada a transfromação PCA;

Transformação do conjunto de treinamento para clusterização (codificação com OrdinalEncoder e padronização com StandardScaler);

Método do cotovelo para determinação da quantidade de clusters no modelo KMeans;

Treinamento do modelo e visualização dos clusters em 2D e 3D, além da visualização de churn por cluster;

Estudo dos clusters determinados e suas características;

## Transformação dos Dados
Realizada a codificação com OrdinalEncoder e padronização com StandardScaler no conjunto de treinamento completo (sem a remoção de colunas irrelevantes para a clusterização);

## Tratamento do desequilíbrio de Classes
Utilizada superamostragem com a técnica SMOTE, muito utilizada para problemas de churn;

## Treinamento dos modelos básicos
Foram treinados modelos básicos (sem ajuste de hiperparâmetros) como LogisticRegression, DecisionTreeClassifier, RandomForest, XGBoost, LightGBM e CatBoost, além da rede neural keras.

Nesta etapa o objetivo foi verificar quais modelos se ajustavam melhor à predição de churn para realizar a seleção daqueles com maior potencial para seguirmos com os ajustes de hiperparâmetros;

### Métricas de Avaliação
Para a avaliação do desempenho do modelo, foram utilizadas as métricas **AUC-ROC, F1_Score, Acurácia, Matriz de confusão, Precisão e Sensibilidade.**

A matriz de confusão tem o objetivo de avaliar se o modelo obtém poucos resultados de Falso Negativo em relação aos resultados de Falso Positivo (custo da perda de um cliente é maior do que o custo de oferecer promoções a um cliente que não sofreria churn).

Foi realizada a comparação das métricas obtidas por cada modelo e selecionados os 4 melhores para a etapa de Tuning;

### Feature Importance
Foi realizado estudo sobre a importância de cada feature no treinamento dos modelos que foram selecionados como os melhores desempenhos;

## Tuning dos modelos
Ajuste dos hiperparâmetros dos modelos selecionados na etapa anterior utilizando GridSearch para melhorar ainda mais seu desempenho;

## Teste dos modelos 
Avaliados os resultados dos modelos no conjunto de teste

# Resultados
O Melhor modelo obtido após ajustes de hiperparâmetros foi o LGBM e alcançou os seguintes resultados:
* AUC-ROC: 0.9420;
* F1: 0.8016;
* Acurácia: 0.8934;
* Recall: 0.7911;
* Precisão: 0.8123;
* Matriz de Confusão: VN=954, FN=80, VP=303 e FP=70

## Estudo do Melhor Modelo
Após definição do melhor modelo foi realizado um estudo do mesmo através de:
* Feature Importance;
* Gráfico SHAP;
* Análise de Índice de Confiança do modelo utilizando Bootstraping, onde foi possível verificar a robustez do modelo, que apresentou baixa variância nas métricas;

# Conclusão
Os resultados obtidos no projeto foram muito satisfatórios e o AUC-ROC objetivo, que era acima de 0.75, foi muito superado por todos os modelos, então todos atenderiam às nossas necessidades.

Porém, analisando as métricas obtidas, percebemos que **O melhor modelo, foi o LightGBM**, pois além de obter o melhor valor de AUC-ROC, também obteve o melhor resultado de F1, uma acurácia muito próxima à dos outros modelos e seu Recall se destacou muito dos demais. 

Conforme descrito no planejamento, uma questão importante é que o modelo tenha uma sensibilidade maior para predizer clientes com possibilidade de churn, pois o custo da perda de um cliente é elevado e, portanto, neste caso é preferível ter mais Falsos Positivos do que Falsos Negativos.

O estudo dos Índices de Confiança com bootstrapping realizado sobre o melhor modelo nos confirmou a robustez do mesmo, indicando que ele é estável mesmo com diferentes amostras do conjunto de dados, pois apresentou baixa variância nas métricas, garantindo que ele não teve um overfitting.

O resultado positivo obtido neste projeto foi consequência de um bom desenvolvimento da AED e também da etapa de Feature Engineering, que permitiram um conhecimento profundo do problema, o que propiciou a criação de features que foram fundamentais para a predição dos modelos, pois dentre as 10 features mais importantes para o modelo, 6 foram criadas na etapa de Feature Engineering.