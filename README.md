# Clusterização de Bisnagas: Eficiência Operacional na Indústria de Cosméticos

## 📄 Sobre o Projeto
Este projeto aplica técnicas de **Aprendizagem de Máquina Não Supervisionada** para mapear e compreender perfis de grupos em um portfólio de mais de 2.000 SKUs de bisnagas. A análise foca em características físicas e técnicas para transformar a performance operacional.
* **Ganho de Produtividade:** Internalização ( retirando de terceiros) de **7% no volume produtivo** através otimização nos roteiros produtivos (cadência e tempo de setup).
* **Retorno Financeiro:** Impacto estimado de **R$ 1,5 milhão em receita**

* 
### 🚀 Impactos nos Indicadores (KPIs)
* **Redução do Lead Time:** Otimização do tempo de resposta da cadeia de suprimentos.
* **Eficiência Produtiva:** Minimização do tempo de **setup de máquinas** ao agrupar e sequenciar itens com características de envase similares.
* **Otimização de Processo:** Otimização dos roteiros de produção baseando-se em análises comparativas de SKU de características similares num mesmo cluster
* **Padronização de Componentes:** Identificação de redundâncias no portfólio de embalagens.

> **Nota:** Os dados originais não estão disponíveis por se tratar de um projeto corporativo confidencial.

## 🛠 Tecnologias e Ferramentas
| Categoria | Tecnologias Utilizadas |
| :--- | :--- |
| **Linguagem** | Python 3.14+ |
| **Manipulação** | Pandas, Numpy |
| **Visualização** | Matplotlib, Seaborn |
| **Modelagem** | Scikit-learn, Scipy (Cluster, Stats) | K-MEANS,  Hierárquico (Ward)
| **Artefatos** | PyArrow, Fastparquet (Arquivos .parquet) |

## ⚙️ Metodologia e Definição do K Ótimo
O projeto utiliza uma abordagem robusta para determinar o número ideal de clusters (K), cruzando o contexto do negócio e métodos estatísticos, e iterativos:

1. **Método da Silhueta (Silhouette Score):** Utilizado para medir a qualidade da separação entre os clusters. Avalia o quão similar um objeto é ao seu próprio cluster em comparação com outros, buscando maximizar a coesão interna.
2. **Método de Mojena:** Aplicado na clusterização hierárquica para determinar o ponto de corte ideal no dendrograma, utilizando o critério baseado no desvio padrão das distâncias de fusão.
3. **Métricas Complementares:** Uso de **DB Index (Davies-Bouldin)** e **Correlação Cofenética** para validar a consistência da estrutura hierárquica.

## 📂 Estrutura de Diretórios
```text
Cluster/
├── data/                            # Datasets Intermediários
│   ├── df_bis_clusters.csv          # Fonte original (CSV)
│   ├── data_cleaned.parquet         # Dados limpos (Output Notebook 01)
│   ├── data_cleaned_with_ids.parquet# Dados + IDs (Output Notebook 02)
│   └── data_features.parquet        # Features preparadas (Output Notebook 02)
├── models/                          # Artefatos por Experimento
│   ├── hierar_k47_comp/             
│   │   ├── modelo.pkl               # Modelo treinado
│   │   ├── metricas.json            # Resultados de performance
│   │   └── pca_clusters.png         # Visualização de clusters
│   └── ...                          # (Total de 8 subpastas de cenários)
└── notebook/                        # Fluxo de Trabalho Modular
    ├── cluster_bis.ipynb            # Notebook Original (Referência)
    ├── 01_eda_limpeza.ipynb         # Etapa 1: Limpeza e EDA
    ├── 02_features.ipynb            # Etapa 2: Feature Engineering
    ├── 03_otimizacao_k.ipynb        # Etapa 3: Estudo de K (Silhueta/Mojena)
    └── 04_modelagem.ipynb           # Etapa 4: Treinamento e Perfis
