# Market Memory

Persönliches Marktjournal: pro Briefing ein lesbarer Markdown-Bericht **und** ein strukturierter JSON-Snapshot, plus eine fortlaufende Scorecard-History für schnelle Auswertung.

Verbindliche Regeln stehen in **[CONVENTION.md](CONVENTION.md)** (v2.0). Diese README ist die Kurzfassung.

## Struktur

```text
briefings/YYYY/MM/YYYY-MM-DD_<type>.md     # menschlich lesbar
briefings/YYYY/MM/YYYY-MM-DD_<type>.json   # maschinenlesbar (Schema v2.0)
scorecards/market_score_history.jsonl      # eine Zeile pro Briefing
templates/                                 # Vorlage + JSON-Schema
_legacy/                                    # eingefrorene Alt-/Defekt-Einträge
CONVENTION.md                              # verbindliche Konvention
```

`<type>` = `europe_daily` | `us_daily` | `weekend`.

## Scorecard-Skala

| Score | Bedeutung |
|---:|---|
| +2 | stark positiv |
| +1 | positiv |
| 0 | neutral |
| -1 | vorsichtig / negativ |
| -2 | stark negativ |

## Scorecard-Dimensionen (fix)

`europe_tech` · `us_tech` · `health_rotation` · `risk_sentiment` · `volatility` · `rates` · `crypto_liquidity`

## Grundprinzipien

- **Deutsch**, Finanzdeutsch. Keine erfundenen Werte — fehlt etwas, ist es `null` / `N/A`.
- Jeder Eintrag ist als `verified-live` oder `shared-context` klassifiziert. *Plausible is not verified.*
- Export schreibt den **vollständigen** Text — keine Kürzung, kein `part_xx`.

## Workflow

Briefing wird erzeugt → als `.md` gespeichert → paralleler `.json`-Snapshot (Schema v2.0) → eine Zeile an `market_score_history.jsonl` angehängt. Daraus lassen sich später Dashboard, Agent oder Vektor-DB bauen.
