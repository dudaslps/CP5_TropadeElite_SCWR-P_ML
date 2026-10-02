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

- **Problema e solução:** agrupar 178 vinhos por semelhança química, sem usar a classe original, com K-means.
- **Pré-processamento:** remoção da coluna `Wine` (a classe original), verificação de nulos (não há) e padronização das 13 variáveis com `StandardScaler`.
- **Número de grupos:** k entre 2 e 8 pelos métodos **Elbow** e **Silhouette**, com k = 3 marcado nos gráficos.
- **Ajuste final** com **k = 3** e análise do perfil de cada cluster, respondendo às perguntas do enunciado (teor alcoólico de cada grupo, grupo mais ácido e o que diferencia os grupos).

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

| Cluster | n | Alcohol | Malic.acid | Ash | Flavanoids | Color.int | Proline | Perfil |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0 | 65 | 12,25 | 1,90 | 2,23 | 2,05 | 2,97 | 510,17 | Leve: menor álcool, cor mais clara, menor Proline e menor cinza |
| 1 | 51 | 13,13 | 3,31 | 2,42 | 0,82 | 7,23 | 619,06 | Ácido e colorido: maior Malic.acid, cor mais intensa e menos flavonoides |
| 2 | 62 | 13,68 | 2,00 | 2,47 | 3,00 | 5,45 | 1100,23 | Alcoólico e encorpado: maior álcool, Proline muito alto e mais fenóis |

- **Teor alcoólico:** 12,25 (Cluster 0), 13,13 (Cluster 1) e 13,68 (Cluster 2).
- **Grupo mais ácido:** Cluster 1 (Malic.acid médio de 3,31, usado como referência de acidez).
- **Cinza (`Ash`):** separa pouco os grupos (2,23 a 2,47); Proline, cor e flavonoides diferenciam mais.

O valor de Silhouette é modesto, o que indica grupos com alguma sobreposição.

## Estrutura do repositório

Ajuste os nomes conforme o seu repositório.

```text
.
├── CP5_TropadeElite_SCWRP_ML_Wines.ipynb   # notebook: Statistical Computing + Machine Learning
├── CP5_Relatorio_TropadeElite_SCWRPML.pdf  # relatório do trabalho
├── wine.csv                                # dataset (baixar do Kaggle)
├── requirements.txt                        # dependências
└── README.md
```

## Como executar

Baixe o dataset no [Kaggle](https://www.kaggle.com/datasets/harrywang/wine-dataset-for-clustering) e salve o arquivo como `wine.csv` (o notebook também aceita `wines.csv`) na mesma pasta do notebook.

### Localmente (Jupyter)

```bash
python -m venv .venv
source .venv/bin/activate        # no Windows: .venv\Scripts\activate
pip install -r requirements.txt
jupyter notebook CP5_TropadeElite_SCWRP_ML_Wines.ipynb
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

### No Google Colab

Envie o notebook em *Arquivo > Fazer upload de notebook*, execute tudo (*Ambiente de execução > Executar tudo*) e, quando solicitado, selecione o `wine.csv`. As bibliotecas já estão instaladas no Colab.

Os resultados são reproduzíveis: o K-means usa `random_state=42` e `n_init=10`.

## Tecnologias

Python, pandas, NumPy, SciPy (`scipy.stats.norm`), Matplotlib e scikit-learn (`StandardScaler`, `KMeans`, `silhouette_score`).

## Limitações e próximos passos

- Não foi aplicado teste formal de normalidade; a Normal foi usada como aproximação teórica.
- A análise estatística cobre apenas duas variáveis.
- O Silhouette moderado sugere sobreposição entre os clusters.
- Próximos passos: testes de normalidade, distribuições assimétricas para Malic.acid e comparação dos clusters com a classe original (`Wine`).
