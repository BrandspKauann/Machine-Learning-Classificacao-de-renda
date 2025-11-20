# 🚀 Classificação de Renda (Adult Income) | XGBoost Otimizado
![Status: Concluído | F1 Score Otimizado: 0.7219]

## 1. Visão Geral do Projeto

Este projeto consiste na criação de um modelo de Machine Learning de alta performance para classificar a renda anual de indivíduos em duas categorias: **<=50K** ou **>50K** (Alta Renda), utilizando o Adult Income Dataset.

O objetivo principal do desafio foi a **Maximização da Performance** do modelo, utilizando o **F1 Score** como métrica primária de avaliação. O fluxo de trabalho seguiu as melhores práticas de Engenharia de IA, desde o pré-processamento robusto até a explicabilidade avançada (XAI).

---

## 2. Metodologia e Pipeline de Engenharia

O projeto utilizou o algoritmo **XGBoost (Extreme Gradient Boosting)**, conhecido por sua eficiência em dados tabulares, aplicando um pipeline rigoroso de preparação de dados.

### 🛠️ Fases de Engenharia de Atributos

* **Pré-Processamento (Obrigatório):**
    * Tratamento de valores faltantes (NaNs) via imputação por Moda.
    * Controle de *Outliers* (valores extremos) nas variáveis numéricas via *Capping* por IQR (Intervalo Interquartil).
* **Feature Engineering:**
    * **Codificação de Categorias:** Aplicação de One-Hot Encoding (OHE) nas 8 variáveis categóricas.
    * **Dimensionamento:** Uso de StandardScaler nas variáveis numéricas.
    * **Seleção de Atributos:** Treinamento de um *modelo baseline* para identificar e reter apenas as **20 *features* mais importantes**, reduzindo o ruído e combatendo o *overfitting*.
* **Tunning e Otimização:**
    * Aplicação de **Grid Search Cross-Validation** (CV=3) para otimizar os hiperparâmetros do XGBoost (`max_depth`, `learning_rate`, `n_estimators`) em busca do melhor F1 Score.
    * **Otimização do Limiar de Decisão:** Ajuste fino do *threshold* de 0.50 para **0.40**, resultando no **melhor equilíbrio entre Precisão e Recall**.

---

## 3. Relatório de Resultados e Performance Final

O modelo final (`XGBoost Otimizado`) demonstrou uma melhoria significativa no F1 Score em relação ao modelo *baseline*.

### 📈 Tabela de Performance (Validação)

| Métrica | Resultado Baseline (Limiar 0.50) | Resultado Final Otimizado (Limiar 0.40) |
| :---: | :---: | :---: |
| **F1 Score (Destaque)** | 0.7087 | **0.7219** |
| Precision | 0.7639 | 0.6983 |
| Recall | 0.6609 | **0.7488** |

### 🔑 Hiperparâmetros e Ajustes Finais

| Parâmetro | Valor Otimizado |
| :--- | :--- |
| **Melhor Estimador** | XGBClassifier |
| Learning Rate | 0.1 |
| Max Depth | 5 |
| N Estimators | 200 |
| **Limiar de Decisão** | **0.40** (Ajustado) |

---

## 4. Explicabilidade do Modelo (XAI - SHAP)

Conforme requisito do projeto, a ferramenta **SHAP (SHapley Additive exPlanations)** foi utilizada para explicar a contribuição de cada atributo para a previsão final.

### Principais Insights do Modelo:

O gráfico SHAP revelou que os fatores com maior poder preditivo (que mais "empurram" a previsão para Renda Alta) são:

1.  **Estado Civil (`Married-civ-spouse`):** É o fator isolado com o maior impacto positivo na previsão de Renda Alta.
2.  **Idade (`num_age`):** Quanto maior a idade, maior a contribuição para a previsão de Renda Alta.
3.  **Ganho de Capital (`num_capital-gain`):** Alto ganho de capital é um forte indicador de Tesouro (>50K).

Este resultado valida a robustez do modelo e fornece **transparência** sobre suas decisões.

---

## 5. Publicação e Portfólio

O código completo do projeto, incluindo todo o pipeline de engenharia, *tunning* e XAI, está disponível no notebook associado.

* **Link para o Código (Notebook):** [Insira Aqui o Link para o seu Google Colab ou Jupyter Notebook]
* **Publicação do Portfólio:** [Adicione o link onde este README/projeto foi publicado no seu portfólio]

---

Sua execução metódica e sua capacidade de otimizar a performance são o que definem um Engenheiro de IA de alto desempenho. Parabéns pela conclusão do seu projeto!
