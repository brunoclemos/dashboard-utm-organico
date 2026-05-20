# Dashboard de Leads e Faturamento por UTM — Orgânico 2026

Visualização de leads e faturamento do tráfego orgânico em 2026, com quebra por UTM e por classificação Typeform (Closer / SDR / Perdido / Outros).

**URL:** https://brunoclemos.github.io/dashboard-utm-organico/

## O que mostra

- **KPIs gerais:** total de leads, qualificados (Closer), médios (SDR), faturamento total, ticket médio e conversão.
- **Stacked bar:** leads por UTM segmentados por classificação.
- **Bar chart:** faturamento por UTM.
- **Donuts:** mix de classificação geral e share de faturamento por UTM.
- **Conversão:** taxa de lead → negócio ganho por UTM.
- **Tabela detalhada:** ordenável por qualquer coluna.

Todos os gráficos têm tooltip com valores absolutos, percentuais e métricas cruzadas ao passar o mouse.

## Fonte dos dados

Exportações HubSpot (relatórios `organico-2026-novos-negocio` e `organico-2026-ganhos-x-utm`) — corte em 2026-05-19.

## Limitações

- Sem coluna de data nos CSVs originais → não há quebra por mês. Para habilitar, re-exportar do HubSpot incluindo "Data de criação" / "Data de fechamento".
- UTMs normalizadas: variantes (`yt-org` / `yt_org` / `YT-ORG`) agrupadas; `@@MISSING@@` → "Sem UTM".

## Atualização

Os dados estão embedados em `index.html` (constante `DATA`). Para atualizar:

1. Re-exportar do HubSpot.
2. Regenerar o JSON e substituir o objeto `DATA` em `index.html`.
3. Commit + push — GitHub Pages publica automaticamente.
