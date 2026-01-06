# Analise_Pandemia

# 📊 Análise de Dados do ENEM (2018-2023) - Pipeline ETL

![Python](https://img.shields.io/badge/Python-3.8%2B-blue)
![Pandas](https://img.shields.io/badge/Pandas-ETL-150458)
![Status](https://img.shields.io/badge/Status-Em_Desenvolvimento-yellow)

## 📝 Descrição do Projeto

Este projeto tem como objetivo analisar o impacto da pandemia de COVID-19 na educação brasileira através dos microdados do ENEM (Exame Nacional do Ensino Médio). 

O principal desafio técnico deste projeto foi lidar com o **volume de dados**. A série histórica completa (2018 a 2023) soma mais de **11GB de arquivos CSV brutos**, o que torna inviável a análise direta em ferramentas de visualização ou planilhas convencionais em um ambiente local.

Para solucionar isso, foi desenvolvido um código em Python para realizar a ingestão, limpeza, padronização e otimização dos dados.

## 🚀 Pipeline de Dados (ETL)

O script `etl_enem.py` realiza as seguintes etapas:

1.  **Ingestão:** Leitura dos arquivos CSV brutos (separados por `;` e encoding `latin1`).
2.  **Amostragem Estratificada:** Aplicação de uma técnica de amostragem (`sample`) coletando 5% dos dados de cada ano.
    * *Nota:* Foi utilizada uma `seed` fixa (`random_state=42`) para garantir a reprodutibilidade estatística dos dados.
3.  **Seleção de Features:** Filtragem apenas das colunas relevantes para a análise (Dados demográficos, notas, tipo de escola, etc.), reduzindo o consumo de memória.
4.  **Tratamento de Dados (Data Quality):**
    * Conversão de tipos de dados (`category`, `int64`, `float32`) para otimização.
    * **Correção de Regra de Negócio (2018):** Identificação e correção de inconsistência na coluna `TP_ESCOLA` no ano de 2018, onde os códigos diferiam do padrão dos anos seguintes (Mapeamento: `3 -> 4` e `4 -> 3`).
5.  **Armazenamento Otimizado:** Consolidação dos dados e exportação para formato **Parquet**, resultando em uma leitura muito mais performática para o Power BI.

## 📉 Resultados de Performance

| Etapa | Formato | Tamanho Total Aprox. |
| :--- | :---: | :---: |
| **Dados Brutos** | `.csv` | ~11.06 GB |
| **Dados Tratados** | `.parquet` | ~23 MB |

> **Ganho:** Redução drástica de armazenamento e tempo de leitura, mantendo a relevância estatística para análise de tendências.

## 🛠️ Tecnologias Utilizadas

* **Python:** Linguagem principal.
* **Pandas:** Manipulação e tratamento de dados.
* **PyArrow:** Backend para gravação de arquivos Parquet.
* **GC (Garbage Collector):** Gerenciamento manual de memória para evitar estouro de RAM durante o processamento.

## ⚙️ Como executar o projeto

### Pré-requisitos
Certifique-se de ter o Python instalado. Recomenda-se o uso de um ambiente virtual.

```bash
pip install pandas pyarrow
