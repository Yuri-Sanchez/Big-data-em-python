# Trabalho de Big Data em Python - Viagem e Turismo

**Aluno:** Yuri Sanchez  
**Disciplina:** Big Data em Python  

---

## Descrição do Projeto

Este projeto faz uma análise de dados sobre o setor de viagem e turismo, utilizando uma base real de reservas de hotéis (hotéis urbanos e resorts). 

O objetivo do trabalho foi importar os dados, fazer a limpeza e o tratamento (remoção de duplicadas e preenchimento de valores nulos), gerar gráficos para entender o comportamento das viagens e montar um dashboard com os principais indicadores para ajudar na tomada de decisões.

---

## Base de Dados

Os dados utilizados são reais e foram retirados do repositório TidyTuesday (Hotel Booking Demand):
* **Link de origem da base:** https://github.com/rfordatascience/tidytuesday/blob/master/data/2020/2020-02-11/readme.md
* **Link direto do CSV utilizado no notebook:** https://gist.githubusercontent.com/Yuri-Sanchez/026bd9aff0777b22f148efb3dab7005b/raw/dados_turismo.csv

---

## Bibliotecas Utilizadas

* **pandas:** para carregar a base, tratar dados nulos, remover duplicadas e fazer agrupamentos.
* **numpy:** suporte para operações matemáticas e vetoriais do pandas.
* **matplotlib:** para criar os gráficos de linhas, colunas e montar o dashboard em grade.
* **seaborn:** para aplicar o estilo visual dos gráficos e desenhar o boxplot das diárias.
* **wordcloud:** para gerar a nuvem de palavras com os países dos turistas.

---

## O que foi feito no projeto

1. **Carga e limpeza dos dados:**
   * Leitura direta do CSV pela internet.
   * Remoção de 28 linhas duplicadas, restando 2.653 reservas válidas.
   * Preenchimento de valores ausentes (mediana para diárias e "Não Informado" para países).
   * Criação das colunas `total_noites` e `total_hospedes`.

2. **Indicadores Principais (KPIs):**
   * Total de Reservas: 2.653
   * Taxa de Cancelamento: 37,09%
   * Valor Médio da Diária: R$ 539,32
   * Média de Noites: 3,4 noites

3. **Gráficos gerados:**
   * Sazonalidade das reservas ao longo dos 12 meses.
   * Comparativo de cancelamento entre Hotel Urbano e Resort.
   * Cancelamento por tempo de antecedência da reserva.
   * Top 5 países que mais enviam turistas.
   * Distribuição dos valores das diárias (Boxplot).
   * Nuvem de palavras com as nacionalidades.
   * Dashboard com 4 gráficos reunidos em uma tela só (`plt.subplots`).

---

## Principais Conclusões

1. **Sazonalidade:** Julho e Agosto são os meses com maior movimento de viagens (férias de verão), enquanto Janeiro e Fevereiro têm a menor procura.
2. **Cancelamentos:** Hotéis urbanos cancelam muito mais (41,9%) do que resorts (27,5%), principalmente por conta de viagens a trabalho que mudam de data.
3. **Antecedência:** Reservas feitas com mais de 90 dias de antecedência têm quase 50% de cancelamento. Reservas de última hora (0 a 7 dias) quase não cancelam (menos de 9%).
4. **Origem dos turistas:** Portugal é o maior emissor de hóspedes da base, seguido por Reino Unido, França, Alemanha e Espanha.
5. **Decisão para o negócio:** Criar tarifas promocionais com desconto para quem pagar adiantado sem direito a reembolso (para evitar cancelamentos com mais de 3 meses), e lançar promoções para a baixa temporada no início do ano.
