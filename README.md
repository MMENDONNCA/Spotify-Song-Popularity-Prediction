# Spotify - Previsão de Popularidade de Músicas

Um projeto de **Machine Learning** para classificar o sucesso de uma música com base em suas características sonoras.

---

## Índice
1. [Contexto do Projeto](#contexto-do-projeto)  
2. [Análise Exploratória de Dados (EDA) - Principais Insights](#análise-exploratória-de-dados-eda---principais-insights)  
3. [Pré-processamento e Modelagem](#pré-processamento-e-modelagem)  
4. [Resultados e Comparação de Modelos](#resultados-e-comparação-de-modelos)  
5. [Conclusão](#conclusão)  
6. [Ferramentas Utilizadas](#ferramentas-utilizadas)  
7. [Autor](#autor)  

---

## 1. Contexto do Projeto
A indústria musical é um mercado extremamente competitivo e saturado. Diariamente, milhares de novas músicas são lançadas, mas apenas uma pequena fração atinge um nível significativo de popularidade. Para gravadoras, artistas e curadores de playlists, entender os ingredientes de um "hit" é um desafio que vale milhões.

Este projeto busca resolver esse desafio através da ciência de dados.  
O objetivo é construir e avaliar um **modelo de Machine Learning de classificação** capaz de prever se uma música tem potencial para se tornar um sucesso, com base exclusivamente em suas características sonoras quantificáveis, como **dançabilidade, energia, tom e valência**.

🔗 [Base de Dados](https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset)
---

## 2. Análise Exploratória de Dados (EDA) - Principais Insights

Antes da modelagem, uma análise profunda foi realizada para entender a natureza dos dados e extrair insights valiosos.

- **Definição de "Hit"**: Para transformar o problema em uma classificação binária, um "hit" foi definido como qualquer música pertencente ao **Top 10% de popularidade** do dataset. Com base na distribuição, isso corresponde a um score de popularidade >= 63.  

- **Desbalanceamento de Classes**: A análise revelou um forte desbalanceamento entre as classes, refletindo a realidade do mercado: existem muito mais músicas "não populares" do que hits.  

- **A "Assinatura Sonora" de um Hit**:  
  Músicas de sucesso tendem a ser:  
  - Mais **Dançantes** (*danceability*) e **Energéticas** (*energy*)  
  - Mais **Altas** (*loudness*)  
  - Significativamente menos **Acústicas** (*acousticness*) e **Instrumentais** (*instrumentalness*)  

- **Correlações**: Nenhuma característica sonora sozinha possui correlação forte o suficiente para prever o sucesso, reforçando a necessidade de um modelo capaz de aprender com a interação entre múltiplas **features**.

---

## 3. Pré-processamento e Modelagem

A preparação dos dados para o treinamento seguiu as melhores práticas:

1. **Limpeza e Seleção de Features**: Remoção de colunas não informativas (IDs, nomes, datas).  
2. **Pré-processamento Avançado**: Utilização de `ColumnTransformer` para aplicar tratamentos distintos por tipo de variável.  
   - **Numéricas**: Normalizadas com `StandardScaler`.  
   - **Categóricas** (`key`, `time_signature`): Convertidas com `OneHotEncoder`.  
3. **Divisão dos Dados**: 80% treino e 20% teste, utilizando `stratify` para manter a proporção de classes.  
4. **Modelos Testados**: Regressão Logística, Random Forest e XGBoost.  

---

## 4. Resultados e Comparação de Modelos

A performance de cada modelo foi avaliada com foco na identificação da classe **'popular'**.  
O **Random Forest** foi o vencedor, apresentando melhor equilíbrio entre as métricas.

| Modelo                | Precision (popular) | Recall (popular) | F1-Score (popular) |
|------------------------|---------------------|------------------|--------------------|
| Regressão Logística    | 0.00                | 0.00             | 0.00               |
| Random Forest (Baseline) | 0.93              | 0.55             | 0.69               |
| XGBoost               | 0.80                | 0.08             | 0.14               |

### Otimizando o Random Forest
Para melhorar o **recall**, o modelo foi re-treinado com `class_weight='balanced'`.

| Versão do Random Forest | Precision (popular) | Recall (popular) | F1-Score (popular) |
|--------------------------|---------------------|------------------|--------------------|
| Baseline                 | 0.93                | 0.55             | 0.69               |
| Com `class_weight`       | 0.82                | 0.57             | 0.68               |

🔹 O ajuste aumentou o recall (55% → 57%), mas reduziu a precisão (93% → 82%), evidenciando o **trade-off clássico em Machine Learning**.

---

## 5. Conclusão

A análise mostrou que é possível prever o potencial de sucesso de uma música com um bom grau de confiança usando apenas suas características sonoras.  
O **Random Forest** superou a Regressão Logística e o XGBoost.

- Para tarefas que exigem **alta confiança** (ex: criar playlists "Top Hits"), o **modelo baseline** é ideal.  
- Para tarefas de **descoberta** (ex: caça-talentos), o modelo ajustado com `class_weight` é mais útil, mesmo com mais falsos positivos.  

### Próximos Passos
- **Ajuste de Hiperparâmetros**: Utilizar `GridSearchCV` ou `RandomizedSearchCV`.  
- **Engenharia de Features**: Incluir informações sobre o artista (ex: número de seguidores) ou aplicar **NLP** às letras.  

---

## 6. Ferramentas Utilizadas
- **Linguagem**: Python  
- **Bibliotecas**: Pandas, NumPy, Scikit-learn, XGBoost, Matplotlib, Seaborn  
- **Ambiente**: Google Colab  

---

## 7. Autor
Matheus Mendonça Sucupira Lima  

🔗 [LinkedIn](www.linkedin.com/in/matheusmendoncasucupira)  
🔗 [GitHub](https://github.com/MMENDONNCA)  

