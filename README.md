
<!-- README.md is generated from README.Rmd. Please edit that file -->

# Mananciais

<!-- badges: start -->

[![R build
status](https://github.com/beatrizmilz/mananciais/workflows/R-CMD-check/badge.svg)](https://github.com/beatrizmilz/mananciais/actions)
[![Lifecycle:
experimental](https://img.shields.io/badge/lifecycle-experimental-orange.svg)](https://www.tidyverse.org/lifecycle/#experimental)
<!-- badges: end -->

O objetivo deste pacote é disponibilizar a base de dados sobre volume
armazenado em mananciais de abastecimento público na Região
Metropolitana de São Paulo (SP - Brasil).

Os dados foram obtidos no [Portal dos
Mananciais](http://mananciais.sabesp.com.br/Situacao) da
[SABESP](http://site.sabesp.com.br/site/Default.aspx).

Este pacote foi derivado de um código web scraping desenvolvido pela
equipe da [Curso-R](https://www.curso-r.com/), em uma
[live](https://youtu.be/jvZIxrMmOcQ), e o código original está
disponível [neste
link](https://github.com/curso-r/lives/blob/master/drafts/20200730_scraper_sabesp.R).

## Instalação

Este pacote pode ser instalada através do [GitHub](https://github.com/)
utilizando:

``` r
# install.packages("devtools")
devtools::install_github("beatrizmilz/mananciais")
```

## Como usar?

Existem dois arquivos disponíveis, em que a diferença é o período dos
dados. Caso você não utilize `R` e queira ter acesso aos dados em
formato `.csv`, os mesmos podem ser acessados através dos links a
seguir. Lembrete: o arquivo foi salvo em formato “separado por ponto e
vírgula”, e com encoding “UTF-8”.

  - `mananciais_consolidado` - 2000 à 2019 - [Baixar versão
    `.csv`](https://github.com/beatrizmilz/mananciais/raw/master/inst/extdata/mananciais_consolidado.csv)

  - `mananciais` - 2000 à 2020 (parcial) - [Baixar versão
    `.csv`](https://github.com/beatrizmilz/mananciais/raw/master/inst/extdata/mananciais.csv).
    Esse arquivo é atualizado através de um workflow no [GitHub
    Actions](https://github.com/beatrizmilz/mananciais/actions).

Abaixo segue um exemplo das bases disponíveis:

``` r
library(mananciais)

dplyr::glimpse(mananciais)
#> Rows: 46,573
#> Columns: 8
#> $ data                [3m[90m<date>[39m[23m 2020-10-18, 2020-10-18, 2020-10-18, 2020-10-18, …
#> $ sistema             [3m[90m<chr>[39m[23m "Cantareira", "Alto Tietê", "Guarapiranga", "Coti…
#> $ volume_porcentagem  [3m[90m<dbl>[39m[23m 37.5, 57.2, 45.8, 60.6, 77.0, 54.4, 63.2, 37.7, 5…
#> $ volume_variacao     [3m[90m<dbl>[39m[23m -0.2, -0.2, -0.2, -0.2, -0.1, -0.5, -0.1, -0.3, -…
#> $ volume_operacional  [3m[90m<dbl>[39m[23m 368.54617, 320.71700, 78.47484, 10.00515, 86.3812…
#> $ pluviometria_dia    [3m[90m<dbl>[39m[23m 0.0, 0.0, 0.0, 0.0, 0.2, 0.0, 0.2, 0.2, 1.1, 0.8,…
#> $ pluviometria_mensal [3m[90m<dbl>[39m[23m 27.6, 34.6, 36.6, 44.8, 49.2, 61.4, 41.0, 27.6, 3…
#> $ pluviometria_hist   [3m[90m<dbl>[39m[23m 127.8, 113.4, 114.9, 113.5, 133.2, 176.1, 141.2, …

dplyr::glimpse(mananciais_consolidado)
#> Rows: 44,529
#> Columns: 8
#> $ data                [3m[90m<date>[39m[23m 2000-01-01, 2000-01-01, 2000-01-01, 2000-01-01, …
#> $ sistema             [3m[90m<chr>[39m[23m "Cantareira", "Alto Tietê", "Guarapiranga", "Coti…
#> $ volume_porcentagem  [3m[90m<dbl>[39m[23m 47.1, 50.9, 36.0, 18.8, 81.0, 73.2, 47.8, 51.4, 3…
#> $ volume_variacao     [3m[90m<dbl>[39m[23m 0.3, 0.1, 0.0, 0.9, 0.4, -0.2, 0.7, 0.5, 0.4, 0.0…
#> $ volume_operacional  [3m[90m<dbl>[39m[23m 365.50555, 196.02547, 64.80029, 2.64579, 91.69406…
#> $ pluviometria_dia    [3m[90m<dbl>[39m[23m 30.9, 26.0, 47.2, 0.0, 0.0, 5.2, 29.1, 47.3, 9.2,…
#> $ pluviometria_mensal [3m[90m<dbl>[39m[23m 30.9, 26.0, 47.2, 0.0, 0.0, 5.2, 60.0, 73.3, 56.4…
#> $ pluviometria_hist   [3m[90m<dbl>[39m[23m 254.8, 238.1, 225.2, 217.8, 235.4, 292.0, 254.8, …
```

Caso queira saber o significado de cada variável, leia a [documentação
da base de
dados](https://beatrizmilz.github.io/mananciais/reference/mananciais.html)
ou utilize a seguinte função:

``` r
?mananciais::mananciais
```

Caso você queira utilizar a base mais atual, sem que seja necessário
reinstalar o pacote, recomendo que utilize o seguinte código:

``` r
mananciais <- readr::read_csv2("https://github.com/beatrizmilz/mananciais/raw/master/inst/extdata/mananciais.csv")
#> [36mℹ[39m Using [34m[34m','[34m[39m as decimal and [34m[34m'.'[34m[39m as grouping mark. Use [30m[47m[30m[47m`read_delim()`[47m[30m[49m[39m for more control.
#> 
#> [36m──[39m [1m[1mColumn specification[1m[22m [36m────────────────────────────────────────────────────────[39m
#> cols(
#>   data = [34mcol_date(format = "")[39m,
#>   sistema = [31mcol_character()[39m,
#>   volume_porcentagem = [32mcol_double()[39m,
#>   volume_variacao = [32mcol_double()[39m,
#>   volume_operacional = [32mcol_double()[39m,
#>   pluviometria_dia = [32mcol_double()[39m,
#>   pluviometria_mensal = [32mcol_double()[39m,
#>   pluviometria_hist = [32mcol_double()[39m
#> )
```

### Exemplo de tabela

``` r
mananciais %>% 
  dplyr::arrange(desc(data)) %>% 
  head(7) %>%
  knitr::kable()
```

| data       | sistema      | volume\_porcentagem | volume\_variacao | volume\_operacional | pluviometria\_dia | pluviometria\_mensal | pluviometria\_hist |
| :--------- | :----------- | ------------------: | ---------------: | ------------------: | ----------------: | -------------------: | -----------------: |
| 2020-10-18 | Cantareira   |                37.5 |            \-0.2 |           368.54617 |               0.0 |                 27.6 |              127.8 |
| 2020-10-18 | Alto Tietê   |                57.2 |            \-0.2 |           320.71700 |               0.0 |                 34.6 |              113.4 |
| 2020-10-18 | Guarapiranga |                45.8 |            \-0.2 |            78.47484 |               0.0 |                 36.6 |              114.9 |
| 2020-10-18 | Cotia        |                60.6 |            \-0.2 |            10.00515 |               0.0 |                 44.8 |              113.5 |
| 2020-10-18 | Rio Grande   |                77.0 |            \-0.1 |            86.38127 |               0.2 |                 49.2 |              133.2 |
| 2020-10-18 | Rio Claro    |                54.4 |            \-0.5 |             7.43732 |               0.0 |                 61.4 |              176.1 |
| 2020-10-18 | São Lourenço |                63.2 |            \-0.1 |            56.13508 |               0.2 |                 41.0 |              141.2 |
