# ETL e Análise dos Microdados do ENEM 2023

Este projeto foi desenvolvido como projeto final da sprint de Engenharia de Dados do curso de pós graduação em Ciência de Dados e Analytics pela PUC RIo de Janeiro. Em relação à estrutura de dados, simula-se a construção de um Data Warehouse baseado nos Microdados do ENEM 2023 (versão mais recente disponível), utilizando o modelo dimensional Estrela e PySpark. Com a carga de dados realizada, deu-se início à análise de ........ COMPLETAR

---

## Estrutura do Projeto

📁 /content/ ├── 📁 tabelas_enem/ # Tabelas salvas no formato Parquet │ ├── dim_participante.parquet │ ├── dim_socioeconomico.parquet │ ├── dim_local_prova.parquet │ ├── dim_local_escola.parquet │ └── fato_resultado_enem.parquet ├── catalogo_de_dados.md # Dicionário de dados completo └── README.md # Este arquivo

AJUSTAR CONFORME GIT

---

## Tecnologias Utilizadas

- Apache **Spark 3.x**
- **PySpark** (DataFrames API)
- Google **Colab**
- Python 3.x

---

## Fonte dos Dados

- **Microdados ENEM 2023**  
  Instituto Nacional de Estudos e Pesquisas Educacionais Anísio Teixeira (INEP)
  [https://www.gov.br/inep/pt-br/acesso-a-informacao/dados-abertos/microdados/enem](https://www.gov.br/inep/pt-br/acesso-a-informacao/dados-abertos/microdados/enem)

---

## Etapas do Projeto

1. Leitura dos microdados com PySpark
2. Seleção de colunas relevantes e tratamento de dados
3. Criação das dimensões com chaves substitutas (`add_surrogate_key`)
4. Criação da tabela fato com joins nas dimensões
5. Exportação das tabelas em formato `.parquet`
6. Criação do catálogo de dados com domínios, categorias e linhagem
7. Análise xxxxxxx COMPLETAR

---

## Esquema Estrela

**Fato:**
- `fato_resultado_enem`: notas, presenças, status da redação

**Dimensões:**
- `dim_participante`: dados pessoais e escolares
- `dim_socioeconomico`: respostas ao questionário socioeconômico
- `dim_local_prova`: informações sobre o local da prova
- `dim_local_escola`: localização e características da escola

---

## Documentação

- `catalogo_de_dados.md`: Catálogo de dados com descrições, domínios e linhagem

---

## Licença

Este projeto é de uso educacional.  
Os dados utilizados são públicos e disponibilizados pelo INEP.
