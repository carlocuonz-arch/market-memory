# Market Memory — Verbindliche Konvention (v2.0)

Single source of truth für Ablage, Benennung und Format. Gilt ab 2026-06-07. Ältere, abweichende Einträge liegen unter `_legacy/`.

## 1. Ablage (co-located)

Markdown und JSON eines Briefings liegen **zusammen** im selben Ordner:

```
briefings/YYYY/MM/YYYY-MM-DD_<type>.md
briefings/YYYY/MM/YYYY-MM-DD_<type>.json
scorecards/market_score_history.jsonl
templates/
_legacy/        # eingefrorene Alt-/Defekt-Einträge, read-only
```

`<type>` ∈ `europe_daily` | `us_daily` | `weekend`.

Beispiel: `briefings/2026/06/2026-06-07_weekend.md` (+ `.json`).

Verboten: verschachtelte Tagesordner (`MM/DD/`), `part_01`-Splits, separater `json/`-Baum, freie Dateinamen.

## 2. Sprache & Integrität

- Sprache: **Deutsch** (Finanzdeutsch). Keine englischen Einträge im Hauptbaum.
- **Keine erfundenen Werte.** Fehlt eine Zahl/ein Score, ist der Wert `null` (JSON) bzw. `N/A` (MD) — niemals geschätzt.
- Jeder Eintrag trägt eine `data_classification`:
  - `verified-live` — auf geprüften aktuellen Markt-/Newsdaten basierend.
  - `shared-context` — aus Briefing-Kontext/Decision-Memory abgeleitet, nicht unabhängig verifiziert.
  - Nie mischen ohne Label. *Plausible is not verified.*

## 3. Scorecard (fix, -2..+2)

Genau diese sieben Dimensionen, immer in dieser Reihenfolge. Nicht zutreffend → `null`.

`europe_tech` · `us_tech` · `health_rotation` · `risk_sentiment` · `volatility` · `rates` · `crypto_liquidity`

Skala: +2 stark positiv · +1 positiv · 0 neutral · -1 vorsichtig/negativ · -2 stark negativ.

## 4. Konfidenz

Immer Prozent als Ganzzahl 0–100 (`confidence.level_pct`). Kein `7/10`, kein „High".

## 5. JSON-Schema

Jedes Briefing-JSON folgt `templates/briefing.schema.json` (schema_version "2.0"). Pflichtfelder dürfen nicht fehlen; unbekannte Werte = `null`.

## 6. Score-History

Pro Briefing **eine** Zeile an `scorecards/market_score_history.jsonl` anhängen (siehe Schema-Kommentar dort). Append-only, eine JSON-Zeile pro `date`+`briefing_type`.

## 7. Export-Garantie (Reliability)

Der Export schreibt den **vollständigen** Briefing-Text — keine Kürzung, kein Chunking, kein `part_xx`. Validierung vor Commit:
- [ ] MD endet nicht mitten im Satz (letzte Zeile vollständig).
- [ ] MD- und JSON-`date`/`briefing_type` stimmen mit dem Dateinamen überein.
- [ ] Alle Schema-Pflichtfelder vorhanden, fehlende Werte `null`.
- [ ] Genau eine neue Zeile in `market_score_history.jsonl`.
