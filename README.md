## ETL ANP - Preços de Combustíveis com Databricks SQL

## 📋 Descrição

Projeto de Engenharia de Dados utilizando dados públicos da Agência Nacional do Petróleo (ANP), com construção de pipeline ETL na arquitetura Medalhão (Bronze, Silver e Gold) utilizando Databricks SQL.

O objetivo do projeto é transformar dados brutos de preços de combustíveis em um dataset confiável, padronizado e analítico para futuras análises de preço, variação temporal e comparação regional.

🏗️ Arquitetura do Pipeline

## Bronze → Silver → Gold

Bronze: ingestão dos dados brutos da ANP sem tratamento
Silver: limpeza, padronização, validação e deduplicação
Gold: camada analítica (agregações e métricas para BI) – em evolução

## 🥉 Camada Bronze (Dados Brutos)

Dados ingeridos diretamente da fonte da ANP
Sem tratamento de qualidade
Estrutura original preservada

## 📊 Contagem:

Bronze: 813731 linhas (SELECT COUNT(*))

Problemas identificados:

* Duplicidades
* Campos nulos em colunas críticas
* Inconsistência de tipos (string vs numérico)
* Variações de nomenclatura em produtos e unidades

🥈 Camada Silver (Dados Tratados)

Nesta etapa, os dados são transformados para garantir consistência, confiabilidade e padronização.

📊 Contagem:

* Bronze: 813731 linhas
* Silver: 804617 linhas
* Remoção: 9.114 linhas 
804617 - 9114
* Gold: 804617 linhas


🔧 Regras e Transformações Aplicadas

🧹 1. Deduplicação

Antes:
Registros repetidos por combinação de data + produto + revenda
Depois:
Remoção dos dados duplicados

❌ 2. Tratamento de Nulos

Antes:
Campos críticos (valor, data, produto) com nulos
Depois:
Remoção de registros inválidos em campos essenciais
Garantia de integridade analítica

⛽ 3. Padronização de Unidade de Medida

Antes:
"R$ / litro", "R$ / m³", "R$ / m3", "null"
Depois:
"R$ / litro", R$ / m³

Resultado:

Comparabilidade uniforme entre todos os registros

💰 4. Conversão de Tipos (Valor_Venda)

Antes:
STRING com inconsistências (vírgula/ponto/texto)
Depois:
DECIMAL(10,2)

Impacto:

Permite agregações corretas (AVG, SUM, MIN, MAX)

📅 5. Validação de Datas

Antes:
múltiplos formatos e datas inválidas
Depois:
formato DATE padronizado e filtrado

Impacto:

Base confiável para análise temporal

⛽ 6. Padronização de Produtos

Antes:
variações como “gasolina comum”, “gasolina comum aditivada”, etc.
Depois:
categorias normalizadas de combustíveis

Impacto:

Análise comparável entre produtos equivalentes

🏷️ 7. Padronização de Colunas

Antes:
"Valor Venda", "Data da Coleta", "Regiao - Sigla"
Depois:
valor_venda, data_coleta, regiao_sigla

🏷️ 8. Coluna Valor de Compra
não possuía preenchimento para o período analisado.
Adicionalmente, foi consultada a documentação oficial da ANP, que informa a descontinuação da coleta 
desse campo a partir do segundo semestre de 2020.
Por esse motivo a coluna foi removida da camada Silver.

Impacto:

Padrão analítico consistente (snake_case)

📌 Impacto da Camada Silver

Após o processamento:

Dataset 100% estruturado e padronizado
Redução de ruído e inconsistências
Dados prontos para consumo analítico
Base confiável para construção da camada Gold

## 🥇 Camada Gold (Evolução do Projeto)

Agregações por estado, produto e período
Cálculo de preço médio e variação temporal
Dataset otimizado para dashboards (Power BI / Databricks SQL)
Foco em análises estratégicas do mercado de combustíveis

## 🚀 Conclusão
Este projeto simula um pipeline real de engenharia de dados baseado em arquitetura medalhão, demonstrando habilidades em:
SQL em Databricks
Limpeza e transformação de dados
Modelagem de dados analíticos
Construção de datasets confiáveis para BI

A saida dessa tabela **gold_combustivel** será usada em um Projeto de ANP_Analytc que já está pronto.
E Será disponibilizado no Github.

