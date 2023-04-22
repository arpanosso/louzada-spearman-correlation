
<!-- README.md is generated from README.Rmd. Please edit that file -->

# louzada-spearman-correlation-update

``` r
library(tidyverse)
#> ── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
#> ✔ dplyr     1.1.1     ✔ readr     2.1.4
#> ✔ forcats   1.0.0     ✔ stringr   1.5.0
#> ✔ ggplot2   3.4.2     ✔ tibble    3.2.1
#> ✔ lubridate 1.9.2     ✔ tidyr     1.3.0
#> ✔ purrr     1.0.1     
#> ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
#> ✖ dplyr::filter() masks stats::filter()
#> ✖ dplyr::lag()    masks stats::lag()
#> ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors
dados <- readxl::read_excel("data/Correlação Entre CR , Cargo , Salário.xlsx")
glimpse(dados)
#> Rows: 60
#> Columns: 4
#> $ Nome    <chr> "Adriana Sampaio Costa de Souza", "Aguinaldo Castaldelli Neto"…
#> $ CR      <dbl> 7.68, 6.78, 7.59, 7.49, 6.98, 6.16, 6.30, 5.74, 6.89, 7.30, 7.…
#> $ Cargo   <chr> "Gerencia", "Gerencia", "Supervisão", "Operacional", "Gerencia…
#> $ Salário <dbl> 37000, 40000, 14000, 5000, 45800, 80000, 11000, 13000, 17500, …
```

## Teste de Pressuposições (normalidade)

### Histograma CR d

``` r
dados %>% 
  ggplot(aes(x=CR))+
  geom_histogram(bins=10, color="black", fill="gray")
```

![](README_files/figure-gfm/unnamed-chunk-3-1.png)<!-- -->

``` r
dados %>% pull(CR) %>% shapiro.test()
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  .
#> W = 0.97661, p-value = 0.3023
```

- Distribuição normal para os CRs.

### Histograma Salário

``` r
dados %>% 
  ggplot(aes(x=Salário))+
  geom_histogram(bins=10, color="black", fill="gray")
```

![](README_files/figure-gfm/unnamed-chunk-5-1.png)<!-- -->

``` r
dados %>% pull(Salário) %>% shapiro.test()
#> 
#>  Shapiro-Wilk normality test
#> 
#> data:  .
#> W = 0.7215, p-value = 2.357e-09
```

- Distribuição assimétrica não normal para Salário.

Devido à falta de normalidade, foi utilizada a correlação de Spearman.

## Correlação de Spearman

``` r
cor(dados %>% select(CR, Salário), method = "spearman")
#>                CR   Salário
#> CR      1.0000000 0.1421561
#> Salário 0.1421561 1.0000000
```

Foi observado que o coeficiente de correlação de postos de Spearman
entre Salário e CR foi de $0,14$, ou seja, foi maior que $0$ e menor que
$1$, indicando uma correlação positiva moderada entre as duas variáveis.
Isso significa que, à medida que uma variável aumenta, a outra também
aumenta, mas não de forma proporcional.
