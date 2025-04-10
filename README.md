# enem__data_analysis

# 📚 Catálogo de Dados — Esquema Estrela ENEM

---

## 🎯 FATO_RESULTADO_ENEM (Fato Principal)

| Coluna               | Tipo      | Descrição |
|----------------------|-----------|-----------|
| NU_INSCRICAO         | String    | Número de inscrição do participante |
| NU_ANO               | Inteiro   | Ano da realização do exame |
| TP_PRESENCA_CN       | Inteiro   | Presença na prova de Ciências da Natureza |
| TP_PRESENCA_CH       | Inteiro   | Presença na prova de Ciências Humanas |
| TP_PRESENCA_LC       | Inteiro   | Presença na prova de Linguagens e Códigos |
| TP_PRESENCA_MT       | Inteiro   | Presença na prova de Matemática |
| NU_NOTA_CN           | Double    | Nota em Ciências da Natureza |
| NU_NOTA_CH           | Double    | Nota em Ciências Humanas |
| NU_NOTA_LC           | Double    | Nota em Linguagens e Códigos |
| NU_NOTA_MT           | Double    | Nota em Matemática |
| TP_STATUS_REDACAO    | Inteiro   | Status da correção da redação |
| NU_NOTA_COMP1        | Double    | Nota da competência 1 da redação |
| NU_NOTA_COMP2        | Double    | Nota da competência 2 da redação |
| NU_NOTA_COMP3        | Double    | Nota da competência 3 da redação |
| NU_NOTA_COMP4        | Double    | Nota da competência 4 da redação |
| NU_NOTA_COMP5        | Double    | Nota da competência 5 da redação |
| NU_NOTA_REDACAO      | Double    | Nota final da redação |
| ID_PARTICIPANTE      | Inteiro   | Chave estrangeira para dim_participante |
| ID_SOCIOECONOMICO    | Inteiro   | Chave estrangeira para dim_socioeconomico |
| ID_LOCAL_PROVA       | Inteiro   | Chave estrangeira para dim_local_prova |
| ID_LOCAL_ESCOLA      | Inteiro   | Chave estrangeira para dim_local_escola |

---

## 🧑 DIM_PARTICIPANTE

| Coluna              | Tipo      | Descrição |
|---------------------|-----------|-----------|
| ID_PARTICIPANTE     | Inteiro   | Chave primária (surrogate key) |
| NU_INSCRICAO        | String    | Número de inscrição |
| TP_FAIXA_ETARIA     | Inteiro   | Faixa etária do participante |
| TP_SEXO             | String    | Sexo do participante |
| TP_ESTADO_CIVIL     | Inteiro   | Estado civil |
| TP_COR_RACA         | Inteiro   | Cor ou raça declarada |
| TP_NACIONALIDADE    | Inteiro   | Nacionalidade |
| TP_ST_CONCLUSAO     | Inteiro   | Situação de conclusão do ensino médio |
| TP_ANO_CONCLUIU     | Inteiro   | Ano de conclusão |
| TP_ESCOLA           | Inteiro   | Tipo de escola frequentada |
| TP_ENSINO           | Inteiro   | Modalidade de ensino |
| IN_TREINEIRO        | Inteiro   | Indicador se o participante é “treineiro” |

---

## 🏠 DIM_SOCIOECONOMICO

| Coluna             | Tipo    | Descrição |
|--------------------|---------|-----------|
| ID_SOCIOECONOMICO  | Inteiro | Chave primária |
| NU_INSCRICAO       | String  | Número de inscrição |
| Q001 – Q025        | String  | Respostas do questionário socioeconômico |

> Exemplos:
> - Q001: Escolaridade do pai  
> - Q002: Escolaridade da mãe  
> - Q006: Renda familiar  
> - Q024: Acesso à internet  
> - Q025: Número de computadores no domicílio

---

## 📍 DIM_LOCAL_PROVA

| Coluna              | Tipo    | Descrição |
|---------------------|---------|-----------|
| ID_LOCAL_PROVA      | Inteiro | Chave primária |
| NU_INSCRICAO        | String  | Número de inscrição |
| CO_MUNICIPIO_PROVA  | Inteiro | Código do município da prova |
| NO_MUNICIPIO_PROVA  | String  | Nome do município da prova |
| CO_UF_PROVA         | Inteiro | Código da UF da prova |
| SG_UF_PROVA         | String  | Sigla da UF da prova |

---

## 🏫 DIM_LOCAL_ESCOLA

| Coluna                    | Tipo    | Descrição |
|---------------------------|---------|-----------|
| ID_LOCAL_ESCOLA           | Inteiro | Chave primária |
| NU_INSCRICAO              | String  | Número de inscrição |
| CO_MUNICIPIO_ESC          | Inteiro | Código do município da escola |
| NO_MUNICIPIO_ESC          | String  | Nome do município da escola |
| CO_UF_ESC                 | Inteiro | Código da UF da escola |
| SG_UF_ESC                 | String  | Sigla da UF da escola |
| TP_DEPENDENCIA_ADM_ESC    | Inteiro | Dependência administrativa (1=Federal, 2=Estadual, etc.) |
| TP_LOCALIZACAO_ESC        | Inteiro | Localização (1=Urbana, 2=Rural) |
| TP_SIT_FUNC_ESC           | Inteiro | Situação de funcionamento da escola |
