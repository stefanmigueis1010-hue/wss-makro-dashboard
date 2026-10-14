# WSS Makro-Dashboard

Wöchentliches Forex-Makro-Dashboard für stef_life Trading.

## Aufbau

```
/index.html          – Dashboard-Seite (Design schwarz/gold, lädt data.json)
/data.json           – Aktuelle Daten (wird bei jedem Lauf überschrieben)
/history/            – Archiv: eine Datei pro Lauf (YYYY-MM-DD.json)
/README.md           – Diese Datei
```

## Datenquellen

| Daten | Quelle |
|-------|--------|
| DXY, S&P 500, VIX, US-10Y, Gold, USD/JPY | Yahoo Finance Chart API |
| COT-Daten | CFTC Public Reporting API (Socrata, Dataset jun7-fc8e) |
| Wirtschaftskalender | TradingView Economic Calendar API |
| Einschätzung (Bias, Pairs, Status) | Claude API (Anthropic) |

## Automatisierung

n8n-Workflow „WSS Makro-Dashboard":
- **Montag 07:00 Uhr** (Europe/Berlin): Vollständiges Update, Vergleich zur Vorwoche
- **Mittwoch 07:00 Uhr** (Europe/Berlin): Mid-Week Update, Vergleich zu Montag

## Manueller Start

Im n8n-Workflow den Manual Trigger ausführen. Der Workflow:
1. Holt Marktdaten von Yahoo Finance
2. Holt COT-Daten von CFTC
3. Holt Wirtschaftskalender von TradingView
4. Erstellt Einschätzung via Claude API
5. Validiert und committet data.json + history/YYYY-MM-DD.json
6. Sendet Telegram-Bestätigung

## GitHub Pages

URL: https://stefanmigueis1010-hue.github.io/wss-makro-dashboard/
