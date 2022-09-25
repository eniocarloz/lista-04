---
title: "lista 4 - MQ"
author: "ENIO SOUZA"
date: "2022-09-06"
output:
  html_document: default
  pdf_document: default
---

```{r setup, include=FALSE}
knitr::opts_chunk$set(echo = FALSE)

```

## Estudos sobre extrativismo

Dados a seguir fazem parte da primeira versão de uma avaliação de políticas públicas.
O objetivo é analisar os dados da tabela 289 do IBGE sobre a produção extrativa vegetal no Brasil.

## IMPORTAÇÃO DE DADOS

```{r cars, echo = TRUE}

install.packages("tidyverse")
library("tidyverse")
library("dplyr")
install.packages("sidrar")
library("sidrar")
library("ggplot2")
library("ggpubr")

dados_extrativismo <- get_sidra(289, variable = "allxp", period = "last", geo = "Brazil",
geo.filter = NULL, classific = "all", category = "all", header = TRUE,
format = 4, digits = "default", api = NULL)

names(dados_extrativismo)[13] <- 'Tipo'
```

## GRÁFICO

gráfico com estimativas intervalares.

hipotese a ser trabalhada: a intervenção estatal influencia na estimativa de produção. 

```{r pressure, echo=TRUE}
slice(dados_extrativismo) %>%
   ggpubr::ggboxplot(x = "Variável", y = "Valor", fill="Variável")
```

