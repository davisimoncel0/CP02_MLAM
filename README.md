# CP02 - Regressão Linear com PIB e Índice ABCR

## Integrantes

| Nome completo | RM |
|---|---|
| Augusto de Souza Avila | 570839 |
| Davi Simoncelo | 571738 |
| João Pedro Sousa | 573962 |
| Matheus Evangelista | 568593 |
| Murilo Lima de Carvalho | 570156 |

## Objetivo

Analisar a relação entre a atividade econômica brasileira e o fluxo de veículos nas rodovias utilizando dados do PIB e do Índice ABCR entre 2006 e 2025.

## Dados

Foram utilizadas as seguintes bases:

- `PIB_IBGE_SIDRA_FINAL.csv` - Índice de volume do PIB a preços de mercado, obtido no IBGE.
- `ABRC_FINAL.csv` - Índice ABCR de fluxo total de veículos no Brasil.

Os dados utilizados são séries sem ajuste sazonal.

## Preparação

Como os dados do PIB são trimestrais, foi calculada a média dos quatro trimestres de cada ano.

Os dados do Índice ABCR são mensais, então foi calculada a média dos doze meses de cada ano.

A base utilizada na análise possui:

- `Ano`
- `PIB_indice`
- `ABCR_indice`

## Análise

Foi criado um gráfico de dispersão entre o índice do PIB e o Índice ABCR e calculada a correlação entre os dois indicadores.

Para a regressão linear foram utilizados:

- Entrada: `PIB_indice`
- Valor estimado: `ABCR_indice`
- Treino: 2006 a 2021
- Teste: 2022 a 2025

Os registros foram mantidos em ordem cronológica.

## Avaliação

O modelo foi avaliado utilizando MAE, MSE e R².

Também foi realizada a comparação entre os valores observados e os valores previstos para os quatro anos de teste.

## Conclusão

A análise permite observar a relação entre o índice de volume do PIB e o fluxo de veículos nas rodovias. A correlação indica o grau de relação entre os indicadores e as métricas permitem avaliar o desempenho da regressão linear.

Uma correlação alta não representa, por si só, uma relação de causa e efeito.

## Fontes

IBGE - Sistema IBGE de Recuperação Automática (SIDRA), Tabela 1620: https://sidra.ibge.gov.br/tabela/1620

ABCR - Índice ABCR: https://melhoresrodovias.org.br/indice-abcr_2/
