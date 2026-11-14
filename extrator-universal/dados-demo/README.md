# Dados de demonstração — camada Silver (workspace "TCC — Inflação")

Amostra real exportada do DataHub em 14/11/2026: **1.039 registros** de 5 países (BRA, CHL, COL, MEX, PER), de 2000 a 2026, já com o contrato Silver aplicado.

| Categoria | Indicador | Código | Fonte | Frequência |
|---|---|---|---|---|
| Inflação | IPCA mensal (%) | SGS 433 | BCB SGS | mensal |
| Inflação | IPCA acumulado em 12 meses | SGS 13522 | BCB SGS | mensal |
| Inflação | Inflação ao consumidor (% a.a.) | FP.CPI.TOTL.ZG | Banco Mundial (WDI) | anual |
| Juros | Selic acumulada no mês, anualizada (base 252) | SGS 4189 | BCB SGS | mensal |
| Câmbio | Câmbio oficial (moeda local por US$, média) | PA.NUS.FCRF | Banco Mundial (WDI) | anual |
| Câmbio | Fator de conversão PPC | PA.NUS.PPP | Banco Mundial (WDI) | anual |
| PIB | Crescimento do PIB (% a.a.) | NY.GDP.MKTP.KD.ZG | Banco Mundial (WDI) | anual |
| PIB | PIB per capita PPC (US$ internacionais de 2021) | NY.GDP.PCAP.PP.KD | Banco Mundial (WDI) | anual |

## Colunas

| Coluna | Descrição |
|---|---|
| `data_ref` | Data de referência em ISO 8601 (1º dia do período) |
| `iso3`, `pais` | País (ISO 3166-1 alfa-3) |
| `categoria`, `indicador`, `codigo`, `frequencia` | Identificação da série |
| `valor` | Valor numérico, na unidade do indicador |
| `fonte`, `origem` | Fonte oficial e canal de entrada (`n8n` ou `chatops`) |
| `url_origem` | URL exata de onde o dado foi baixado |
| `hash_conteudo` | SHA-256 do registro, usado na deduplicação e na auditoria |

## Uso rápido

```python
import pandas as pd

df = pd.read_csv("silver_tcc_inflacao.csv", parse_dates=["data_ref"])
ipca = df.query("codigo == 'SGS 433'").set_index("data_ref")["valor"]
print(ipca.tail(12))
```

```r
library(readr); library(dplyr)
df <- read_csv("silver_tcc_inflacao.csv")
df |> filter(categoria == "Inflação", frequencia == "anual") |> group_by(iso3) |> summarise(media = mean(valor, na.rm = TRUE))
```

Os dados são públicos, das fontes indicadas; a curadoria e o pipeline são do DataHub. Quer conferir um número? Use a `url_origem` da linha.
