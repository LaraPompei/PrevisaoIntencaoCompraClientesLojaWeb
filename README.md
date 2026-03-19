# Previsão de Intenção de Compra de Clientes em Loja Web

## Sobre o projeto

Este projeto tem como objetivo prever a intenção de compra de clientes em uma loja web a partir de variáveis demográficas, renda, comportamento de consumo e interação com o canal digital.

A proposta foi construir um fluxo completo de análise e modelagem, passando por preparação dos dados, análise exploratória, pré-processamento, comparação entre algoritmos e avaliação final de desempenho.

## Objetivo

Desenvolver um modelo de classificação capaz de identificar se um cliente possui ou não intenção de compra no canal web, utilizando informações históricas e comportamentais para apoiar decisões de marketing e segmentação.

## Dataset

A base contém informações sobre perfil e comportamento dos clientes, incluindo variáveis como:

- `Year_Birth`
- `Education`
- `Marital_Status`
- `Income`
- `Kidhome`
- `Recency`
- gastos com diferentes categorias de produtos
- número de compras em loja
- número de visitas ao site por mês
- reclamações
- variável alvo `WebPurchases`

## Etapas do projeto

### 1. Preparação dos dados

Nesta etapa foram realizadas verificações iniciais de integridade e consistência da base.

Principais ações:
- leitura e inspeção inicial da base
- análise estatística descritiva
- verificação de tipos das variáveis
- conversão da variável `WebPurchases` para tipo booleano
- identificação de valores ausentes
- identificação de registros duplicados

### 2. Tratamento de dados faltantes

A variável `Income` apresentava valores ausentes.

Foi adotada a seguinte estratégia:
- imputação pela mediana dentro dos grupos formados por `Education` e `Marital_Status`
- preenchimento residual com a mediana global da variável

Resultado:
- todos os valores ausentes foram tratados
- a base passou a ficar sem dados nulos

### 3. Remoção de duplicatas

Foram identificadas **201 linhas duplicadas**, que foram removidas da base para evitar distorções na análise e na modelagem.

### 4. Tratamento de inconsistências e outliers

Foram identificadas categorias raras ou inconsistentes em `Marital_Status`, como `YOLO` e `Absurd`, que foram tratadas como valores inválidos e removidas.

Também foram removidos registros considerados incoerentes para o problema:
- `Year_Birth <= 1940`
- `Income >= 600000`

Esses filtros ajudaram a reduzir ruído e tornar a base mais aderente ao contexto real de negócio.

### 5. Análise exploratória de dados

Foi realizada análise visual das variáveis categóricas e numéricas com gráficos desenvolvidos em Plotly.

Foram exploradas:
- distribuições das variáveis categóricas
- boxplots das variáveis numéricas
- identificação de padrões gerais e possíveis anomalias
- avaliação visual antes e depois do tratamento de inconsistências

### 6. Pré-processamento

Para viabilizar a modelagem, as variáveis categóricas foram codificadas com **One Hot Encoding**.

Variáveis transformadas:
- `Marital_Status`
- `Education`

Após a codificação, a base final utilizada na modelagem passou a conter **2031 registros** e **24 colunas**.

### 7. Análise de correlação

Foi construída uma matriz de correlação para investigar associações entre as variáveis numéricas e entender o espaço para seleção e interpretação de atributos.

A análise mostrou associação mais forte da variável alvo com:
- histórico de consumo
- renda
- indicadores de interação com o canal digital

### 8. Modelagem

Foram avaliadas três abordagens:

- **Regressão Logística**
- **Random Forest**
- **Regressão Logística com PCA**

A validação foi feita com:
- `KFold(n_splits=5, shuffle=True, random_state=42)`
- métrica principal: **F1-score**

## Resultados

### Desempenho médio na validação cruzada

| Modelo | F1 médio | Desvio padrão |
|---|---:|---:|
| Regressão Logística | 0.8365 | 0.0091 |
| Random Forest | 0.8996 | 0.0117 |
| Regressão Logística com PCA | 0.8298 | 0.0167 |

### Avaliação final da Regressão Logística

- **Acurácia:** 0.84
- **F1 classe 0:** 0.83
- **F1 classe 1:** 0.84
- **F1 macro:** 0.84

### Avaliação final da Random Forest

- **Acurácia:** 0.89
- **F1 classe 0:** 0.89
- **F1 classe 1:** 0.90
- **F1 macro:** 0.89

## Conclusões

A **Random Forest** apresentou o melhor desempenho entre os modelos testados, superando a Regressão Logística tanto em F1-score quanto em acurácia.

Principais conclusões:
- o tratamento prévio da base foi essencial para melhorar a consistência dos dados
- a modelagem baseada em árvores capturou melhor os padrões do problema
- a aplicação de PCA não trouxe ganho de desempenho neste caso
- o projeto mostra um pipeline completo de classificação supervisionada aplicado a um problema de negócio

## Tecnologias utilizadas

- Python
- Pandas
- NumPy
- Plotly
- Scikit-learn
- Jupyter Notebook

