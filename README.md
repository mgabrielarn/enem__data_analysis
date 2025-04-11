# ETL e Análise dos Microdados do ENEM 2023

Este projeto foi desenvolvido como projeto final da sprint de Engenharia de Dados do curso de pós graduação em Ciência de Dados e Analytics pela PUC RIo de Janeiro. Em relação à estrutura de dados, faz-se a construção de um Data Warehouse baseado nos Microdados do ENEM 2023 (versão mais recente disponível), utilizando o modelo dimensional Estrela e Spark. O objetivo principal é fornecer informações sobre como as notas se distrubuem de acordo com fatores como UF, sexo, raça e ano de conclusão do ensino médio. Além disso, possibilitar análises dentro do questionário socioeconônimo como as relacionadas a renda familiar e nível de escolaridade dos pais.


O projeto foi desenvolvidos através do Databricks Community, com os dados armazenados no Google Drive (após estração do site oficial). Estão presentes nesse repositório o notebook com o pipeline do ETL (), o notebook com as análises e o catálogo de dados ().

---

## Fonte dos Dados

- **Microdados ENEM 2023**  
  Instituto Nacional de Estudos e Pesquisas Educacionais Anísio Teixeira (INEP)
  [https://www.gov.br/inep/pt-br/acesso-a-informacao/dados-abertos/microdados/enem](https://www.gov.br/inep/pt-br/acesso-a-informacao/dados-abertos/microdados/enem)


---

## Esquema Estrela

**Fato:**
- `fato_resultado_enem`: notas, presenças, status da redação

**Dimensões:**
- `dim_participante`: dados pessoais e escolares
- `dim_socioeconomico`: respostas ao questionário socioeconômico
- `dim_local_prova`: informações sobre o local da prova

---

## Documentação

- `catalogo_de_dados.md`: Catálogo de dados com descrições, domínios e linhagem

---

## Licença

Este projeto é de uso educacional.  
Os dados utilizados são públicos e disponibilizados pelo INEP.
