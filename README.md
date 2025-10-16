# Pipeline de Dados na Azure com Databricks e Data Factory
<p align="center">
  <img width="580" height="320" alt="Pipeline no Azure Data Factory" src="https://github.com/user-attachments/assets/fb6a3189-3dcc-4e41-99e1-b9e2c2ae585f" />
</p>

Este projeto demonstra a criação e orquestração de um **pipeline de dados em nuvem** utilizando **Azure Databricks** e **Azure Data Factory (ADF)**.  
O objetivo é construir um fluxo automatizado de ingestão, transformação e armazenamento de dados em um **Data Lake**, aplicando boas práticas de Engenharia de Dados.

---

## Visão Geral

O pipeline desenvolvido realiza todas as etapas de um fluxo moderno de dados:
<p align="center">
<img width="1366" height="630" alt="Image" src="https://github.com/user-attachments/assets/57a0c430-d6e5-4c24-9933-f74ccadabc4c" />
</p>

- Leitura de um **dataset JSON de imóveis** armazenado na camada **Inbound** (`dados_brutos_imoveis.json`);
- Processamento e transformação dos dados no **Azure Databricks**, gerando as camadas **Bronze** e **Silver**;
- Orquestração e automação das execuções com **Azure Data Factory**, utilizando um **gatilho (trigger)** configurado para rodar **a cada 1 hora**.

Esse projeto tem como propósito **demonstrar o ciclo completo de um pipeline de dados em nuvem**, desde a ingestão até o tratamento final dos dados, com monitoramento e automação.

---

## Estrutura de Camadas do Data Lake

### Inbound → Bronze → Silver

| Camada | Descrição |
|:--------|:-----------|
| **Inbound** | Dados brutos em JSON (dados de imóveis). |
| **Bronze** | Dados padronizados e com limpeza básica. |
| **Silver** | Dados tratados e otimizados em formato Delta, prontos para consumo analítico. |

---

## ⚙️ Tecnologias Utilizadas

| Categoria | Ferramenta | Descrição |
|------------|-------------|-----------|
| **Cloud Provider** | Microsoft Azure | Hospedagem e gerenciamento dos serviços em nuvem |
| **Processamento** | Azure Databricks | Tratamento e transformação dos dados |
| **Orquestração** | Azure Data Factory | Agendamento e automação dos pipelines |
| **Armazenamento** | Azure Data Lake Storage | Estruturação das camadas Inbound, Bronze e Silver |
| **Linguagens** | Python / Scala | Desenvolvimento dos notebooks de ETL |
| **Versionamento** | GitHub | Controle de versão do código e integração com Databricks |

---

## 📂 Estrutura do Projeto

A estrutura do repositório no GitHub está organizada da seguinte forma:

📁 pipeline_databricks_azure/<br>
├── 📁 databricks-curso-pipeline/ <br>
├── 📁 factory/     # Definição da factory do Azure Data Factory<br>
├── 📁 linkedService/     # Conexões entre ADF, Databricks e Data Lake<br>
├── 📁 notebooks/     # Notebooks de transformação no Databricks<br>
│ ├── inbound_to_bronze.py<br>
│ ├── bronze_to_silver.py<br>
│ └── python_etl_inbound_to_silver.py<br>
│<br>
├── 📁 pipeline/     # Pipeline principal do Data Factory<br>
│ └── datalake_ingestion_pipeline.json<br>
│<br>
├── 📁 trigger/     # Gatilho configurado para execução a cada 1 hora<br>
│ └── pipeline_trigger.json<br>
│<br>
├── .gitignore<br>
├── publish_config.json<br>
└── README.md<br>

---

## 🔄 Fluxo de Execução

1. **Dados Iniciais (Inbound):**  
   O arquivo `dados_brutos_imoveis.json` é armazenado na camada *Inbound* do Data Lake.

2. **Transformação no Databricks:**  
   - O notebook `inbound_to_bronze` lê e padroniza os dados.  
   - O notebook `bronze_to_silver` aplica transformações adicionais e salva os resultados em **formato Delta** na camada Silver.

3. **Orquestração com Data Factory:**  
   - O pipeline no ADF utiliza duas atividades do tipo **Databricks**, executadas em sequência.  
   - Um **gatilho (trigger)** foi configurado para executar o pipeline automaticamente **a cada 1 hora**.

4. **Monitoramento:**  
   O status das execuções pode ser acompanhado no painel do **Azure Data Factory**, com logs detalhados e histórico de runs.

---

## 🧠 Conceitos Aplicados

- Estrutura de **Data Lake em múltiplas camadas** (Inbound, Bronze, Silver);  
- Ingestão e tratamento de **dados brutos JSON**;  
- Uso do **Delta Lake** para versionamento e otimização de consultas;  
- **Orquestração e automação** com o Azure Data Factory;  
- Boas práticas de **integração entre Databricks, Data Factory e Data Lake**;  
- **Versionamento com GitHub**, permitindo CI/CD e rastreabilidade.

---

## Pipeline no Data Factory

### Fluxo visual do pipeline criado no **Azure Data Factory**:

<p align="center">
<img width="503" height="290" alt="Image" src="https://github.com/user-attachments/assets/32f6889e-0a13-49bf-a749-819e5cd971d7" />
</p>

### Cada notebook é executado em sequência, processando os dados das camadas anteriores e gravando os resultados tratados no Data Lake.

*(Na imagem abaixo, ambas as atividades aparecem com status “✅ Bem-sucedido” após a execução do pipeline.)*
<p align="center">
<img width="800" height="467" alt="Image" src="https://github.com/user-attachments/assets/1edb6fea-42ff-4be2-8525-c319a5825360" />
</p>

---

## 🕒 Automação com Gatilho

O **gatilho (trigger)** executa automaticamente o pipeline a cada **1 hora**, garantindo a atualização contínua dos dados.  
Essa automação elimina a necessidade de execução manual, mantendo o fluxo sempre atualizado.

---

## 🧾 Resultados

- Dados brutos de imóveis transformados em formato Delta otimizado;  
- Pipeline automatizado e monitorado via ADF;  
- Estrutura modular e escalável, facilitando futuras extensões;  
- Base sólida para construção de camadas **Gold** e relatórios em BI.


---

## 👨‍💻 Autor

**Ramon Santos**  
Projeto pessoal desenvolvido para prática e portfólio voltado à **Engenharia de Dados**  
📧 Contato: [LinkedIn](https://www.linkedin.com/in/ramonsantoss/)
