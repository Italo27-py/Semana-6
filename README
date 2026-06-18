# Comparação entre Modelos de Machine Learning para Previsão de Churn

## 1. Introdução

Este projeto tem como objetivo comparar dois modelos de Machine Learning utilizados para prever o **churn de clientes bancários**, ou seja, identificar clientes com maior probabilidade de deixar o banco.

Foram analisados dois notebooks diferentes:

- **Projeto 1:** Random Forest;
- **Projeto 2:** Árvore de Decisão.

Os dois projetos utilizam uma base de dados com aproximadamente **10.000 clientes**, contendo informações como idade, país, gênero, saldo bancário, número de produtos contratados e status de churn.

---

## 2. Distribuição da variável alvo

A variável alvo utilizada nos dois projetos foi `churn`.

| Situação do cliente | Percentual aproximado |
|---|---:|
| Permaneceu no banco | 79,63% |
| Deixou o banco | 20,37% |

A base está **desbalanceada**, pois há muito mais clientes que permaneceram no banco do que clientes que saíram. Por isso, não é suficiente analisar apenas a acurácia. Também devem ser consideradas precisão, recall, F1-score e AUC.

---

## 3. Modelos utilizados

### Projeto 1 — Random Forest

O primeiro projeto utiliza o algoritmo **Random Forest**, que combina várias árvores de decisão.

Foram avaliadas duas versões:

1. Random Forest inicial;
2. Random Forest ajustada, com alterações nos hiperparâmetros e balanceamento das classes.

### Projeto 2 — Árvore de Decisão

O segundo projeto utiliza uma única **Árvore de Decisão**. Esse modelo é mais simples e fácil de interpretar, mas pode apresentar maior risco de sobreajuste e resultados menos estáveis.

---

## 4. Comparação das métricas

| Métrica | Random Forest inicial | Random Forest ajustada | Árvore de Decisão |
|---|---:|---:|---:|
| Acurácia | 86,4% | **84,3%** | 77,0% |
| Precisão | 78,6% | **60,8%** | 45,6% |
| Recall | 45,2% | 63,6% | **67,3%** |
| F1-score | 57,4% | **62,2%** | 54,4% |
| AUC | 85,7% | **86,4%** | 82,1% |
| Acurácia no treino | 100% | 91,4% | Não apresentada |

---

## 5. Análise da Random Forest inicial

A Random Forest inicial apresentou:

- Acurácia de 86,4%;
- Precisão de 78,6%;
- Recall de 45,2%;
- F1-score de 57,4%;
- AUC de 85,7%.

O modelo apresentou boa acurácia e alta precisão. Isso significa que, quando classificava um cliente como provável churn, geralmente estava correto.

Entretanto, o recall foi baixo. O modelo identificou menos da metade dos clientes que realmente deixaram o banco.

Além disso, a acurácia de 100% no conjunto de treinamento indica um possível caso de **sobreajuste**, pois o modelo aprendeu muito bem os dados de treino, mas apresentou desempenho inferior nos dados de teste.

---

## 6. Análise da Random Forest ajustada

Depois dos ajustes, a Random Forest apresentou:

- Acurácia de 84,3%;
- Precisão de 60,8%;
- Recall de 63,6%;
- F1-score de 62,2%;
- AUC de 86,4%;
- Acurácia de 91,4% no treinamento.

Embora a acurácia tenha diminuído, o modelo passou a identificar uma quantidade maior de clientes que realmente deixariam o banco.

O recall aumentou de 45,2% para 63,6%. Também houve melhora no F1-score e na AUC, indicando um modelo mais equilibrado.

A diferença entre o desempenho no treinamento e no teste diminuiu, reduzindo os sinais de sobreajuste.

---

## 7. Comparação entre as duas versões da Random Forest

| Resultado | Random Forest inicial | Random Forest ajustada | Diferença |
|---|---:|---:|---:|
| Clientes que ficaram corretamente identificados | 1.543 | 1.426 | -117 |
| Falsos positivos | 50 | 167 | +117 |
| Clientes com churn não identificados | 223 | 148 | **-75** |
| Clientes com churn identificados | 184 | 259 | **+75** |

A Random Forest ajustada identificou 75 clientes a mais que realmente deixaram o banco. Ao mesmo tempo, produziu mais falsos positivos.

Isso representa uma troca entre precisão e recall:

- o modelo inicial era mais conservador;
- o modelo ajustado passou a detectar mais clientes em risco;
- em compensação, também passou a gerar mais alertas incorretos.

Para um problema de churn, reduzir falsos negativos costuma ser importante, pois deixar de identificar um cliente em risco pode representar perda financeira para a empresa.

---

## 8. Random Forest ajustada versus Árvore de Decisão

A Árvore de Decisão apresentou o maior recall:

- Árvore de Decisão: 67,3%;
- Random Forest ajustada: 63,6%.

Isso significa que a Árvore de Decisão identificou uma proporção ligeiramente maior dos clientes que realmente deixaram o banco. Porém, a Random Forest ajustada apresentou melhores resultados nas demais métricas.

| Indicador | Random Forest ajustada | Árvore de Decisão |
|---|---:|---:|
| Identificação de clientes com churn | 63,6% | **67,3%** |
| Clientes com churn não identificados | 36,4% | **32,7%** |
| Taxa de falsos positivos | **10,5%** | 20,5% |
| Precisão dos alertas de churn | **60,8%** | 45,6% |

A Árvore de Decisão encontrou um pouco mais de clientes em risco, mas produziu uma quantidade muito maior de falsos positivos.

Na prática, isso pode fazer o banco oferecer descontos, benefícios ou campanhas de retenção para clientes que não pretendiam sair.

A Random Forest ajustada apresentou melhor equilíbrio entre identificação de churn, redução de falsos positivos, precisão, F1-score e AUC.

---

## 9. Diferenças metodológicas entre os projetos

A comparação deve ser realizada com cuidado, pois os notebooks não utilizaram exatamente as mesmas configurações.

| Elemento | Projeto 1 | Projeto 2 |
|---|---|---|
| Algoritmo | Random Forest | Árvore de Decisão |
| Divisão dos dados | 80% treino e 20% teste | 70% treino e 30% teste |
| `random_state` | 42 | 0 |
| Codificação das categorias | One-Hot Encoding | Label Encoding |
| Remoção de `customer_id` | Sim | Não corretamente |
| Balanceamento das classes | `class_weight="balanced"` | `class_weight="balanced"` |
| Uso de Pipeline | Sim | Não |

Como os dois projetos utilizaram divisões diferentes dos dados, os modelos não foram avaliados exatamente sobre os mesmos clientes.

Para uma comparação mais justa, os dois modelos deveriam utilizar:

- a mesma divisão de treino e teste;
- o mesmo `random_state`;
- o mesmo pré-processamento;
- as mesmas variáveis de entrada;
- as mesmas métricas;
- validação cruzada.

---

## 10. Problemas encontrados no Projeto 1

A conclusão escrita no notebook apresenta métricas diferentes das métricas mostradas nas células executadas.

A conclusão menciona:

- Acurácia de 86,8%;
- Precisão de 78,2%;
- Recall de 48,4%;
- F1-score de 59,8%.

Porém, a saída executada apresenta:

- Acurácia de 86,4%;
- Precisão de 78,6%;
- Recall de 45,2%;
- F1-score de 57,4%;
- AUC de 85,7%.

Esses valores devem ser corrigidos para que a conclusão fique de acordo com os resultados reais do notebook.

---

## 11. Problemas encontrados no Projeto 2

### Uso incorreto de `customer_id`

O código cria uma versão da base sem a coluna `customer_id`:

```python
df = dataset.drop(columns=["customer_id"])
```

Porém, posteriormente, cria as variáveis de entrada utilizando novamente o DataFrame original:

```python
X = dataset.drop(columns=["churn"])
```

Dessa forma, a coluna `customer_id` continua sendo utilizada pelo modelo. Essa coluna deve ser removida, pois representa apenas um identificador.

A correção recomendada é:

```python
X = dataset.drop(columns=["customer_id", "churn"])
```

### Uso de Label Encoding em variáveis nominais

O Projeto 2 utiliza Label Encoding para transformar variáveis categóricas em números. Esse método pode criar uma ordem artificial entre categorias como França, Alemanha e Espanha.

Para esse tipo de variável, o One-Hot Encoding utilizado no Projeto 1 é mais adequado.

### Erro ao visualizar a árvore

O notebook apresenta o erro:

```text
NameError: name 'plot_tree' is not defined
```

A função precisa ser importada antes de ser utilizada:

```python
from sklearn.tree import plot_tree
```

---

## 12. Pontos positivos de cada projeto

### Projeto 1

O Projeto 1 apresentou maior consistência metodológica porque:

- removeu corretamente o identificador do cliente;
- utilizou One-Hot Encoding;
- organizou o pré-processamento e o modelo em uma Pipeline;
- avaliou sinais de sobreajuste;
- testou ajustes de hiperparâmetros;
- comparou métricas antes e depois dos ajustes;
- relacionou os resultados ao problema de negócio.

### Projeto 2

O Projeto 2 apresentou uma análise exploratória visual mais completa, incluindo:

- relação entre idade e churn;
- relação entre saldo e churn;
- relação entre score de crédito e churn;
- churn por país;
- churn por gênero;
- churn por quantidade de produtos;
- importância das variáveis;
- tentativa de visualização da árvore.

---

## 13. Modelo com melhor resultado

Considerando o conjunto de métricas, a **Random Forest ajustada apresentou o melhor resultado geral**.

Apesar de a Árvore de Decisão ter obtido recall ligeiramente maior, a Random Forest ajustada apresentou:

- maior acurácia;
- maior precisão;
- maior F1-score;
- maior AUC;
- menor proporção de falsos positivos;
- melhor equilíbrio entre as classes.

A redução da acurácia da Random Forest inicial para a ajustada não significa necessariamente uma piora. Como a base é desbalanceada, um modelo pode atingir alta acurácia apenas por prever corretamente a classe majoritária.

O modelo ajustado passou a reconhecer melhor os clientes com churn, tornando-se mais útil para o objetivo do projeto.

---

## 14. Conclusão

Os dois modelos apresentaram comportamentos diferentes na previsão de churn.

A Árvore de Decisão alcançou o maior recall, identificando 67,3% dos clientes que deixaram o banco, enquanto a Random Forest ajustada identificou 63,6%.

Entretanto, a Árvore de Decisão apresentou menor precisão, menor acurácia, menor F1-score e uma quantidade proporcionalmente maior de falsos positivos.

A Random Forest ajustada obteve:

- Acurácia de 84,3%;
- Precisão de 60,8%;
- Recall de 63,6%;
- F1-score de 62,2%;
- AUC de 86,4%.

Esses resultados demonstram maior equilíbrio entre a identificação de clientes em risco e a redução de alertas incorretos.

Portanto, considerando o conjunto das métricas, a **Random Forest ajustada foi considerada o modelo mais adequado para o problema de churn**.

Entretanto, para uma comparação definitiva, os dois algoritmos deveriam ser treinados e avaliados utilizando exatamente a mesma divisão dos dados, o mesmo pré-processamento e os mesmos critérios de avaliação.

---

## 15. Melhorias futuras

- Comparar os dois modelos usando a mesma divisão de treino e teste;
- Utilizar validação cruzada;
- Realizar busca de hiperparâmetros com `GridSearchCV` ou `RandomizedSearchCV`;
- Testar outros algoritmos, como XGBoost, LightGBM ou Regressão Logística;
- Ajustar o limiar de decisão do modelo;
- Analisar a curva ROC e a curva Precision-Recall;
- Avaliar o custo financeiro de falsos positivos e falsos negativos;
- Remover definitivamente variáveis identificadoras;
- Padronizar todo o pré-processamento dentro de uma Pipeline.

---

## Tecnologias utilizadas

- Python;
- Pandas;
- NumPy;
- Matplotlib;
- Seaborn;
- Scikit-learn;
- Jupyter Notebook.
