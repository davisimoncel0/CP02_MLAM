# Regressão linear com PIB e Índice ABCR

Este projeto investiga a relação entre a atividade econômica brasileira e o fluxo de veículos em rodovias pedagiadas usando dados do **IBGE** e da **ABCR**.

Foram utilizados **20 anos completos em comum, de 2006 a 2025**, sempre com as séries **sem ajuste sazonal** e com números-índice, conforme solicitado.

## Fontes

- **IBGE — Tabela 1620 do SIDRA:** Série encadeada do índice de volume trimestral, base média de 1995 = 100. Foi selecionado **Brasil** e **PIB a preços de mercado**.
  - https://sidra.ibge.gov.br/tabela/1620
  - Página do Sistema de Contas Nacionais Trimestrais: https://www.ibge.gov.br/estatisticas/economicas/contas-nacionais/9300-contas-nacionais-trimestrais.html
- **ABCR — Índice ABCR:** série original do **fluxo total de veículos**, número-índice com base 1999 = 100.
  - https://melhoresrodovias.org.br/indice-abcr_2/

Os arquivos originais usados na análise estão em `dados_originais/`.

## Preparação dos dados

As duas séries possuem frequências diferentes:

- PIB: 4 observações trimestrais por ano;
- ABCR: 12 observações mensais por ano.

Para cada ano, foi calculada a média simples das observações disponíveis:

- `PIB_indice`: média dos quatro índices trimestrais;
- `ABCR_indice`: média dos doze índices mensais.

Foi feita uma verificação de completude e todos os anos de 2006 a 2025 possuem exatamente 4 trimestres do PIB e 12 meses do ABCR.

A base anual final está em `dados/dados_anuais.csv`.

## Modelo

Foi utilizada uma regressão linear simples:

- **X:** `PIB_indice`;
- **y:** `ABCR_indice`;
- **Treino:** 2006 a 2021, total de 16 anos;
- **Teste:** 2022 a 2025, total de 4 anos;
- Registros mantidos em ordem cronológica, sem embaralhamento.

Modelo ajustado no conjunto de treino:

```text
ABCR_indice = -56.7856 + 1.2145 × PIB_indice
```

## Resultados

A correlação de Pearson entre os dois índices nos 20 anos foi:

```text
r = 0.9641
```

Esse valor indica uma associação linear positiva forte: em geral, anos com maior índice de volume do PIB também apresentam maior índice ABCR. Isso **não prova causalidade**.

No conjunto de teste:

| Métrica | Valor |
|---|---:|
| MAE | 4.9489 |
| MSE | 25.9502 |
| R² | 0.4849 |

### Previsões no teste

| Ano | ABCR observado | ABCR previsto |
|---:|---:|---:|
| 2022 | 154.1235 | 159.4589 |
| 2023 | 163.4908 | 166.4667 |
| 2024 | 168.8758 | 174.1001 |
| 2025 | 173.1204 | 179.3803 |

O **MAE de 4.95** significa que, em média, as previsões ficaram aproximadamente 4,95 pontos de índice distantes dos valores observados. O **MSE de 25.95** penaliza mais fortemente erros maiores. O **R² de 0.485** indica que, nesses quatro anos de teste, o modelo explica aproximadamente 48,5% da variação observada do Índice ABCR.

Apesar da correlação alta no período completo, o desempenho fora da amostra foi apenas moderado. Nos quatro anos de teste, o modelo superestimou o ABCR em todos os casos. Isso mostra que uma relação histórica forte entre as séries não garante previsões perfeitas, principalmente quando existem choques ou mudanças estruturais ao longo do tempo.

## Dificuldades e soluções

1. **Frequências diferentes:** o PIB é trimestral e o ABCR é mensal. A solução foi transformar ambos em médias anuais.
2. **Identificação da série correta:** no ABCR foi usada a aba de **série original**, coluna **TOTAL**, evitando a série dessazonalizada.
3. **Números-índice com bases diferentes:** o PIB usa média de 1995 = 100 e o ABCR usa 1999 = 100. Isso não impede a regressão, pois a análise estuda a associação entre as escalas, e não a igualdade numérica entre os índices.
4. **Divisão temporal:** foi evitado o `train_test_split` com embaralhamento. Os 16 primeiros anos foram usados no treino e os quatro últimos no teste.
5. **Revisões estatísticas:** séries do IBGE podem ser revisadas ao longo do tempo. Por isso, os arquivos originais usados nesta execução foram mantidos no repositório.

## Estrutura

```text
regressao-pib-indice-abcr/
├── README.md
├── regressao_pib_abcr.ipynb
├── requirements.txt
├── dados/
│   ├── pib_trimestral.csv
│   ├── abcr_mensal.csv
│   └── dados_anuais.csv
├── dados_originais/
│   ├── ibge_sidra.csv
│   └── abcr_0826.xlsx
└── resultados/
    ├── metricas.csv
    ├── previsoes_teste.csv
    ├── dispersao_pib_abcr.png
    └── observado_vs_previsto.png
```

## Como executar

Instale as dependências:

```bash
pip install -r requirements.txt
```

Depois abra e execute o notebook `regressao_pib_abcr.ipynb`.

## Conclusão

Os dados de 2006 a 2025 mostram uma associação linear positiva forte entre o índice de volume do PIB e o Índice ABCR, com correlação de aproximadamente **0.964**. A regressão treinada até 2021 consegue acompanhar a direção geral dos anos seguintes, mas apresenta erro médio próximo de 5 pontos de índice e R² de aproximadamente **0.485** no teste.

Portanto, o fluxo de veículos em rodovias pedagiadas apresenta relação estatística relevante com a atividade econômica brasileira, mas o PIB sozinho não explica toda a variação do Índice ABCR. Correlação e regressão linear não devem ser interpretadas como prova de causa e efeito.
