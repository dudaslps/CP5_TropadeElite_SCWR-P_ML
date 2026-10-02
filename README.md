# Checkpoint 5 – Statistical Computing + Machine Learning (Dataset Wine)

Trabalho do **Checkpoint 5 (2º semestre)** do curso de Tecnólogo em Inteligência Artificial da FIAP. O projeto integra **análise estatística descritiva e probabilística** com **modelagem não supervisionada (K-means)** sobre o dataset Wine.

## Integrantes

| Nome | RM |
| --- | --- |
| Arthur Costa Donaire | RM571283 |
| Felipe Pereira de Jesus | RM573263 |
| Giovanna Pereira de Oliveira | RM570989 |
| Gustavo Paiva Silva | RM572249 |
| Maria Eduarda Soares Lopes e Souza | RM572612 |

## Dataset

- **Fonte:** [Wine Dataset for Clustering (Kaggle, harrywang)](https://www.kaggle.com/datasets/harrywang/wine-dataset-for-clustering)
- **Tamanho:** 178 vinhos e 14 colunas, sem valores nulos.
- **Colunas:** `Wine` (classe original: 1, 2 ou 3) e 13 medidas químicas quantitativas: `Alcohol`, `Malic.acid`, `Ash`, `Acl`, `Mg`, `Phenols`, `Flavanoids`, `Nonflavanoid.phenols`, `Proanth`, `Color.int`, `Hue`, `OD` e `Proline`.

## O que o projeto faz

### Parte 1 – Statistical Computing (Python)

Foram escolhidas duas variáveis quantitativas com comportamentos opostos: **Alcohol** (baixa dispersão relativa) e **Malic.acid** (alta dispersão relativa).

- **(a) Visualização:** tabela de distribuição de frequências (9 classes, com frequência absoluta, relativa e acumuladas) e histograma com média e mediana.
- **(b) Análise descritiva:** média, mediana, moda, mínimo, máximo, amplitude, variância, desvio padrão, coeficiente de variação e quartis (Q1, Q2, Q3, IQR).
- **(c) Análise probabilística:** distribuição Normal (média e desvio padrão amostrais) e quatro cálculos, dois por variável, comparados com a frequência empírica.

### Parte 2 – Machine Learning (K-means)

- Remoção da coluna `Wine` (a classe original não é usada no agrupamento).
- Padronização das 13 variáveis com `StandardScaler`.
- Escolha de k entre 2 e 8 pelos métodos **Elbow** e **Silhouette**.
- Ajuste final com **k = 3** e análise do perfil de cada cluster.

## Principais resultados

### Estatística descritiva

| Medida | Alcohol | Malic.acid |
| --- | --- | --- |
| Média | 13,0006 | 2,3363 |
| Mediana | 13,0500 | 1,8650 |
| Desvio padrão | 0,8118 | 1,1171 |
| **Coef. de variação** | **6,24%** | **47,82%** |
| Q1 / Q3 | 12,36 / 13,68 | 1,60 / 3,08 |
| IQR | 1,3150 | 1,4800 |

Alcohol é homogêneo e aproximadamente simétrico (média próxima da mediana). Malic.acid é heterogêneo e assimétrico à direita (média maior que a mediana).

### Probabilidades (Normal × frequência empírica)

| Variável | Cálculo | Normal (%) | Empírica (%) |
| --- | --- | --- | --- |
| Alcohol | P(X > 13,5) | 26,92 | 30,90 |
| Alcohol | P(12,5 < X < 14,0) | 62,21 | 55,62 |
| Malic.acid | P(X > 3,0) | 27,62 | 26,40 |
| Malic.acid | P(1,5 < X < 2,5) | 33,12 | 46,07 |

A Normal é uma aproximação razoável para Alcohol e limitada para Malic.acid, cuja assimetria à direita faz o intervalo central ser subestimado em cerca de 13 pontos percentuais.

### Clusters (K-means, k = 3)

O maior Silhouette Score ocorreu em **k = 3 (0,2849)**, e o Elbow mostrou queda acentuada da inércia até três grupos.

| Cluster | n | Alcohol | Malic.acid | Color.int | Proline | Perfil |
| --- | --- | --- | --- | --- | --- | --- |
| 0 | 65 | 12,25 | 1,90 | 2,97 | 510,17 | Menor álcool, cor mais clara e menor Proline |
| 1 | 51 | 13,13 | 3,31 | 7,23 | 619,06 | Maior Malic.acid e maior intensidade de cor |
| 2 | 62 | 13,68 | 2,00 | 5,45 | 1100,23 | Maior álcool, Proline muito alto e mais fenóis |

O valor de Silhouette é modesto, o que indica grupos com alguma sobreposição.

## Estrutura do repositório

Ajuste os nomes conforme o seu repositório.

```text
.
├── Checkpoint5_Wines.ipynb      # notebook com a análise completa
├── wine.csv                     # dataset (baixar do Kaggle)
├── Checkpoint5_Relatorio.pdf    # relatório do trabalho
├── requirements.txt             # dependências
└── README.md
```

## Como executar

1. Baixe o dataset no [Kaggle](https://www.kaggle.com/datasets/harrywang/wine-dataset-for-clustering) e salve o arquivo como `wine.csv` na mesma pasta do notebook.
2. Crie um ambiente e instale as dependências:

```bash
python -m venv .venv
source .venv/bin/activate        # no Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

3. Abra e execute o notebook:

```bash
jupyter notebook Checkpoint5_Wines.ipynb
```

`requirements.txt`:

```text
numpy
pandas
matplotlib
scipy
scikit-learn
jupyter
```

Os resultados são reproduzíveis: o K-means usa `random_state=42` e `n_init=10`.

## Tecnologias

Python, pandas, NumPy, SciPy (`scipy.stats.norm`), Matplotlib e scikit-learn (`StandardScaler`, `KMeans`, `silhouette_score`).

## Limitações e próximos passos

- Não foi aplicado teste formal de normalidade; a Normal foi usada como aproximação teórica.
- A análise estatística cobre apenas duas variáveis.
- O Silhouette moderado sugere sobreposição entre os clusters.
- Próximos passos: testes de normalidade, distribuições assimétricas para Malic.acid e comparação dos clusters com a classe original (`Wine`).
