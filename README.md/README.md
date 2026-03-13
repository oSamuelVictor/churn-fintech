# 🏦 Previsão de Churn em Clientes Bancários

Modelo de machine learning para identificar clientes com alta probabilidade de cancelar a conta — permitindo que o banco aja com ações de retenção antes que o cliente saia.

---

## 📌 Problema de negócio

Bancos perdem receita significativa quando clientes encerram suas contas. Identificar **quem está em risco antes que isso aconteça** permite agir com ofertas personalizadas, reduzindo o churn de forma proativa e econômica.

> **Pergunta central:** dado o perfil de um cliente, qual a probabilidade de ele cancelar a conta nos próximos meses?

---

## 📊 Resultados

| Modelo | AUC-ROC | F1-Score |
|---|---|---|
| Baseline (DummyClassifier) | 0.500 | 0.000 |
| Regressão Logística | ~0.77 | ~0.58 |
| Random Forest | ~0.86 | ~0.62 |
| **XGBoost** ✅ | **~0.87** | **~0.64** |

**Impacto financeiro estimado** (base de 10.000 clientes):
- O modelo identifica clientes em risco com precisão suficiente para gerar retorno positivo nas ações de retenção
- Falsos Negativos (clientes perdidos sem aviso) reduzidos significativamente em relação ao baseline
- Threshold ótimo ajustado para maximizar o impacto financeiro, não apenas a métrica técnica

---

## 🔍 Principais insights da análise

- **Idade** é o preditor mais forte — clientes acima de 45 anos têm risco de churn significativamente maior
- **Membros inativos** saem quase o dobro dos ativos (variável mais importante comportamentalmente)
- **Clientes alemães** têm taxa de churn ~2x maior que franceses e espanhóis
- **Clientes com 3-4 produtos** apresentam comportamento anômalo — taxa de churn surpreendentemente alta
- Dataset desbalanceado (20% churn) tratado com `class_weight='balanced'`

---

## 🗂️ Estrutura do projeto

```
churn-fintech/
│
├── data/
│   ├── raw/                        # Dataset original (não modificado)
│   └── processed/                  # Datasets gerados pelos notebooks
│
├── notebooks/
│   ├── 01_eda.ipynb                # Análise exploratória completa
│   ├── 02_feature_engineering.ipynb # Criação e seleção de features
│   └── 03_modeling.ipynb           # Treinamento, avaliação e impacto
│
├── models/
│   └── modelo_churn_final.pkl      # Modelo treinado serializado
│
├── reports/                        # Gráficos exportados pelos notebooks
│
└── README.md
```

---

## 🛠️ Tecnologias utilizadas

- **Python 3.10+**
- `pandas` e `numpy` — manipulação de dados
- `matplotlib` e `seaborn` — visualizações
- `scikit-learn` — pré-processamento, modelos e métricas
- `xgboost` — modelo final
- `scipy` — testes estatísticos (Mann-Whitney U, Point-Biserial)

---

## ▶️ Como executar

**1. Clone o repositório**
```bash
git clone https://github.com/seu-usuario/churn-fintech.git
cd churn-fintech
```

**2. Instale as dependências**
```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost scipy jupyter
```

**3. Adicione o dataset**

Baixe o arquivo `Churn_Modelling.csv` no [Kaggle](https://www.kaggle.com/datasets/mathchi/churn-for-bank-customers) e coloque em `data/raw/`.

**4. Execute os notebooks na ordem**
```
01_eda.ipynb → 02_feature_engineering.ipynb → 03_modeling.ipynb
```

---

## 📁 Dataset

- **Fonte:** [Bank Customer Churn — Kaggle](https://www.kaggle.com/datasets/mathchi/churn-for-bank-customers)
- **Registros:** 10.000 clientes
- **Variável alvo:** `Exited` (1 = fez churn, 0 = permaneceu)
- **Features originais:** CreditScore, Geography, Gender, Age, Tenure, Balance, NumOfProducts, HasCrCard, IsActiveMember, EstimatedSalary

---

## 📚 Etapas do projeto

Este projeto seguiu o pipeline completo de análise de dados:

1. **Entendimento do problema** — definição da pergunta de negócio e critério de sucesso
2. **Coleta de dados** — dataset público com 10.000 clientes de banco europeu
3. **Limpeza e preparação** — remoção de colunas irrelevantes, checagem de nulos e duplicatas
4. **Análise exploratória (EDA)** — distribuições, correlações, testes estatísticos e visualizações
5. **Feature engineering** — 20+ features criadas com hipóteses de negócio documentadas
6. **Modelagem** — 3 algoritmos comparados com cross-validation estratificado
7. **Avaliação** — métricas adequadas para dados desbalanceados + análise de impacto financeiro
8. **Comunicação** — notebooks organizados, gráficos exportados, README documentado

---

*Projeto desenvolvido como portfólio de análise de dados | Dataset público — Kaggle*
