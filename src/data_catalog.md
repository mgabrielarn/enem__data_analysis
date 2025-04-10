# 📚 Catálogo de Dados — Esquema Estrela ENEM

---

## 📌 Observações Gerais

Independentemente do modelo, deve ser construído um **Catálogo de Dados** contendo minimamente uma **descrição detalhada dos dados e seus domínios**, incluindo:

- 🧮 **Valores mínimos e máximos esperados para dados numéricos**
- 🧾 **Possíveis categorias para dados categóricos**
- 🔍 **Linhagem dos dados**, incluindo:
  - Fonte de origem (como foram obtidos)
  - Técnicas utilizadas para compor o conjunto de dados (ex: seleção de colunas, joins, limpeza, tratamento de duplicidades, geração de chaves substitutas etc.)

---

## 🔗 Linhagem dos Dados

- **Fonte:** Microdados ENEM 2023 — disponível para download em: [https://www.gov.br/inep/pt-br/acesso-a-informacao/dados-abertos/microdados](https://www.gov.br/inep/pt-br/acesso-a-informacao/dados-abertos/microdados)
- **Formato original:** Arquivo texto (.CSV) delimitado por `;` e acompanhado de dicionário de dados (.XLSX)
- **Transformações aplicadas:**
  - Leitura com PySpark
  - Seleção de colunas relevantes
  - Criação de tabelas dimensão com `.dropDuplicates()`
  - Geração de **chaves substitutas (surrogate keys)** para tabelas dimensão com função `add_surrogate_key`
  - Criação da **fato_resultado_enem** com `join` das chaves substitutas
  - Escrita final no formato `.parquet` no ambiente do Google Colab

---

## 🎯 FATO_RESULTADO_ENEM

| Coluna               | Tipo      | Descrição | Domínio Esperado |
|----------------------|-----------|-----------|------------------|
| NU_INSCRICAO         | String    | Número de inscrição do participante | Numérico, identificador único |
| NU_ANO               | Inteiro   | Ano da realização do exame | 2023 |
| TP_PRESENCA_*        | Inteiro   | Presença nas provas (0 = ausente, 1 = presente, 2 = eliminado) | {0, 1, 2} |
| NU_NOTA_*            | Double    | Nota por área do conhecimento | 0–1000 |
| TP_STATUS_REDACAO    | Inteiro   | Status da correção da redação | Ex: {1, 2, 3, ...} |
| NU_NOTA_COMP*        | Double    | Notas de 0 a 200 por competência | 0–200 |
| NU_NOTA_REDACAO      | Double    | Nota final da redação | 0–1000 |
| ID_*                 | Inteiro   | Chaves estrangeiras para dimensões | Geradas via surrogate key |

---

## 🧑 DIM_PARTICIPANTE

| Coluna              | Tipo      | Descrição | Domínio Esperado |
|---------------------|-----------|-----------|------------------|
| TP_FAIXA_ETARIA     | Inteiro   | Faixa etária | 1–17 (de acordo com faixas do INEP) |
| TP_SEXO             | String    | Sexo | {"M", "F"} |
| TP_ESTADO_CIVIL     | Inteiro   | Estado civil | {0: Não informado, 1: Solteiro, ...} |
| TP_COR_RACA         | Inteiro   | Cor ou raça | {0: Não declarado, 1: Branca, ..., 5: Indígena} |
| TP_NACIONALIDADE    | Inteiro   | Nacionalidade | {1: Brasileira, 2: Brasileira - Nascido exterior, 3: Estrangeira} |
| TP_ST_CONCLUSAO     | Inteiro   | Situação de conclusão do ensino médio | {1: Já concluído, 2: Concluirá, ...} |
| TP_ANO_CONCLUIU     | Inteiro   | Ano de conclusão | Valores reais de anos |
| TP_ESCOLA           | Inteiro   | Tipo de escola | {1: Pública, 2: Privada, etc.} |
| TP_ENSINO           | Inteiro   | Modalidade de ensino | {1: Regular, 2: EJA, etc.} |
| IN_TREINEIRO        | Inteiro   | Participante treineiro? | {0, 1} |

---

## 🏠 DIM_SOCIOECONOMICO

| Coluna         | Tipo   | Descrição | Domínio Esperado |
|----------------|--------|-----------|------------------|
| Q001–Q027      | String | Respostas ao questionário socioeconômico | {"A", "B", "C", "D", "E", "F"} conforme pergunta |

> Exemplo:  
> - Q001: Escolaridade do pai — A: Nunca estudou, B: Até 4ª série, ..., E: Superior completo  
> - Q006: Renda familiar — A: Nenhuma, B: Até R$998, ..., F: Acima de R$9.600

---

## 📍 DIM_LOCAL_PROVA

| Coluna              | Tipo    | Descrição | Domínio Esperado |
|---------------------|---------|-----------|------------------|
| CO_MUNICIPIO_PROVA  | Inteiro | Código IBGE do município | Código válido de município |
| NO_MUNICIPIO_PROVA  | String  | Nome do município da prova | Texto |
| CO_UF_PROVA         | Inteiro | Código da UF da prova | 11 a 53 (IBGE) |
| SG_UF_PROVA         | String  | Sigla da UF da prova | {"SP", "RJ", "BA", ...} |

---

## 🏫 DIM_LOCAL_ESCOLA

| Coluna                    | Tipo    | Descrição | Domínio Esperado |
|---------------------------|---------|-----------|------------------|
| CO_MUNICIPIO_ESC          | Inteiro | Código do município da escola | Código IBGE |
| NO_MUNICIPIO_ESC          | String  | Nome do município | Texto |
| CO_UF_ESC                 | Inteiro | Código da UF da escola | 11 a 53 |
| SG_UF_ESC                 | String  | Sigla da UF | {"SP", "BA", "PA", ...} |
| TP_DEPENDENCIA_ADM_ESC    | Inteiro | Tipo de administração | {1: Federal, 2: Estadual, 3: Municipal, 4: Privada} |
| TP_LOCALIZACAO_ESC        | Inteiro | Localização | {1: Urbana, 2: Rural} |
| TP_SIT_FUNC_ESC           | Inteiro | Situação da escola | {1: Em atividade, 2: Extinta, etc.} |
