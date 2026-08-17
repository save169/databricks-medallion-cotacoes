# 📈 Real-Time Exchange Rate Pipeline | Databricks Medallion Architecture

[![Databricks](https://img.shields.io/badge/Databricks-PySpark-red?style=flat-square&logo=databricks)](https://databricks.com/)
[![Delta Lake](https://img.shields.io/badge/Storage-Delta%20Lake-blue?style=flat-square)](https://delta.io/)
[![Language](https://img.shields.io/badge/Language-Python%20%7C%20PySpark-yellow?style=flat-square&logo=python)](https://www.python.org/)

---

## Descrição

Um pipeline de engenharia de dados de ponta a ponta, construído no Databricks, implementando a **Medallion Architecture** (Bronze, Silver, Gold). O pipeline ingere payloads JSON de taxas de câmbio multi-moeda, aplica esquemas automatizados e validações de qualidade de dados, e calcula métricas financeiras agregadas diárias prontas para BI.

---

## 🏗️ Arquitetura & Data Pipeline

mermaid
graph TD
    A[External API / JSON Source] --> B[BRONZE LAYER<br>(bronze_cotacoes_raw)<br>Ingestão com preservação de esquema bruto<br>Colunas de auditoria de timestamp]
    B --> C[SILVER LAYER<br>(silver_cotacoes_limpo)<br>Limpeza, tipagem estrita (Double/Timestamp)<br>Deduplicação e validação de esquema]
    C --> D[GOLD LAYER<br>(gold_cotacoes_diarias)<br>Agregações de negócio (Min/Max/Média Diária)<br>Tabelas Delta otimizadas para Power BI/SQL]


---

### 💡 Principais Features & Destaques

- **Medallion Lakehouse Pattern:** Separação completa entre armazenamento bruto, transformações limpas e modelos de agregação.
- **Transações ACID:** Baseado em Delta Lake, com enforcement de esquema, evolução de esquema e time-travel.
- **Limpeza & Validação:** Tipagem estrita para números financeiros, eliminação de duplicatas e remoção de valores nulos.
- **Governança:** Pronto para Unity Catalog (catalog.schema.table).

---

## 📁 Estrutura do Repositório

plaintext
databricks-medallion-cotacoes/
├── README.md                           # Documentação técnica
├── notebooks/
│   ├── 01_bronze_ingestao.py           # Ingestão JSON bruta & rastreamento de metadata
│   ├── 02_silver_transformacao.py      # Limpeza, cast de tipos & deduplicação
│   └── 03_gold_agregacao.py            # Agregação de métricas diárias para analytics
└── docs/                               # Documentação adicional


---

## 🚀 Como Executar no Databricks

**Pré-requisitos:**
- Workspace Databricks (Community ou Cloud)
- Ambiente PySpark & Delta Lake
- Fonte de dados JSON configurada no Unity Catalog Volume/DBFS

**Passos:**
1. Clone o repositório: Workspace → Repos → Add Repo (URL do GitHub)
2. Execute os notebooks sequencialmente:
   - `01_bronze_ingestao`: Popula camada Bronze
   - `02_silver_transformacao`: Limpa dados
   - `03_gold_agregacao`: Calcula tabelas analíticas

---

## 📊 Output Analítico (Gold Layer)

| Coluna                | Tipo      | Descrição                                      |
|-----------------------|-----------|------------------------------------------------|
| data_referencia       | Date      | Data de referência da negociação               |
| moeda_origem          | String    | Código da moeda base (ex: USD, EUR)            |
| nome_par              | String    | Nome completo do par de moedas                 |
| media_valor_compra    | Double    | Média diária arredondada de compra             |
| media_valor_venda     | Double    | Média diária arredondada de venda              |
| max_valor_venda       | Double    | Maior taxa de venda registrada no intervalo    |
| min_valor_venda       | Double    | Menor taxa de venda registrada no intervalo    |

---

## 🛠️ Tech Stack & Ferramentas

- **Compute & Processing:** Apache Spark (PySpark), Databricks Repos
- **Storage Layer:** Delta Lake
- **Governança & Metastore:** Unity Catalog
- **Linguagem:** Python 3.x, SQL

---

## 👤 Autor & Contato

- **Salvador Peres — Data Engineer**
- [LinkedIn](https://www.linkedin.com/in/salvador-inacio-peres/)
- GitHub: [https://github.com/save169](#)
- Email: [save_169@yahoo.com.br]