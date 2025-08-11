# knn-fraude
# Detecção de Fraudes Financeiras com KNN Otimizado

## Visão Geral do Projeto

Este projeto demonstra um pipeline completo de Machine Learning para a construção de um modelo de detecção de fraudes em transações financeiras. O desafio central é o severo desbalanceamento de classes no dataset, onde as transações fraudulentas representam menos de 0.2% do total.

O objetivo foi otimizar o algoritmo K-Nearest Neighbors (KNN), frequentemente considerado inadequado para tais cenários, e transformá-lo em um classificador de alta performance com um equilíbrio funcional entre a detecção de fraudes (Recall) e a confiabilidade dos alertas (Precisão).

## Dataset

O conjunto de dados utilizado é o "Synthetic Financial Datasets For Fraud Detection" da plataforma Kaggle. Ele contém dados sintéticos de transações financeiras, modelados a partir de dados reais.

- **Link para o Dataset:** [Kaggle](https://www.kaggle.com/datasets/ealaxi/paysim1)

## Metodologia Aplicada

O pipeline desenvolvido seguiu uma abordagem metodológica rigorosa para garantir um resultado robusto e defensável:

1.  **Engenharia de Features:** Criação de novas features (`erro_saldo_origem`, `erro_saldo_destino`) para capturar anomalias nos balanços das contas que não são explícitas nos dados originais.
2.  **Divisão Estratégica:** O dataset foi dividido em conjuntos de treino (80%) e teste (20%) usando amostragem estratificada, garantindo que o conjunto de teste (hold-out) permanecesse como uma representação fiel do "mundo real".
3.  **Escalonamento (Scaling):** As features foram padronizadas usando `StandardScaler`, ajustado apenas no conjunto de treino para evitar vazamento de dados.
4.  **Otimização de Hiperparâmetros:** Foi utilizado o `GridSearchCV` para encontrar a melhor combinação de hiperparâmetros para o KNN (`n_neighbors`, `weights`, `p`), otimizando diretamente pela métrica **F1-Score**.
5.  **Ajuste Fino do Limiar de Decisão:** Após treinar o melhor modelo, foi gerada a Curva Precisão-Recall para identificar o limiar de decisão (`threshold`) que maximiza o F1-Score, calibrando o modelo para o ponto de equilíbrio ideal.

## Resultados Finais

O modelo final, após todas as otimizações, alcançou um excelente equilíbrio entre a detecção de fraudes e a geração de alertas confiáveis.

| Métrica (Classe Fraude) | Pontuação |
| :--- | :--- |
| **Recall (Sensibilidade)** | 89.8% |
| **Precisão** | 91.6% |
| **F1-Score (Equilíbrio)**| 90.7% |

Este resultado demonstra que, com a metodologia correta, é possível construir um modelo KNN de alta performance, mesmo em um cenário de dados extremamente desbalanceado.

## Como Executar

1.  Clone este repositório.
2.  Certifique-se de ter as bibliotecas listadas no notebook instaladas (`pandas`, `numpy`, `scikit-learn`, `matplotlib`, `seaborn`).
3.  Coloque o arquivo `PS_20174392719_1491204439457_log.csv` no mesmo diretório.
4.  Execute o notebook Jupyter `analise_fraude_knn.ipynb` célula por célula.
