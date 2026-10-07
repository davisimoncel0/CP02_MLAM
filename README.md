# Regressão Linear com PIB e Índice ABCR

Este trabalho analisa a relação entre a atividade econômica brasileira e o fluxo de veículos nas rodovias.

Foram utilizados dados de 2006 a 2025.

## Fontes

- IBGE - Tabela 1620 do SIDRA
- ABCR - Índice ABCR

Para o PIB, foi utilizado o índice de volume do PIB a preços de mercado, sem ajuste sazonal.

Para o Índice ABCR, foi utilizada a série original do fluxo total de veículos no Brasil.

## Preparação dos dados

Os dados do PIB são trimestrais, por isso foi calculada a média dos quatro trimestres de cada ano.

Os dados da ABCR são mensais, então foi calculada a média dos doze meses de cada ano.

A base final ficou com as colunas:

- Ano
- PIB_indice
- ABCR_indice

## Análise

Foi feito um gráfico de dispersão entre o índice do PIB e o Índice ABCR e calculada a correlação entre os dois indicadores.

Depois foi treinado um modelo de regressão linear utilizando:

- PIB_indice como entrada
- ABCR_indice como valor a ser estimado
- 2006 a 2021 para treino
- 2022 a 2025 para teste

Os dados foram mantidos em ordem cronológica.

## Avaliação

O modelo foi avaliado utilizando MAE, MSE e R².

Também foi feita uma comparação entre os valores reais e os valores previstos pelo modelo.

## Conclusão

Os resultados mostraram uma relação positiva entre o índice do PIB e o Índice ABCR.

A correlação encontrada foi alta, mas isso não significa que exista uma relação direta de causa e efeito entre os dois indicadores.

O modelo apresentou desempenho moderado nos dados de teste, mostrando que o PIB ajuda a explicar o comportamento do fluxo de veículos, mas outros fatores também podem influenciar o Índice ABCR.
