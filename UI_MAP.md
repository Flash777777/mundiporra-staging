# ðºï¸ Mundiporra Dashboard â UI Map
> Kanonische Komponentennamen fÃ¼r Patrick â Claude Kommunikation
> Stand: v1.23.20 Â· Repo: `Flash777777/mundiporra-staging` + `mundiporra-dashboard`

**Konvention:** `Kanonischer Name` â `fn()` / `#id` / `.class`
Wenn Patrick "X" sagt â Claude adressiert exakt den Code hinter "X". Keine Interpretation.

---

## GLOBALE SHELL

```
âââââââââââââââââââââââââââââââââââââââââââââââââââââââââââ
â  STAGING BANNER          .staging-banner                â  â nur staging-URL sichtbar
âââââââââââââââââââââââââââââââââââââââââââââââââââââââââââ
â  HEADER                                                 â
â    App-Titel (statisch)  Version Badge  #headerVersionBadge â
âââââââââââââââââââââââââââââââââââââââââââââââââââââââââââ
â  TAB-NAV BAR                                            â
â  [ð Zusammenfassung] [ð Rangliste] [ð¥ Gruppe]        â
â  [âï¸ Vergleich] [â½ Spiele] [âï¸ Bracket] [ðï¸ Gruppen]   â
â  [â­ Campeones] [ð Statistiken] [ð Suche]             â
â  [ðï¸ Datenbasis] [ð Log]                               â
âââââââââââââââââââââââââââââââââââââââââââââââââââââââââââ
```

### Globale Modals (immer verfÃ¼gbar, tab-unabhÃ¤ngig)

| Kanonischer Name     | ID / Funktion         | Ãffnet sich wennâ¦                     |
|----------------------|-----------------------|---------------------------------------|
| **Setup Modal**      | `#setupModal`         | Erstaufruf / kein User gesetzt        |
| **Force Reload Modal** | `#forceReloadModal` | User klickt Reload-Button             |
| **Sanity Modal**     | `#sanityModal`        | Datenvalidierungsfehler               |
| **Porra Card Modal** | `#porra-card-modal`   | `showMyPorraCard()` aufgerufen        |

---

## TAB 1 â ð Zusammenfassung (`#tab-overview`)

```
âââââââââââââââââââââââââââââââââââââââââââââââââââââââââââ
â  KPI GRID                           #kpiGrid            â
â  ââââââââ ââââââââ ââââââââ ââââââââ ââââââââ ...     â
â  â Rang â â Pts  â â Form â âMomt. â âRÃ¼ckstâ         â
â  ââââââââ ââââââââ ââââââââ ââââââââ ââââââââ         â
â  [Toggle: Mehr/Weniger KPIs]                            â
âââââââââââââââââââââââââââââââââââââââââââââââââââââââââââ
â  ââââââââââââââââââââââââ  ââââââââââââââââââââââââââââ â
â  â  LAST RESULT CARD    â  â  NEXT MATCH CARD         â â
â  â  #lastMatchCard      â  â  #nextMatchCard          â â
â  â  â FT Match Card(s)  â  â  â Live/Upcoming Card(s) â â
â  ââââââââââââââââââââââââ  ââââââââââââââââââââââââââââ â
âââââââââââââââââââââââââââââââââââââââââââââââââââââââââââ
â  LIVE GAMES SUMMARY BLOCK           #liveGamesSummaryBlock â
â  (nur sichtbar wenn â¥1 Spiel LIVE)                      â
â  ââââââââââââââââââââââââââââââââââââââââââââââââââââ   â
â  â  ð´ Live â N Spiele  (animiert)                  â   â
â  â  â Tip Block (je Live-Spiel, nur Gruppe + User)  â   â
â  ââââââââââââââââââââââââââââââââââââââââââââââââââââ   â
âââââââââââââââââââââââââââââââââââââââââââââââââââââââââââ
â  â¼ LATEST GAME SUMMARY (collapsible) #latestGamesBody   â
â  â¼ UPCOMING GAMES SUMMARY (collapsible) #upcomingGamesBody â
âââââââââââââââââââââââââââââââââââââââââââââââââââââââââââ
â  ââââââââââââââââââââââââ  ââââââââââââââââââââââââââââ â
â  â  GROUP SUMMARY CARD  â  â  KUDOS POOL CARD         â â
â  â  #groupSummaryContentâ  â  #kuDosSplit             â â
â  ââââââââââââââââââââââââ  ââââââââââââââââââââââââââââ â
âââââââââââââââââââââââââââââââââââââââââââââââââââââââââââ
```

| Kanonischer Name              | Funktion / ID                         | Beschreibung                              |
|-------------------------------|---------------------------------------|-------------------------------------------|
| **KPI Grid**                  | `renderKPIs()` / `#kpiGrid`           | Kennzahlen-Kacheln (Rang, Pts, Formâ¦)     |
| **KPI Toggle**                | `#kpiCollapsWrap` / `#kpiToggleBtn`   | Mehr/Weniger KPIs ein-/ausblenden         |
| **Last Result Card**          | `#lastMatchCard` / `#lastMatchContent`| Letzter abgeschlossener Spieltag-Slot     |
| **Next Match Card**           | `#nextMatchCard` / `#nextMatchContent`| NÃ¤chster Kick-off oder laufende Spiele    |
| **Live Games Summary Block**  | `#liveGamesSummaryBlock`              | Erscheint nur wenn â¥1 Spiel LIVE          |
| **Latest Game Summary**       | `#latestGamesBody` (collapsible)      | Letzte abgeschlossene Spiele (aufklappbar)|
| **Upcoming Games Summary**    | `#upcomingGamesBody` (collapsible)    | NÃ¤chste Spiele (aufklappbar)              |
| **Group Summary Card**        | `#groupSummaryContent`                | Mini-Leaderboard der eigenen Gruppe       |
| **Kudos Pool Card**           | `#kuDosSplit`                         | Preisgeld-Verteilungs-Balken              |

---

## TAB 2 â ð Rangliste (`#tab-leaderboard`)

| Kanonischer Name          | Funktion / ID                | Beschreibung                   |
|---------------------------|------------------------------|--------------------------------|
| **Leaderboard Table**     | `renderLeaderboard()` / `#lbTable` / `#lbBody` | VollstÃ¤ndige Rangliste aller 154 Spieler |
| **You-Legend**            | `#lbYouLegend` / `#lbYouTag` | Legende fÃ¼r eigene Zeile       |

---

## TAB 3 â ð¥ Meine Gruppe (`#tab-group`)

| Kanonischer Name              | Funktion / ID                  | Beschreibung                      |
|-------------------------------|--------------------------------|-----------------------------------|
| **Group Tab Leaderboard**     | `renderGroupTab()` / `#groupTabContent` | Gruppen-interne Rangliste inkl. Klassifikationspunkte (ð) |
| **Latest Game in Group**      | `renderGroupLatestGame()` / `#groupLatestGame` | Letztes Spiel mit Gruppen-Tipps |

---

## TAB 4 â âï¸ Vergleich / H2H (`#tab-h2h`)

| Kanonischer Name          | Funktion / ID               | Beschreibung                        |
|---------------------------|-----------------------------|-------------------------------------|
| **H2H Player Selectors**  | `#h2hSelectorRows` / `#h2hAddBtn` | Spieler-Auswahl-Zeilen        |
| **H2H Summary Table**     | `#h2hSummary`               | Punkte-Vergleich je Kategorie       |
| **H2H Games Table**       | `#h2hGamesWrap`             | Spiel-fÃ¼r-Spiel Vergleich           |

---

## TAB 5 â â½ Spiele (`#tab-games`)

| Kanonischer Name      | Funktion / ID                   | Beschreibung                         |
|-----------------------|---------------------------------|--------------------------------------|
| **Games Grid**        | `renderGames()` / `#gamesGrid`  | Spiel-Kacheln mit Tipp-Badge         |
| **Game Detail Panel** | `showGameDetail()` / `#gameDetailPanel` | Aufklappbares Detail aller Tipps |

---

## TAB 6 â âï¸ KO-Bracket (`#tab-kobracket`) â NEU seit v1.23.0

```
âââââââââââââââââââââââââââââââââââââââââââââââââââââââââââ
â  KO BRACKET VIEW         #koBracketContent              â
â  Desktop: horizontales Bracket-Layout (zoom-fÃ¤hig)      â
â  Mobile:  vertikales Bracket-Layout                     â
âââââââââââââââââââââââââââââââââââââââââââââââââââââââââââ
â  Runden: Achtelfinale â Viertelfinale â Halbfinale      â
â           â Spiel um Platz 3 â Finale                   â
â  Jede Matchcard: Team A vs Team B, Ergebnis/Tipp        â
âââââââââââââââââââââââââââââââââââââââââââââââââââââââââââ
```

| Kanonischer Name          | Funktion / ID                   | Beschreibung                          |
|---------------------------|---------------------------------|---------------------------------------|
| **KO Bracket Container**  | `renderKOBracket()` / `#koBracketContent` | Gesamter Bracket-View         |
| **KO Match Card**         | `_buildKOMatchCard()`           | Einzelne Match-Card im Bracket        |
| **KO Desktop Layout**     | `_buildKODesktop()`             | Desktop-Bracket (horizontal, zoom)    |
| **KO Mobile Layout**      | `_buildKOMobile()`              | Mobile-Bracket (vertikal)             |
| **KO Zoom Controls**      | `_koZoomIn/Out/Reset()`         | Zoom-Buttons Desktop                  |

---

## TAB 7 â ðï¸ Gruppen (`#tab-gruppen`) â NEU seit v1.21.0

```
âââââââââââââââââââââââââââââââââââââââââââââââââââââââââââ
â  GROUP STANDINGS (ESPN)  #gruppenContent                â
â  Gruppe A â¦ Gruppe L                                    â
â  Je Gruppe: Tabelle mit Pos/Team/Sp/S/U/N/Tore/Punkte   â
â  Team-Name + ð <Klassifikationspunkte> des Users       â
â  Quali-Ampel (grÃ¼n/gelb/rot)                            â
âââââââââââââââââââââââââââââââââââââââââââââââââââââââââââ
```

| Kanonischer Name              | Funktion / ID                      | Beschreibung                               |
|-------------------------------|------------------------------------|--------------------------------------------|
| **Gruppen Container**         | `renderGruppen()` / `#gruppenContent` | Alle 12 Gruppen-Tabellen                |
| **Gruppen Render UI**         | `_renderGruppenUI()`               | Interne Render-Funktion fÃ¼r Standings-UI   |
| **Group Classification Pts**  | `calcTeamClassificationPoints()`   | Punkte pro Team fÃ¼r den User (ESPN-basiert)|
| **Group Class Standings Fetch** | `fetchGrupClassStandings()`      | ESPN-Standings in `_grupClassCache` laden  |

---

## TAB 8 â â­ Campeones (`#tab-champions`)

| Kanonischer Name      | Funktion / ID                  | Beschreibung                          |
|-----------------------|--------------------------------|---------------------------------------|
| **Champion Grid**     | `renderChampions()` / `#champGrid` | LÃ¤nder-Kacheln mit Tipper-Anzahl  |
| **Scorer Grid**       | `#scorerGrid`                  | TorschÃ¼tzen-Cards mit ESPN-Tore       |

---

## TAB 9 â ð Statistiken (`#tab-stats`)

| Kanonischer Name          | ID                    | Beschreibung                                    |
|---------------------------|-----------------------|-------------------------------------------------|
| **Overall Accuracy Card** | `#accBars`            | Exact/Diff/Trend/Wrong-Verteilung aller Spieler |
| **Your Accuracy Card**    | `#yourAccBars`        | Eigene Trefferquote                             |
| **Upset Card**            | `#upsetGrid`          | Spieler die gegen Mehrheit lagen und Recht hatten |
| **Contrarian Card**       | `#contrarianContent`  | Top 15 KontrÃ¤r-Spieler                          |
| **Group Rank Card**       | `#groupRankChart`     | Ã Score je Porra-Gruppe (Balken)                |
| **Consensus Card**        | `#consensusContent`   | Spiele mit hÃ¶chstem Community-Konsens           |
| **Split Card**            | `#splitContent`       | Umstrittenste Spiele (gleichmÃ¤Ãige Verteilung)  |

---

## TAB 10 â ð Suche (`#tab-search`)

| Kanonischer Name      | Funktion / ID            | Beschreibung                       |
|-----------------------|--------------------------|-------------------------------------|
| **Search Input**      | `#searchInput`           | Freitext-Eingabe Spielername        |
| **Player Detail Card**| `doSearch()` / `#searchResults` | Dynamische Detail-Card je Spieler |

---

## TAB 11 â ðï¸ Datenbasis (`#tab-database`)

| Kanonischer Name      | Funktion / ID            | Beschreibung                       |
|-----------------------|--------------------------|-------------------------------------|
| **Filter Bar**        | `#dbSearch`, `#dbGroupFilter`, `#dbGameFilter` | Such- und Filter-Leiste |
| **Database Table**    | `renderDatabase()` / `#databaseContent` | Alle 154 Spieler Ã Tipps |

---

## TAB 12 â ð Changelog (`#tab-changelog`)

Statisches HTML. Keine Render-Funktion. Karten chronologisch (neueste oben), eine Karte (`.card`) je Version.

---

## ð MATCH CARD TYPEN (Shared Components)

| Kanonischer Name        | Funktion                      | Eingesetzt in                                     |
|-------------------------|-------------------------------|---------------------------------------------------|
| **Live Match Card**     | `matchCardLive(g, a)`         | Next Match Card (wenn live), Live Games Summary   |
| **FT Match Card**       | `matchCardFinished(g, a, lb)` | Last Result Card                                  |
| **Upcoming Match Card** | `matchCardUpcoming(g)`        | Next Match Card (wenn upcoming)                   |
| **Tip Block**           | `renderGameTipBlock(...)`     | Live Games Summary, Latest/Upcoming Summary, Group, Games Detail |

### Live Match Card â Elemente
`matchCardLive(g, a)`: Disruptor Badge Â· Team Logos Â· Live Score Â· HZ-Score Â· Rote Karten Â· Live-Status Â· Scorer Events Grid (TV-Style, 2-spaltig) Â· **My/Community Tip Row** (blau) Â· Live Punkteverteilung (4 Boxen) Â· Match Meta

### FT Match Card â Elemente
`matchCardFinished(g, a, lb)`: Farbgradient (Punkte) Â· Points Badge Â· Teams/Score Â· FT-Pill Â· My Tip Display + Label (Exakt/Diff/Trend/Falsch) Â· FT Punkteverteilung Â· Match Meta

### Upcoming Match Card â Elemente
`matchCardUpcoming(g)`: Teams Â· Countdown Pill (`.cd-pill`, Live-Update) Â· **My/Community Tip Row** (blau) Â· Match Meta

### Tip Block â Elemente
`renderGameTipBlock(...)`: Score Label (FT/LIVE/â) Â· My/Community Tip Row Â· Player Tip Cards (`.player-tip-card`, sortiert nach Rang, farbig nach Punkte)