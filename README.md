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

## 5. Conclusão: Desafios e Tomadas de Decisão

O sucesso deste projeto não residiu apenas na aplicação de um algoritmo robusto (XGBoost), mas principalmente nas **decisões estratégicas de Engenharia de IA** tomadas em cada etapa do pipeline:

* **Desafio da Qualidade dos Dados (Outliers):** A principal decisão de Engenharia de Dados foi evitar a exclusão de *outliers* em colunas críticas como `capital-gain`. A exclusão teria removido exemplos raros, mas vitais, da classe minoritária (`>50K`). Optamos pelo **Capping via IQR** para controlar a escala sem perder a informação binária da alta riqueza.
* **Controle de Complexidade (Seleção de Atributos):** Após o One-Hot Encoding expandir o *dataset* para 108 *features*, foi crucial empregar a **Seleção de Atributos** baseada na importância do XGBoost. Retivemos apenas as 20 *features* mais preditivas, simplificando o modelo, reduzindo o risco de *overfitting* e acelerando o *tunning*.
* **Otimização do F1 Score (Limiar de Decisão):** O desafio final de maximização do F1 Score foi superado não apenas pelo *tunning* de hiperparâmetros, mas pela otimização do **Limiar de Decisão**. O ajuste do *threshold* padrão de 0.50 para **0.40** permitiu que o modelo se tornasse estrategicamente mais agressivo, aumentando o **Recall** (achando mais Renda Alta real) e elevando o F1 Score final para **0.7219**.
* **Atendimento à Explicabilidade (XAI):** Para abordar o desafio de **interpretabilidade** inerente aos modelos de *ensemble* (XGBoost), aplicamos a técnica **SHAP**. Isso permitiu não só validar os *insights* do modelo mas também cumprir o requisito fundamental de fornecer **transparência e justificação** para as decisões do modelo.

Este processo demonstra a capacidade de transformar requisitos de negócio em decisões técnicas que garantem o melhor desempenho e a robustez do modelo.
