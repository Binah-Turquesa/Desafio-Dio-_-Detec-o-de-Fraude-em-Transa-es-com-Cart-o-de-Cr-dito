# Desafio-Dio
Importância das variáveis : Quais variáveis influenciam a decisão do modelo.
# 🛡️ Detecção de Fraudes em Cartão de Crédito com XGBoost

Este projeto foi desenvolvido como um desafio prático do Bootcamp para explorar as áreas de Ciência de Dados e Cibersegurança Bancária.

## 🧠 O Objetivo
O foco do projeto foi criar um modelo de Inteligência Artificial capaz de analisar transações reais de cartões de crédito e identificar quais delas eram transações legítimas e quais eram tentativas de fraude.

## 🛠️ Tecnologias Utilizadas
* **Python** (Linguagem principal)
* **Google Colab** (Ambiente de desenvolvimento)
* **Pandas** (Para organização das tabelas de dados)
* **XGBoost** (O algoritmo de Machine Learning usado para detecção rápida)
* **Seaborn & Matplotlib** (Para a geração dos gráficos de Storytelling)

## 🕵️‍♀️ Minha Análise e Descobertas (O Desafio da V14)
Durante a aula, analisei o gráfico gerado pelo modelo para entender o peso das variáveis no eixo Y. 

De todas as colunas examinadas no arquivo (do V1 ao V28 e o Amount), deu para ver claramente que a barra da **V14** é a mais alta. Isso me mostra que a **V14** é a variável que mais ajuda o robô a tomar a decisão. Se o banco precisar caçar uma fraude rápido, a V14 é o principal sinal de alerta que o nosso código usa!

<img width="847" height="490" alt="GRAFICO_DESAFIO_MÉTRICA_PYTHON" src="https://github.com/user-attachments/assets/a6cd8798-e857-4783-b908-a6bcefd74438" />
#Código-Resposta ao desafio.

import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt


pesos = xgb.feature_importances_


colunas = x_train.columns


df_importancia = pd.DataFrame({'Variavel': colunas, 'Peso': pesos})
df_importancia = df_importancia.sort_values(by='Peso', ascending=False).head(10) # Pegamos as 10 mais importantes


cores_importancia = ["#e63946"] + ["#cfcfcf"] * 9

plt.figure(figsize=(10, 5))

sns.barplot(x='Variavel', y='Peso', data=df_importancia, palette=cores_importancia, hue='Variavel', legend=False)


variavel_principal = df_importancia.iloc[0]['Variavel']
plt.title(f'A Variável {variavel_principal} é o Fator de Maior Peso na Detecção de Fraudes do Banco', 
          fontsize=13, fontweight='bold', pad=20)

plt.xlabel('Variáveis do Dataset (Eixo X)')
plt.ylabel('Peso / Influência no Modelo (Eixo Y)', fontsize=11)
sns.despine()

plt.show()

