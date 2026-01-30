# Project 2Folds

Este repositório apresenta a implementação, backtest e análise da estratégia **2Folds**, um modelo quantitativo de investimento desenvolvido em Python.

A estratégia combina **aprendizado de máquina por ensemble (XGBoost)** com **análise de sentimento financeiro (FinBERT)** e variáveis macroeconômicas, explorando ineficiências de mercado geradas pela interação entre estrutura técnica, fluxo informacional e comportamento dos agentes.

---

## Sumário
1. [Visão Geral](#visão-geral)
2. [Hipótese de Investimento](#hipótese-de-investimento)
3. [Metodologia e Modelagem](#metodologia-e-modelagem)
    - [Modelo A: Estrutura Técnica](#modelo-a-estrutura-técnica)
    - [Modelo B: Sentimento e Macroeconomia](#modelo-b-sentimento-e-macroeconomia)
    - [Fusão dos Modelos (2 Folds)](#fusão-dos-modelos-2-folds)
4. [Regras de Operação e Backtest](#regras-de-operação-e-backtest)
5. [Resultados](#resultados)
6. [Engenharia de Dados](#engenharia-de-dados)

---

## Visão Geral

| Parâmetro | Detalhe |
|---|---|
| **Estratégia** | Portfólio Quantitativo |
| **Classe de Ativos** | Ações |
| **Universo** | Ibovespa |
| **Frequência** | Semanal |
| **Rebalanceamento** | Sexta-feira |
| **Benchmark** | IBOV / CDI |
| **Tecnologia** | Python (Pandas, XGBoost, HuggingFace, Scikit-learn) |

---

## Hipótese de Investimento

A hipótese central do projeto é que **modelos puramente técnicos ou puramente informacionais capturam apenas parte da dinâmica do mercado**.

> A integração entre **modelos de Ensemble Learning baseados em dados técnicos** e **modelos de Análise de Sentimento e variáveis macroeconômicas**, quando combinados por um mecanismo adaptativo de ponderação, é capaz de gerar **alpha consistente acima do benchmark e do ativo livre de risco (CDI)**.

O nome **2Folds** representa a dualidade estrutural do modelo:
- Um *fold* focado em padrões estatísticos e recorrência técnica;
- Um *fold* focado na entropia informacional do mercado (sentimento e macro).

---

## Metodologia e Modelagem

A arquitetura do sistema é composta por **dois modelos independentes por ativo**, treinados separadamente e posteriormente combinados.

### Modelo A: Estrutura Técnica

O **Modelo A** utiliza o algoritmo **XGBoost**, um método de ensemble baseado em árvores de decisão e otimização por gradiente de segunda ordem.

- **Features Técnicas:**
  - Retornos e volatilidade em múltiplas janelas
  - Indicadores técnicos (RSI, MACD, Bollinger Bands, ATR)
  - Estrutura de candles (corpo, sombras, ranges)
- **Target:** retorno semanal do ativo
- **Objetivo:** capturar padrões estatísticos persistentes e estruturas de momentum/reversão

---

### Modelo B: Sentimento e Macroeconomia

O **Modelo B** explora informações não estruturadas e variáveis exógenas ao preço.

- **Análise de Sentimento:**
  - Uso do **FinBERT**, modelo Transformer treinado em linguagem financeira
  - Classificação de notícias em polaridades (positiva, neutra, negativa)
- **Variáveis Macroeconômicas:**
  - Taxa de juros (CDI)
  - Indicadores de mercado e risco sistêmico
- **Objetivo:** capturar mudanças de regime e choques informacionais não refletidos imediatamente nos preços

---

### Fusão dos Modelos (2 Folds)

As previsões dos dois modelos são combinadas por um mecanismo de ponderação dinâmica, formando o sinal final de decisão.

- Cada *fold* gera um score normalizado por ativo
- O sinal agregado define:
  - Seleção dos ativos
  - Direção e intensidade da exposição
- A lógica de ensemble reduz ruído e aumenta robustez fora da amostra

---

## Regras de Operação e Backtest

Para garantir robustez estatística e replicabilidade:

- **Frequência:** rebalanceamento semanal (sextas-feiras)
- **Prevenção de Lookahead Bias:** uso exclusivo de dados disponíveis até o momento da decisão
- **Custos de Transação:** considerados no resultado líquido
- **Base de Comparação:** Ibovespa e CDI
- **Janela de Análise:** conforme período disponível no dataset consolidado

---

## Resultados

O backtest indicou que a estratégia:

- Superou o **Ibovespa** em retorno total e métricas ajustadas ao risco
- Apresentou **Sharpe Ratio superior** ao benchmark
- Gerou retorno acima do **CDI**, evidenciando criação de valor além do prêmio de risco da economia

Os resultados sugerem que a combinação entre estrutura técnica e informação qualitativa contribui para a geração de alpha consistente.

---

## Engenharia de Dados

A engenharia de dados foi um componente central do projeto.

- **Fontes:**
  - Yahoo Finance (preços)
  - Bases públicas e agregadores de notícias financeiras
  - Banco Central do Brasil (CDI)
- **Processos:**
  - Limpeza e alinhamento temporal
  - Feature engineering técnico e textual
  - Normalização e controle de *data leakage*

---

*Disclaimer: Este projeto possui finalidade exclusivamente educacional e acadêmica. Os resultados apresentados são provenientes de simulações (backtests) e não constituem recomendação de investimento.*
