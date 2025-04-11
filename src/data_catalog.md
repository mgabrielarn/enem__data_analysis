# Catálogo de Dados — Microdados do ENEM 2023
---


## Linhagem dos Dados

- **Fonte:** Microdados ENEM 2023 — disponível para download em: [https://www.gov.br/inep/pt-br/acesso-a-informacao/dados-abertos/microdados/enem](https://www.gov.br/inep/pt-br/acesso-a-informacao/dados-abertos/microdados/enem)
- **Formato original:** Arquivo texto (.CSV) delimitado por `;` e acompanhado de dicionário de dados
- **Transformações aplicadas:**
  - Leitura do arquivo
  - Seleção de colunas relevantes
  - Criação de tabelas dimensão com `.dropDuplicates()`
  - Geração de **chaves substitutas (surrogate keys)** para tabelas dimensão com função `add_surrogate_key`
  - Criação da **fato_resultado_enem** com `join` das chaves substitutas
  - Escrita final no ambiente de arquivos

---

## FATO_RESULTADO_ENEM

| Coluna               | Tipo      | Descrição | Domínio Esperado |
|----------------------|-----------|-----------|------------------|
| NU_ANO               | Inteiro   | Ano da realização do exame | 2023 |
| TP_PRESENCA_* (CN, CH, LC, MT)        | Inteiro   | Presença nas provas (0 = ausente, 1 = presente, 2 = eliminado) | {0, 1, 2} |
| NU_NOTA_* (CN, CH, LC, MT)           | Double    | Nota por área do conhecimento | 0–1000 |
| TP_STATUS_REDACAO    | Inteiro   | Status da correção da redação (1 = Sem problemas, 2 = Anulada, 3 = Cópia Texo Motivador, 4 = Em Branco, 6 = Fuga ao tema, 7= Não atendeu ao tipo textual, 8 = Texto insuficiente, 9 = Parte desconectada) | Ex: {1, 2, 3, ... , 9} |
| NU_NOTA_REDACAO      | Double    | Nota final da redação | 0–1000 |
| ID_* (PARTICIPANTE, SOCIOECONOMICO, LOCAL_PROVA)                 | Inteiro   | Chaves estrangeiras para dimensões | Geradas via surrogate key |

---

## DIM_PARTICIPANTE

| Coluna              | Tipo      | Descrição | Domínio Esperado |
|---------------------|-----------|-----------|------------------|
| ID_PARTICIPANTE     | Inteiro   | Identificador único de participante | Chave estrangeira gerada via surrogate key |
| TP_FAIXA_ETARIA     | Inteiro   | Faixa etária | 1–20 (de acordo com faixas do INEP) |
| TP_SEXO             | String    | Sexo | {"M", "F"} |
| TP_ESTADO_CIVIL     | Inteiro   | Estado civil | {0: Não informado, 1: Solteiro, ...} |
| TP_COR_RACA         | Inteiro   | Cor ou raça | {0: Não declarado, 1: Branca, 2: Preta, 3: Parda, 4: Amarela, 5: Indígena, 6: Não dispõe da informação} |
| TP_NACIONALIDADE    | Inteiro   | Nacionalidade | {1: Brasileira, 2: Brasileira - Nascido exterior, 3: Estrangeira, ...} |
| TP_ST_CONCLUSAO     | Inteiro   | Situação de conclusão do ensino médio | {1: Já concluído, 2: Concluirá em 2023, ...} |
| TP_ANO_CONCLUIU     | Inteiro   | Ano de conclusão | Valores reais de anos de conclusão (2007 - 2022) |
| TP_ESCOLA           | Inteiro   | Tipo de escola | {1: Não respondeu; 2: Pública, 3: Privada.} |
| TP_ENSINO           | Inteiro   | Tipo de instituição que concluiu ou concluirá o Ensino Médio  | {1: Regular, 2: Educação Especial.} |
| IN_TREINEIRO        | Inteiro   | Indica se o inscrito fez a prova com intuito de apenas treinar seus conhecimentos | {0, 1} |

---

## DIM_SOCIOECONOMICO

| Coluna         | Tipo   | Descrição | Domínio Esperado |
|----------------|--------|-----------|------------------|
| ID_SOCIOECONOMICO    | Inteiro   | Identificador único de participante no questionário socioeconomico | Chave estrangeira gerada via surrogate key |
| Q001                | CHAR      | Até que série seu pai, ou o homem responsável por você, estudou? | {A: Nunca estudou., B: Não completou a 4ª série/5º ano do Ensino Fundamental., C: Completou a 4ª série/5º ano, mas não completou a 8ª série/9º ano., D: Completou a 8ª série/9º ano do Ensino Fundamental, mas não o Ensino Médio., E: Completou o Ensino Médio, mas não completou a Faculdade., F: Completou a Faculdade, mas não completou a Pós-graduação., G: Completou a Pós-graduação., H: Não sei.} |
| Q002                | CHAR      | Até que série sua mãe, ou a mulher responsável por você, estudou? | {A: Nunca estudou., B: Não completou a 4ª série/5º ano do Ensino Fundamental., C: Completou a 4ª série/5º ano, mas não completou a 8ª série/9º ano., D: Completou a 8ª série/9º ano do Ensino Fundamental, mas não o Ensino Médio., E: Completou o Ensino Médio, mas não completou a Faculdade., F: Completou a Faculdade, mas não completou a Pós-graduação., G: Completou a Pós-graduação., H: Não sei.} |
| Q003                | CHAR      | Em relação às pessoas que moram com você, o seu pai mora com você? | {A: Sim., B: Não., C: Não sei.} |
| Q004                | CHAR      | Em relação às pessoas que moram com você, a sua mãe mora com você? | {A: Sim., B: Não., C: Não sei.} |
| Q005                | CHAR      | Qual é a renda mensal aproximada de sua família (soma da renda de todos os integrantes)? | {A: Nenhuma renda., B: Até R$ 998,00., C: De R$ 998,01 até R$ 1.497,00., D: De R$ 1.497,01 até R$ 1.996,00., E: De R$ 1.996,01 até R$ 2.495,00., F: De R$ 2.495,01 até R$ 2.994,00., G: De R$ 2.994,01 até R$ 3.992,00., H: De R$ 3.992,01 até R$ 4.990,00., I: De R$ 4.990,01 até R$ 5.988,00., J: De R$ 5.988,01 até R$ 6.986,00., K: De R$ 6.986,01 até R$ 7.984,00., L: De R$ 7.984,01 até R$ 8.982,00., M: De R$ 8.982,01 até R$ 9.980,00., N: Acima de R$ 9.980,00.} |
| Q006                | CHAR      | Quantas pessoas moram em sua residência, incluindo você? | {A: 1, B: 2, C: 3, D: 4, E: 5, F: 6, G: 7, H: 8 ou mais} |
| Q007                | CHAR      | Em sua residência tem banheiro? | {A: Não, B: Sim, 1, C: Sim, 2, D: Sim, 3, E: Sim, 4, F: Sim, 5 ou mais} |
| Q008                | CHAR      | Em sua residência tem quarto para dormir? | {A: Não, B: Sim, 1, C: Sim, 2, D: Sim, 3, E: Sim, 4, F: Sim, 5 ou mais} |
| Q009                | CHAR      | Quantas televisões em cores existem em sua residência? | {A: Nenhuma, B: 1, C: 2, D: 3, E: 4, F: 5 ou mais} |
| Q010                | CHAR      | Quantos carros existem em sua residência? | {A: Nenhum, B: 1, C: 2, D: 3 ou mais} |
| Q011                | CHAR      | Quantas motocicletas existem em sua residência? | {A: Nenhuma, B: 1, C: 2, D: 3 ou mais} |
| Q012                | CHAR      | Quantos rádios existem em sua residência? | {A: Nenhum, B: 1, C: 2, D: 3 ou mais} |
| Q013                | CHAR      | Quantos fornos micro-ondas existem em sua residência? | {A: Nenhum, B: 1, C: 2, D: 3 ou mais} |
| Q014                | CHAR      | Quantas máquinas de lavar roupa existem em sua residência? | {A: Nenhuma, B: 1, C: 2, D: 3 ou mais} |
| Q015                | CHAR      | Quantos máquinas de secar roupa existem em sua residência? | {A: Nenhuma, B: 1, C: 2, D: 3 ou mais} |
| Q016                | CHAR      | Quantos computadores existem em sua residência? | {A: Nenhum, B: 1, C: 2, D: 3 ou mais} |
| Q017                | CHAR      | Quantos lava-louças existem em sua residência? | {A: Nenhum, B: 1, C: 2, D: 3 ou mais} |
| Q018                | CHAR      | Quantos aspiradores de pó existem em sua residência? | {A: Nenhum, B: 1, C: 2, D: 3 ou mais} |
| Q019                | CHAR      | Qual a principal forma de acesso à internet na sua residência? | {A: Não tem acesso, B: Banda larga fixa, C: Banda larga móvel (chip de celular), D: Roteador de vizinho, E: Outro} |
| Q020                | CHAR      | Quantas pessoas com 16 anos ou mais moram em sua residência? | {A: Nenhuma, B: 1, C: 2, D: 3, E: 4, F: 5 ou mais} |
| Q021                | CHAR      | Dentre as pessoas que moram em sua casa, quantas trabalham? | {A: Nenhuma, B: 1, C: 2, D: 3 ou mais} |
| Q022                | CHAR      | Qual é a escolaridade da pessoa responsável financeiramente por sua família? | {A: Nunca estudou, B: Até 4ª série/5º ano, C: Até 8ª série/9º ano, D: Ensino Médio completo, E: Faculdade completa, F: Pós-graduação} |
| Q023                | CHAR      | Essa pessoa responsável trabalha? | {A: Não trabalha, B: Trabalha, sem registro, C: Trabalha com registro, D: Trabalha por conta própria, E: Aposentado/pensionista} |
| Q024                | CHAR      | Você já terminou ou está cursando o Ensino Médio? | {A: Já terminei, B: Estou cursando, C: Nunca cursei} |
| Q025                | CHAR      | Em que tipo de escola você frequentou o Ensino Médio? | {A: Pública somente, B: Pública com parte em particular, C: Particular com bolsa, D: Particular sem bolsa} |




---

## DIM_LOCAL_PROVA

| Coluna              | Tipo    | Descrição | Domínio Esperado |
|---------------------|---------|-----------|------------------|
| ID_LOCAL_PROVA    | Inteiro   | Identificador único de município onde se aplicou a prova | Chave estrangeira gerada via surrogate key |
| CO_MUNICIPIO_PROVA  | Inteiro | Código IBGE do município | Código válido de município |
| NO_MUNICIPIO_PROVA  | String  | Nome do município da prova | Texto |
| CO_UF_PROVA         | Inteiro | Código da UF da prova | 11 a 53 (IBGE) |
| SG_UF_PROVA         | String  | Sigla da UF da prova | {"SP", "RJ", "BA", ...} |

---
