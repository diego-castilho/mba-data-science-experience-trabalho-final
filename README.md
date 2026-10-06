# Data Science Experience · Trabalho Final

Previsão de atraso na entrega no e-commerce brasileiro, com a base pública da Olist.

Trabalho final da disciplina Data Science Experience do MBA.

**Integrantes:** Diego Castilho, Leandro Oliveira, Luiz Fernando, Matheus Ferreira, Rodrigo Palma e Sara Barros.

[![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/diego-castilho/mba-data-science-experience-trabalho-final/blob/main/Data_Science_Experience.ipynb)

## Sobre o trabalho

Na Olist, pedidos entregues depois da data prometida recebem nota 1 ou 2 em 54% dos casos, contra 9% dos
pedidos entregues no prazo. O objetivo do trabalho é prever o atraso no momento em que o vendedor posta o
pedido, quando ainda é possível agir.

O problema foi modelado de duas formas, a partir da mesma variável:

- **Classificação:** o pedido vai atrasar? (`target_atraso`)
- **Regressão:** com quantos dias de atraso ou de folga o pedido vai chegar? (`atraso_dias`)

O notebook segue os 10 itens da atividade: escolha da base, definição do problema, limpeza, análise
exploratória, preparação, modelagem, otimização com AutoML, avaliação, interpretabilidade e conclusões.

## Principais resultados

| | Classificação (F1) | Regressão (MAE) |
|---|---|---|
| Baseline | 0,000 | 6,74 dias |
| Melhor modelo inicial | 0,418 (Random Forest) | 3,99 dias (Gradient Boosting) |
| Melhor modelo final | 0,443 (Gradient Boosting + Optuna) | 3,93 dias (Gradient Boosting + Optuna) |

- Foram comparados seis modelos em cada problema: Regressão Logística ou Linear, KNN, Árvore de Decisão,
  Random Forest, Gradient Boosting e Rede Neural.
- A otimização de hiperparâmetros foi feita com Optuna.
- A interpretação dos modelos usou Feature Importance por permutação e SHAP.
- A variável mais importante foi a folga do prazo no despacho, criada pelo grupo a partir do prazo
  prometido e do tempo que o vendedor levou para postar.

## Estrutura do repositório

| Arquivo | Conteúdo |
|---|---|
| `Data_Science_Experience.ipynb` | Notebook completo do trabalho, já executado, com todas as saídas |
| `pyproject.toml` e `uv.lock` | Dependências do ambiente Python |
| `.python-version` | Versão do Python usada (3.13) |

## Como executar

**Google Colab:** clique no botão "Abrir no Colab" acima e use `Ambiente de execução → Executar tudo`. A
primeira célula instala as bibliotecas que faltarem. A execução leva cerca de 1h10.

**Localmente (VSCode):** o ambiente foi criado com o [uv](https://docs.astral.sh/uv/).

```bash
git clone https://github.com/diego-castilho/mba-data-science-experience-trabalho-final.git
cd mba-data-science-experience-trabalho-final
uv sync
```

Depois, abra o notebook no VSCode, selecione o ambiente `.venv` como kernel e execute todas as células.
A execução leva cerca de 20 minutos.

## Base de dados

A base é o [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce),
com cerca de 100 mil pedidos feitos entre 2016 e 2018, distribuídos em 9 tabelas, e publicada sob a
licença CC BY-NC-SA 4.0.

Os arquivos não estão no repositório, pois o notebook baixa a base direto do Kaggle com o `kagglehub`. Se
os CSVs estiverem em `data/raw/`, essa cópia local é usada.
