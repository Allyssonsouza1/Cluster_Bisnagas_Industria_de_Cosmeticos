# Clusterização de Bisnagas: Eficiência Operacional na Indústria de Cosméticos

## 📄 Sobre o Projeto
Este projeto aplica técnicas de **Aprendizagem de Máquina Não Supervisionada** para mapear e compreender perfis de grupos em um portfólio de mais de **2.000 SKUs de bisnagas**. A análise foca em características físicas e técnicas para transformar a performance operacional.

![Objeto de Estudo](https://raw.githubusercontent.com/Allyssonsouza1/Cluster_Bisnagas_Industria_de_Cosmeticos/main/paper/obj_estudo%20.png)

🎓 Este projeto é a resolução de um **problema real da indústria** e foi utilizado como trabalho de conclusão da especialização em **Data Science e Big Data pela UFPR**. Para uma visão completa da metodologia e resultados, [acesse o artigo completo aqui](https://github.com/Allyssonsouza1/Cluster_Bisnagas_Industria_de_Cosmeticos/blob/main/paper/DSBD_UFPR_Cluster_Allyson.pdf).

### 🚀 Impactos nos Indicadores (KPIs)
* **Ganho de Produtividade:** Internalização ( retirando de terceiros) de **7% no volume produtivo** através otimização nos roteiros produtivos (cadência e tempo de setup).
* **Retorno Financeiro:** Impacto estimado de **R$ 1,5 milhão em receita**
* **Eficiência Produtiva:** Minimização do tempo de **setup de máquinas** ao agrupar e sequenciar itens com características de envase similares.
* **Otimização de Processo:** Otimização dos roteiros de produção baseando-se em análises comparativas de SKU de características similares num mesmo cluster

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

   
## 📊 Resultados dos Cenários de Clusterização

| Cen. | Método      | K  | Conj. Dados | Silhueta | DBI    | Corr. Cofenética |
|------|-------------|----|-------------|----------|--------|------------------|
| C1   | Hierárquico | 47 | Conjunto 1  | 0,5582   | 0,8128 | 0,7216           |
| C2   | Hierárquico | 47 | Conjunto 2  | 0,5578   | 0,6119 | 0,8060           |
| C3   | Hierárquico | 65 | Conjunto 1  | 0,5872   | 0,7268 | 0,7216           |
| C4   | Hierárquico | 65 | Conjunto 2  | 0,5746   | 0,5195 | 0,8060           |
| C5   | K-Means     | 47 | Conjunto 1  | 0,5386   | 0,7893 | N/A              |
| C6   | K-Means     | 47 | Conjunto 2  | 0,5453   | 0,5688 | N/A              |
| C7   | K-Means     | 65 | Conjunto 1  | 0,5728   | 0,6218 | N/A              |
| C8   | K-Means     | 65 | Conjunto 2  | 0,5733   | 0,5240 | N/A              |

---

## 🏆 Conclusão e Modelo Final

O **Cenário C8** (K-Means, K=65, sem a variável comprimento) foi selecionado como o modelo de produção pelos seguintes motivos:

- **Melhor Separação:** Apresentou o menor índice de dispersão (DBI `0,5240`) entre os modelos com K=65.
- **Equilíbrio:** Manteve uma Silhueta alta (`0,5733`), superando a dispersão excessiva observada no modelo hierárquico C3.
- **Robustez Operacional:** A remoção da variável redundante (comprimento) resultou em famílias mais homogêneas e tecnicamente coerentes para o processo produtivo.
- **Impacto:** A definição destas 65 famílias elimina a subjetividade no sequenciamento, otimiza o OEE e permite a redução drástica de setups de máquina.

### Principais Ganhos

1. Substituição da experiência subjetiva por rigor estatístico.
2. Mapeamento de **65 grupos acionáveis** para gestão industrial.
3. Fundamentação para aumento de **7% no volume produtivo** via internalização.
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
