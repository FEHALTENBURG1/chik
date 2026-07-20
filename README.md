# Painel HTML — Chikungunya na RIDE-DF

Este painel substitui o aplicativo Shiny por uma página HTML estática. Os cálculos são executados no navegador e os dados são carregados diretamente do repositório:

- `dados/chikungunya_ride.csv`
- `dados/atraso_nacional.csv`
- `populacao_ride.csv`
- `dados/ride.geojson`

## Publicação no GitHub Pages

1. Coloque o arquivo `index.html` na raiz do repositório que hospedará o painel.
2. No GitHub, abra **Settings > Pages**.
3. Em **Build and deployment**, selecione **Deploy from a branch**.
4. Escolha a branch `main` e a pasta `/ (root)`.
5. Salve e abra o endereço informado pelo GitHub Pages.

O painel tenta primeiro os arquivos do repositório remoto `FEHALTENBURG1/dados_chikungunya`. Se a busca remota falhar, tenta arquivos locais com os mesmos nomes.

## Definições implementadas

- Casos confirmados: `CLASSI_FIN == 13`.
- Em investigação: `CLASSI_FIN` vazio, `0`, `8` ou `9`.
- Positividade RT-PCR: `RESUL_PCR_ == 1` dividido por `RESUL_PCR_` igual a `1` ou `2`.
- Inconclusivos, não realizados e campos vazios ficam fora do denominador da positividade.
- As curvas usam prioritariamente `SEM_PRI`; na ausência, usam `ANO_EPI` + `SE`; como contingência, calculam a semana a partir de `DT_SIN_PRI`.
- Dimensão territorial dos mapas: município de residência.
- Alertas laboratoriais: município notificante, quando essa informação está disponível.

## Dependências carregadas por CDN

- Papa Parse
- Chart.js
- Leaflet

A página precisa de acesso à internet para carregar as bibliotecas, os dados e o mapa-base.

## Diagrama de controle

A semana epidemiológica mais recente permanece apresentada na curva, mas é tratada como preliminar. A classificação de situação — Controle, Segurança, Alerta ou Epidemia — utiliza a semana epidemiológica anterior, reduzindo o efeito da incompletude dos dados mais recentes.
## Regra do canal endêmico

A semana epidemiológica mais recente é considerada preliminar e não aparece no canal endêmico. O gráfico, o selo de situação e a lista de semanas consolidadas terminam na semana imediatamente anterior.
