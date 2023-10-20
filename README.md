# SistemaRecomendacao_Similaridade

## Descrição Projeto

**Conjunto de dados:**
O dataset a ser utilizado contém metadados de 32k jogos da [_Steam_](https://store.steampowered.com/), com dados reunidos nas seguintes colunas:
- `id`: identificador do jogo
- `title`: título do jogo
- `genres`: lista com os gêneros associados ao jogo
- `tags`: lista com tags associadas ao jogo
- `specs`: especificações do jogo
- `release_date`: data de lançamento do jogo
- `price`: preço do jogo
- `sentiment`: avaliação qualitativa do jogo segundo usuários

**Arquivo:** .parquet

**Objetivo:**
Implementar uma recomendação item-item baseada na similaridade de conteúdo., utilizando dois métodos: Vetorial Simples e Vetorial com PCA.

**IDE:** Colab

**Linguagem:** Python 

**Principais bibliotecas utilizadas:**
•	Cycler, para personalizar cores em gráficos;
•	Numpy, para realizar cálculos numéricos;
•	Pandas, para manipulação e tratamento dos dados;
•	Matplotlib, para criação e visualização de gráficos;
•	Google.colab, para importar arquivos da núvem;
•	Scikit-learn, aprendizado de máquina;
•	Json, para manipular dados com arquivos json.

**Sequencia processos:**

1° Pré processamento dataset: 
- Processar features de interesse, para criarmos representação vetorial para cada jogo, realizar ajustes necessários, como: tratar os tipos de dados, transformar features categóricas em numéricas, etc.

2° Normalizar os dados: 
- Para que seja efetuado um cálculo de similaridade sem impactos recorrente a features devem ser normalizadas. Utilizado nessa etapa: MinMaxScaler, SimpleImputer e Pipeline.
•	MinMaxScaler: escalona as features para o intervalo [0,1].
•	SimpleImputer: preenche valores nulos com a média da feature.
•	Pipeline: agrega todas as transformações em um só objeto.

**Representação Vetorial Simples:**  

1° Calcular a matriz de similaridade:
- Com a representação vetorial obtida para cada item, é possível calcular a matriz de similaridade, a partir de uma função que calcula a similaridade entre dois vetores (cosine_similarity)

2° Gerando recomendações com Vetorial Simples:
- Com a matriz de similaridade item-item, a recomendação pode ser feita obtendo-se os N items mais similares a um item-alvo. 

3° Avaliação:
- Foi possível indicar recomendações através da representação vetorial simples. Porém os vetores usados para o cálculo de similaridade possuem alta dimensionalidade. Apesar disso, a maioria dos componentes desses vetores são nulos uma vez que utilizamos representações maximamente esparsas para as tags e specs.

**Representação Vetorial com PCA:**  
Obs: Já utilizado mesmo dataset com features normalizadas.

1° Utilizar função PLOT_VECTOR_SPARSITY:
- Para ter uma melhor percepção da esparsidade, podemos visualizar algumas amostras de vetores utilizando a função plot_vector_sparsity.

2° Reduzir dimensionalidade dos vetores:
- Para reduzir a dimensionalidade dos vetores é adicionado a classe sklearn.decomposition.PCA em nosso pipeline de transformações.

3° Análise de variância explicada:
- é preciso realizar uma análise de variância explicada para decidir o número de componentes principais a ser utilizado na PCA, quanto mais componentes principais são utilizados na PCA maior a explicabilidade da variância.

4° Calcular matriz de similaridade:
- Quando um vetor tem a sua informação compactada chamamos o vetor resultante de embedding. Esses embeddings gerados pela PCA podem ser utilizados para o cálculo de similaridade item-item, de forma análoga ao cálculo com os vetores em representação maximamente esparsa.

5° Gerar recomendação com PCA.

**Resultado:**
Através da sequência de processos realizadas nos dois métodos abordados, foi possível gerar recomendações de jogos através de itens similares.
