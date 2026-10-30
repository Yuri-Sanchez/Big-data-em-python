# Analise de Dados no Setor de Viagem e Turismo

Projeto pratico desenvolvido para a disciplina de Big Data em Python.

**Aluno:** Yuri Sanchez  
**Disciplina:** Big Data em Python  
**Linguagem:** Python 3  
**Repositório Oficial:** https://github.com/Yuri-Sanchez/Big-data-em-python  

---

## 1. Descricao do Projeto

O objetivo deste projeto e aplicar os conceitos fundamentais de Big Data e Ciencia de Dados para analisar uma base real de reservas hoteleiras no setor de viagem e turismo. O trabalho abrange todo o ciclo analitico: importacao remota de dados, diagnostico e tratamento de inconsistencias (Data Cleaning), calculo de metricas de negocio (KPIs), analises exploratorias estatisticas e construcao de um painel integrado (Dashboard) em tela unica.

A analise visa responder a perguntas criticas da gestao hoteleira:
* Quais meses do ano concentram a alta e a baixa temporada de viagens?
* Qual tipo de hospedagem (Hotel Urbano ou Resort) sofre maior taxa de cancelamento?
* Como o tempo de antecedencia da reserva impacta o cancelamento?
* Quais sao os principais mercados internacionais emissores de turistas?
* Como se comporta a dispersao dos precos das diarias em cada modalidade?

---

## 2. Origem da Base de Dados

A base de dados utilizada possui validacao cientifica internacional, correspondendo ao conjunto de dados Hotel Booking Demand Datasets, documentado pelos pesquisadores Nuno Antonio, Ana de Almeida e Luis Nunes (ISCTE-IUL, Portugal) e publicado no periodico internacional Data in Brief (Elsevier, 2019, DOI: 10.1016/j.dib.2018.11.126). 

Os dados foram disponibilizados atraves do projeto TidyTuesday da iniciativa R for Data Science.

Links de acesso:
* Link de Origem (TidyTuesday): https://github.com/rfordatascience/tidytuesday/blob/master/data/2020/2020-02-11/readme.md
* Download Direto da Base Bruta Original (hotels.csv): https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2020/2020-02-11/hotels.csv
* Link Direto da Base de Dados Tratada (Gist Publico): https://gist.githubusercontent.com/Yuri-Sanchez/026bd9aff0777b22f148efb3dab7005b/raw/dados_turismo.csv

---

## 3. Bibliotecas Utilizadas

O projeto foi construido exclusivamente em Python 3, utilizando as seguintes bibliotecas:

* **Pandas:** Utilizada para importacao do arquivo CSV via web (read_csv), inspecao estrutural (head, info, isnull), limpeza e higienizacao de dados (drop_duplicates, fillna), operacoes vetorizadas para engenharia de variaveis e calculos de agregacao estatistica (mean, median, value_counts, groupby, cut).
* **NumPy:** Biblioteca de computacao numerica que atua como o motor matematico subjacente ao Pandas e Seaborn, processando matrizes e operacoes vetorizadas com alta performance na memoria.
* **Matplotlib (matplotlib.pyplot):** Utilizada para criacao das figuras graficas (figure, subplots), desenho dos graficos de linha (plot) e colunas (bar), configuracao de titulos, eixos, rotulos percentuais nos topos das barras (text) e composicao do Dashboard 2x2.
* **Seaborn:** Utilizada para padronizacao estetica global dos graficos com fundo branco e grade suave (set_theme(style='whitegrid')) e renderizacao do diagrama estatistico de caixas (boxplot) para comparar a dispersao e a mediana das diarias.
* **WordCloud:** Utilizada para processamento visual de texto, compilando os nomes dos paises de origem e gerando a Nuvem de Palavras proporcional a recorrencia de cada nacionalidade.
* **Warnings:** Modulo nativo do Python utilizado com filterwarnings('ignore') para suprimir avisos cosmeticos e manter as celulas de saida limpas.

---

## 4. Tratamento e Limpeza de Dados (Data Cleaning)

A base bruta inicial continha 2.681 registros de reservas. As seguintes etapas de tratamento foram aplicadas:

1. **Remocao de Registros Duplicados:** Foram identificadas 28 linhas com valores 100% identicos em todas as colunas. A remocao foi executada via `df.drop_duplicates(inplace=True)`, consolidando a base em 2.653 reservas unicas e validas.
2. **Tratamento de Valores Nulos:**
   * Na coluna `pais_origem`, os campos ausentes foram preenchidos com `'Não Informado'` via `fillna()`, preservando os dados da reserva.
   * Na coluna `valor_diaria`, os valores faltantes foram substituidos pela mediana amostral (R$ 539,32), escolha metodologica que protege as metricas contra a distorcao de diarias atipicas de luxo (outliers).
   * Na coluna `qtd_criancas`, valores vazios foram assumidos como zero.
3. **Engenharia de Variaveis (Feature Engineering):**
   * `total_noites`: soma das noites de fim de semana com dias uteis.
   * `total_hospedes`: soma da quantidade de adultos e criancas.

---

## 5. Indicadores Principais de Desempenho (KPIs)

Apos o tratamento dos dados, foram calculados os seguintes indicadores-chave de negocio:

* **Total de Reservas Validas:** 2.653 estadias analisadas.
* **Taxa Geral de Cancelamento:** 37,09% (total de 984 reservas canceladas antes do check-in).
* **Valor Medio da Diaria (ADR):** R$ 539,32 por noite.
* **Media de Permanencia (Estadia):** 3,4 noites por reserva.

---

## 6. Analises Exploratorias Realizadas

O notebook contem 5 analises estatisticas individuais, 1 analise complementar e 1 painel consolidado:

1. **Analise 1 - Sazonalidade das Reservas por Mes:** Mapeamento do volume de viagens de Janeiro a Dezembro. Revela forte concentracao de alta temporada em Julho (282 reservas) e Agosto (307 reservas) durante as ferias de verao, e menor ocupacao em Janeiro (126) e Fevereiro (183).
2. **Analise 2 - Taxa de Cancelamento por Tipo de Hotel:** Comparativo demonstrando que Hoteis Urbanos possuem taxa de cancelamento substancialmente mais alta (41,9%) do que Resorts (27,5%), decorrente da volatilidade de viagens corporativas.
3. **Analise 3 - Cancelamento por Antecedencia da Reserva (Lead Time):** Segmentacao dos dias entre compra e check-in. Reservas de ultima hora (0 a 7 dias) possuem cancelamento de apenas 8,8%, enquanto reservas feitas com mais de 90 dias cancelam quase metade (49,6%).
4. **Analise 4 - Top 5 Paises de Origem dos Turistas:** Ranking liderado por Portugal (1.070 reservas), seguido por Reino Unido (276), Franca (224), Alemanha (184) e Espanha (172), demonstrando predominancia do mercado europeu.
5. **Analise 5 - Distribuicao do Valor da Diaria (Boxplot):** Diagrama de caixas avaliando a dispersao tarifaria. Hotel Urbano apresenta media de R$ 557,35 com valores concentrados na faixa central, enquanto o Resort apresenta media de R$ 503,59 com cauda mais dispersa em datas festivas.
6. **Analise Bonus - Nuvem de Palavras (WordCloud):** Sintese visual da frequencia textual das nacionalidades dos turistas.
7. **Dashboard Executivo Integrado:** Painel 2x2 com `plt.subplots` reunindo simultaneamente Sazonalidade, Risco de Cancelamento, Mercados Principais e Rentabilidade Tarifaria em tela unica.

---

## 7. Principais Conclusoes e Tomada de Decisao

Com base nos dados analisados, foram definidas 5 recomendacoes estrategicas para a gestao hoteleira:

1. **Gestao Ativa da Sazonalidade:** Contratacao antecipada de equipe temporaria em Maio/Junho para suportar o pico de Julho e Agosto, e criacao de pacotes promocionais 'early booking' para atrair demanda na baixa temporada (Janeiro e Fevereiro).
2. **Combate ao Cancelamento de Longo Prazo:** Como reservas feitas com mais de 90 dias cancelam quase metade (49,6%), o hotel deve oferecer descontos exclusivos (ex.: 15%) condicionados ao pagamento antecipado integral e estritamente nao-reembolsavel, travando a receita com meses de folga.
3. **Politicas Rigorosas para Hoteis Urbanos:** Hoteis Urbanos sofrem com 41,9% de cancelamento. Devem ser implementadas confirmacoes ativas via WhatsApp e e-mail 48 horas antes do check-in para liberar vagas ociosas para clientes de ultima hora.
4. **Marketing Internacional Focado:** Direcionar campanhas de marketing digital e parcerias com companhias aereas nos tres principais mercados emissores: Portugal, Reino Unido e Franca.
5. **Precificacao Dinamica Inteligente:** Aplicar tarifas mais elevadas no meio de semana para hoteis urbanos (viagens a negocios) e comercializar pacotes fechados premium para resorts em feriados prolongados.

---

## 8. Como Executar o Projeto

1. Clone o repositorio:
```bash
git clone https://github.com/Yuri-Sanchez/Big-data-em-python.git
cd Big-data-em-python
```

2. Certifique-se de ter as bibliotecas instaladas:
```bash
pip install pandas numpy matplotlib seaborn wordcloud
```

3. Inicie o Jupyter Notebook:
```bash
jupyter notebook projeto_viagem_turismo.ipynb
```

O arquivo baixa os dados automaticamente da internet e executa todas as etapas de limpeza, metricas, graficos e conclusoes.
