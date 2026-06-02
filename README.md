# Market Memory

Persönliches Marktjournal für tägliche US-Marktbriefings.

Ziel: Jeden Handelstag als Markdown-Datei für Menschen und als JSON-Datei für Maschinen ablegen.

## Struktur

```text
briefings/
  YYYY/
    MM/
      YYYY-MM-DD.md
json/
  YYYY/
    MM/
      YYYY-MM-DD.json
scorecards/
  market_score_history.jsonl
templates/
  daily_briefing_template.md
  daily_scorecard_schema.json
```

## Grundprinzip

- `briefings/` enthält lesbare Tagesberichte.
- `json/` enthält strukturierte Tagesdaten.
- `scorecards/market_score_history.jsonl` enthält eine Zeile pro Markttag für schnelle Auswertung.
- `templates/` definiert das Standardformat.

## Score-Skala

| Score | Bedeutung |
|---:|---|
| +2 | stark positiv |
| +1 | positiv |
| 0 | neutral |
| -1 | vorsichtig / negativ |
| -2 | stark negativ |

## Haupt-Scores

- US Tech Momentum
- Health Rotation
- Risk Sentiment
- Volatility
- Bond Pressure
- Oil / Inflation Risk
- Crypto Tone

## Workflow

Täglich wird ein Briefing als Markdown gespeichert und parallel ein JSON-Snapshot erzeugt. Später kann daraus ein Friday-/Market-Memory-Agent, ein Dashboard oder eine Vektor-Datenbank gebaut werden.
