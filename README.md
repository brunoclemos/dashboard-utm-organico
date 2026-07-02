# Dashboard de Leads, ROAS e Tráfego por UTM — 2026

Visualização de leads, faturamento, **ROAS por canal de aquisição** e **funil de tráfego (Meta + Google)**, alimentada **ao vivo** direto do Google Sheets.

**URL:** https://brunoclemos.github.io/dashboard-utm-organico/

## O que mostra

- **KPIs gerais:** leads, investimento (Meta + Google), faturamento ganho, ROAS pago, negócios ganhos, ticket médio, CPL e conversão.
- **ROAS por canal de aquisição:** ROAS dos canais pagos, faturamento por canal e tabela completa (leads, investimento, ganhos, ROAS, CPL, CAC, conversão).
- **Evolução mensal por canal:** leads e faturamento empilhados por canal × mês + ROAS Meta vs Google.
- **Painel Meta Ads (isolado):** funil completo (impressões → cliques → LPV → conversões → ganhos), KPIs (CTR, CPM, CPC, CPA, ROAS), gráfico diário, **performance por campanha** (ROAS, faturamento e leads qualificados) e **ranking de criativos** (com faturamento e ROAS por criativo).
- **Painel Google Ads (isolado):** funil, KPIs, **performance por campanha** e **ranking de anúncios** (ROAS, faturamento e leads qualificados por anúncio, com rollup anúncio → campanha).
- **Atribuição por campanha/anúncio:** cruza `utm_campaign` e `utm_content` do lead com os nomes de campanha/anúncio das abas de tráfego, por nome normalizado (ignora espaço, underscore, hífen e acento) e escopado por canal. Leads qualificados = Closer + SDR. "(sem atribuição)" = lead/venda do canal sem correspondência de nome.
- **Qualidade dos leads por canal:** classificação Typeform (Closer / SDR / Perdido).

## Fonte dos dados (ao vivo)

Os dados são puxados em tempo real da planilha do Google Sheets via endpoint CSV do gviz (com CORS liberado para o domínio do GitHub Pages). Não há dados embedados — sempre reflete a planilha.

| Métrica | Aba | Como |
|---|---|---|
| Leads | `Todos os Negócios - 2026` | `COUNT` por utm_source/medium/campaign × mês × classificação; utm_content por src/medium/classificação |
| Faturamento / ganhos | `Negócios ganhos - 2026` | linhas cruas (valor, utm_campaign, utm_content, source, medium) + soma no navegador (ver nota abaixo) |
| Investimento + tráfego Meta | `Meta Ads` | `SUM` por dia, por campanha e por criativo (Ad Name) |
| Investimento + tráfego Google | `Google Ads` | `SUM` por dia, por campanha e por anúncio (Ad Name → Campaign) |

A planilha precisa estar compartilhada como **"qualquer pessoa com o link pode ver"**.

### Classificação de canal

Pela combinação `utm_source` + `utm_medium` do lead/negócio:
- `FB_*` / `fb_` / `ig_Instagram` / `paid` / Audience Network → **Meta Ads**
- `Search` e `YT_*` / Demand Gen (`DMG`) → **Google Ads**
- `*-ORG` / `*_ORG` / `social` → **orgânico** (YouTube / Instagram)
- sem UTM → **Sem UTM** (canal próprio, fora do ROAS pago)

### ROAS

`ROAS = faturamento atribuído ao canal (via UTM do lead) ÷ investimento do canal`. Apenas Meta e Google têm custo de mídia; canais orgânicos aparecem como "Orgânico".

## Notas técnicas

- **"Valor fechado" com formatação mista:** algumas células dessa coluna estão formatadas como data, o que **infla o `SUM` do gviz**. Por isso o faturamento é puxado linha a linha e somado no navegador (apenas ~1.000 linhas).
- **Sem UTM:** ~27% do faturamento ganho está sem UTM no CRM — aparece como canal próprio e não entra no ROAS pago.
- **Conversão lead → ganho** é um indicador (ganhos ÷ leads no período); são coortes diferentes, leia como tendência.

## Auth

Acesso restrito via Supabase (email/senha + allowlist). Editar `ALLOWED_EMAILS` em `index.html` para liberar novos acessos.

## Atualização

Não precisa regenerar nada — a dashboard lê a planilha ao vivo. Basta a planilha estar atualizada. O botão de refresh no cabeçalho recarrega os dados sob demanda.
