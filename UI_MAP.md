# 🗺️ Mundiporra Dashboard — UI Map
> Kanonische Komponentennamen für Patrick ↔ Claude Kommunikation
> Stand: v1.21.4 · Repo: `Flash777777/mundiporra-staging` + `mundiporra-dashboard`

**Konvention:** `Kanonischer Name` → `fn()` / `#id` / `.class`
Wenn Patrick "X" sagt → Claude adressiert exakt den Code hinter "X". Keine Interpretation.

---

## GLOBALE SHELL

```
┌─────────────────────────────────────────────────────────┐
│  STAGING BANNER          .staging-banner                │  ← nur staging-URL sichtbar
│─────────────────────────────────────────────────────────│
│  HEADER                                                 │
│    App-Titel (statisch)  Version Badge  #headerVersionBadge │
│─────────────────────────────────────────────────────────│
│  TAB-NAV BAR                                            │
│  [📋 Zusammenfassung] [🏆 Rangliste] [👥 Gruppe]        │
│  [⚔️ Vergleich] [⚽ Spiele] [⭐ Campeones]              │
│  [📊 Statistiken] [🔍 Suche] [🗄️ Datenbasis] [📝 Log]  │
└─────────────────────────────────────────────────────────┘
```

### Globale Modals (immer verfügbar, tab-unabhängig)

| Kanonischer Name     | ID / Funktion         | Öffnet sich wenn…                     |
|----------------------|-----------------------|---------------------------------------|
| **Setup Modal**      | `#setupModal`         | Erstaufruf / kein User gesetzt        |
| **Force Reload Modal** | `#forceReloadModal` | User klickt Reload-Button             |
| **Sanity Modal**     | `#sanityModal`        | Datenvalidierungsfehler               |
| **Porra Card Modal** | `#porra-card-modal`   | `showMyPorraCard()` aufgerufen        |

---

## TAB 1 — 📋 Zusammenfassung (`#tab-overview`)

```
┌─────────────────────────────────────────────────────────┐
│  KPI GRID                           #kpiGrid            │
│  ┌──────┐ ┌──────┐ ┌──────┐ ┌──────┐ ┌──────┐ ...     │
│  │ Rang │ │ Pts  │ │ Form │ │Momt. │ │Rückst│         │
│  └──────┘ └──────┘ └──────┘ └──────┘ └──────┘         │
│  [Toggle: Mehr/Weniger KPIs]                            │
│─────────────────────────────────────────────────────────│
│  ┌──────────────────────┐  ┌──────────────────────────┐ │
│  │  LAST RESULT CARD    │  │  NEXT MATCH CARD         │ │
│  │  #lastMatchCard      │  │  #nextMatchCard          │ │
│  │  → FT Match Card(s)  │  │  → Live/Upcoming Card(s) │ │
│  └──────────────────────┘  └──────────────────────────┘ │
│─────────────────────────────────────────────────────────│
│  LIVE GAMES SUMMARY BLOCK           #liveGamesSummaryBlock │
│  (nur sichtbar wenn ≥1 Spiel LIVE)                      │
│  ┌──────────────────────────────────────────────────┐   │
│  │  🔴 Live — N Spiele  (animiert)                  │   │
│  │  → Tip Block (je Live-Spiel, nur Gruppe + User)  │   │
│  └──────────────────────────────────────────────────┘   │
│─────────────────────────────────────────────────────────│
│  ▼ LATEST GAME SUMMARY (collapsible) #latestGamesBody   │
│  ▼ UPCOMING GAMES SUMMARY (collapsible) #upcomingGamesBody │
│─────────────────────────────────────────────────────────│
│  ┌──────────────────────┐  ┌──────────────────────────┐ │
│  │  GROUP SUMMARY CARD  │  │  KUDOS POOL CARD         │ │
│  │  #groupSummaryContent│  │  #kuDosSplit             │ │
│  └──────────────────────┘  └──────────────────────────┘ │
└─────────────────────────────────────────────────────────┘
```

| Kanonischer Name              | Funktion / ID                         | Beschreibung                              |
|-------------------------------|---------------------------------------|-------------------------------------------|
| **KPI Grid**                  | `renderKPIs()` / `#kpiGrid`           | Kennzahlen-Kacheln (Rang, Pts, Form…)     |
| **KPI Toggle**                | `#kpiCollapsWrap` / `#kpiToggleBtn`   | Mehr/Weniger KPIs ein-/ausblenden         |
| **Last Result Card**          | `#lastMatchCard` / `#lastMatchContent`| Letzter abgeschlossener Spieltag-Slot     |
| **Next Match Card**           | `#nextMatchCard` / `#nextMatchContent`| Nächster Kick-off oder laufende Spiele    |
| **Live Games Summary Block**  | `#liveGamesSummaryBlock`              | Erscheint nur wenn ≥1 Spiel LIVE          |
| **Latest Game Summary**       | `#latestGamesBody` (collapsible)      | Letzte abgeschlossene Spiele (aufklappbar)|
| **Upcoming Games Summary**    | `#upcomingGamesBody` (collapsible)    | Nächste Spiele (aufklappbar)              |
| **Group Summary Card**        | `#groupSummaryContent`                | Mini-Leaderboard der eigenen Gruppe       |
| **Kudos Pool Card**           | `#kuDosSplit`                         | Preisgeld-Verteilungs-Balken              |

---

## TAB 2 — 🏆 Rangliste (`#tab-leaderboard`)

| Kanonischer Name          | Funktion / ID                | Beschreibung                   |
|---------------------------|------------------------------|--------------------------------|
| **Leaderboard Table**     | `renderLeaderboard()` / `#lbTable` / `#lbBody` | Vollständige Rangliste aller 154 Spieler |
| **You-Legend**            | `#lbYouLegend` / `#lbYouTag` | Legende für eigene Zeile       |

---

## TAB 3 — 👥 Meine Gruppe (`#tab-group`)

| Kanonischer Name              | Funktion / ID                  | Beschreibung                      |
|-------------------------------|--------------------------------|-----------------------------------|
| **Group Tab Leaderboard**     | `renderGroupTab()` / `#groupTabContent` | Gruppen-interne Rangliste  |
| **Latest Game in Group**      | `renderGroupLatestGame()` / `#groupLatestGame` | Letztes Spiel mit Gruppen-Tipps |

---

## TAB 4 — ⚔️ Vergleich / H2H (`#tab-h2h`)

| Kanonischer Name          | Funktion / ID               | Beschreibung                        |
|---------------------------|-----------------------------|-------------------------------------|
| **H2H Player Selectors**  | `#h2hSelectorRows` / `#h2hAddBtn` | Spieler-Auswahl-Zeilen        |
| **H2H Summary Table**     | `#h2hSummary`               | Punkte-Vergleich je Kategorie       |
| **H2H Games Table**       | `#h2hGamesWrap`             | Spiel-für-Spiel Vergleich           |

---

## TAB 5 — ⚽ Spiele (`#tab-games`)

| Kanonischer Name      | Funktion / ID                   | Beschreibung                         |
|-----------------------|---------------------------------|--------------------------------------|
| **Games Grid**        | `renderGames()` / `#gamesGrid`  | Spiel-Kacheln mit Tipp-Badge         |
| **Game Detail Panel** | `showGameDetail()` / `#gameDetailPanel` | Aufklappbares Detail aller Tipps |

---

## TAB 6 — ⭐ Campeones (`#tab-champions`)

| Kanonischer Name      | Funktion / ID                  | Beschreibung                          |
|-----------------------|--------------------------------|---------------------------------------|
| **Champion Grid**     | `renderChampions()` / `#champGrid` | Länder-Kacheln mit Tipper-Anzahl  |
| **Scorer Grid**       | `#scorerGrid`                  | Torschützen-Cards mit ESPN-Tore       |

---

## TAB 7 — 📊 Statistiken (`#tab-stats`)

| Kanonischer Name          | ID                    | Beschreibung                                    |
|---------------------------|-----------------------|-------------------------------------------------|
| **Overall Accuracy Card** | `#accBars`            | Exact/Diff/Trend/Wrong-Verteilung aller Spieler |
| **Your Accuracy Card**    | `#yourAccBars`        | Eigene Trefferquote                             |
| **Upset Card**            | `#upsetGrid`          | Spieler die gegen Mehrheit lagen und Recht hatten |
| **Contrarian Card**       | `#contrarianContent`  | Top 15 Konträr-Spieler                          |
| **Group Rank Card**       | `#groupRankChart`     | Ø Score je Porra-Gruppe (Balken)                |
| **Consensus Card**        | `#consensusContent`   | Spiele mit höchstem Community-Konsens           |
| **Split Card**            | `#splitContent`       | Umstrittenste Spiele (gleichmäßige Verteilung)  |

---

## TAB 8 — 🔍 Suche (`#tab-search`)

| Kanonischer Name      | Funktion / ID            | Beschreibung                       |
|-----------------------|--------------------------|------------------------------------|
| **Search Input**      | `#searchInput`           | Freitext-Eingabe Spielername       |
| **Player Detail Card**| `doSearch()` / `#searchResults` | Dynamische Detail-Card je Spieler |

---

## TAB 9 — 🗄️ Datenbasis (`#tab-database`)

| Kanonischer Name      | Funktion / ID            | Beschreibung                       |
|-----------------------|--------------------------|------------------------------------|
| **Filter Bar**        | `#dbSearch`, `#dbGroupFilter`, `#dbGameFilter` | Such- und Filter-Leiste |
| **Database Table**    | `renderDatabase()` / `#databaseContent` | Alle 154 Spieler × Tipps |

---

## TAB 10 — 📝 Changelog (`#tab-changelog`)

Statisches HTML. Keine Render-Funktion. Karten chronologisch (neueste oben), eine Karte (`.card`) je Version.

---

## 🃏 MATCH CARD TYPEN (Shared Components)

| Kanonischer Name        | Funktion                      | Eingesetzt in                                     |
|-------------------------|-------------------------------|---------------------------------------------------|
| **Live Match Card**     | `matchCardLive(g, a)`         | Next Match Card (wenn live), Live Games Summary   |
| **FT Match Card**       | `matchCardFinished(g, a, lb)` | Last Result Card                                  |
| **Upcoming Match Card** | `matchCardUpcoming(g)`        | Next Match Card (wenn upcoming)                   |
| **Tip Block**           | `renderGameTipBlock(...)`     | Live Games Summary, Latest/Upcoming Summary, Group, Games Detail |

### Live Match Card — Elemente
`matchCardLive(g, a)`: Disruptor Badge · Team Logos · Live Score · HZ-Score · Rote Karten · Live-Status · Scorer Events Grid (TV-Style, 2-spaltig) · **My/Community Tip Row** (blau) · Live Punkteverteilung (4 Boxen) · Match Meta

### FT Match Card — Elemente
`matchCardFinished(g, a, lb)`: Farbgradient (Punkte) · Points Badge · Teams/Score · FT-Pill · My Tip Display + Label (Exakt/Diff/Trend/Falsch) · FT Punkteverteilung · Match Meta

### Upcoming Match Card — Elemente
`matchCardUpcoming(g)`: Teams · Countdown Pill (`.cd-pill`, Live-Update) · **My/Community Tip Row** (blau) · Match Meta

### Tip Block — Elemente
`renderGameTipBlock(...)`: Score Label (FT/LIVE/–) · My/Community Tip Row · Player Tip Cards (`.player-tip-card`, sortiert nach Rang, farbig nach Punkte)
