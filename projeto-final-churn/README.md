# Projeto Final — Previsão de Churn de Clientes (Interconnect / Telecom)

Projeto final da minha formação em Ciência de Dados. A proposta foi resolver um problema real
de uma operadora de telecomunicações: **prever quais clientes estão prestes a cancelar o
serviço (churn)**, para que a equipe de marketing possa agir antes, com ofertas e retenção.

É o projeto que amarra boa parte do que aprendi ao longo do curso — de manipulação de dados
até machine learning de ponta a ponta.

## O problema de negócio

Reter um cliente custa bem menos do que conquistar um novo. Se a empresa consegue identificar
com antecedência quem tem risco de sair, ela direciona a verba de retenção para quem realmente
precisa, em vez de dar desconto para todo mundo. O objetivo do modelo é justamente esse:
sinalizar os clientes em risco.

## Os dados

Quatro fontes diferentes, ligadas pelo identificador do cliente:

- `contract.csv` — dados do contrato (tipo, cobranças, datas).
- `personal.csv` — dados pessoais (gênero, dependentes, etc.).
- `internet.csv` — serviços de internet contratados.
- `phone.csv` — serviço de telefonia.

São cerca de 7 mil clientes, com ~26,5% de cancelamento (classes desbalanceadas).

## O que foi feito

1. **Limpeza e junção** das quatro fontes num único dataset, tratando valores ausentes que na
   verdade significavam "serviço não contratado".
2. **Análise exploratória (EDA)** para entender o churn e levantar os principais fatores.
3. **Engenharia de atributos** — criação de variáveis como tempo de casa, número de serviços e
   valor por serviço.
4. **Preparação** — codificação, padronização e divisão treino/teste estratificada, tudo dentro
   de um pipeline para evitar vazamento de dados.
5. **Modelagem** — modelo de referência (dummy) e comparação de três algoritmos (Regressão
   Logística, Random Forest e LightGBM), com ajuste de hiperparâmetros via `RandomizedSearchCV`.
6. **Calibração do limiar** de decisão priorizando o recall (porque deixar passar um cliente que
   vai cancelar é o erro mais caro).
7. **Interpretação** dos fatores de churn e recomendações de negócio segmentadas por risco.

## Resultado

O melhor modelo (**Regressão Logística**) alcançou **ROC-AUC ≈ 0,84** no conjunto de teste,
acima da meta do projeto e sem sinais de overfitting. Os fatores que mais explicam o churn:
**contrato mês a mês, pouco tempo de casa, internet por fibra e pagamento por cheque
eletrônico**.

## Competências do curso aplicadas aqui

- **Python / pandas** — manipulação, limpeza e junção de múltiplas fontes.
- **Análise e estatística de dados** — EDA, distribuições, taxas por segmento.
- **Preparação de dados para ML** — encoding, escalonamento, tratamento de desbalanceamento.
- **Machine learning supervisionado** — baseline, comparação de modelos, validação cruzada,
  ajuste de hiperparâmetros, calibração de limiar e avaliação por ROC-AUC / recall / precisão.

## Como rodar

1. Coloque os quatro CSVs numa pasta (por padrão o notebook procura em `projeto/`; ajuste o
   `DATA_DIR` no topo se precisar).
2. Abra `Projeto_Final_Churn_Interconnect.ipynb` no Jupyter e execute as células em ordem.

**Bibliotecas:** pandas, numpy, matplotlib, seaborn, scikit-learn e lightgbm. O notebook foi
escrito para rodar tanto em versões recentes do scikit-learn quanto na 0.24.

## Estrutura

```
projeto-final-churn/
├── README.md
└── Projeto_Final_Churn_Interconnect.ipynb
```
