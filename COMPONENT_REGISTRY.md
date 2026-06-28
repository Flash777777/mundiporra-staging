# âï¸ Mundiporra Dashboard â Component Registry
> Technische Vollreferenz inkl. Render-Chain fÃ¼r Claude
> Stand: v1.23.20 Â· Repo: `Flash777777/mundiporra-staging` + `mundiporra-dashboard`
> â ï¸ PFLICHT: Diese Datei wird bei jedem Push zu `index.html` im selben Commit aktualisiert.

---

## 1. RENDER-CHAIN (Call Graph)

```
initDashboard()
âââ populateSetupModal()
    âââ [User submits Setup Modal]
        âââ fetchGrupClassStandings()   â befÃ¼llt _grupClassCache (await!)
        âââ buildLeaderboard()          â schreibt _lastLb (inkl. classificationPts)
        âââ switchTab('overview')
            âââ [alle Overview-Renders]

switchTab('overview')
âââ renderKPIs(lb)
â   âââ getActual(game)
âââ renderLastNextMatch()
â   âââ groupByKickoff(games, windowMs)
â   âââ matchCardFinished(g, a, lb)
â   âââ matchCardLive(g, a)
â   âââ matchCardUpcoming(g)
âââ renderLiveGamesSummary(lb)
âââ renderLatestGameSummary(lb)
âââ renderUpcomingGamesSummary(lb)
âââ renderGroupSummary(lb)
âââ renderKudos(lb)

switchTab('leaderboard') â buildLeaderboard() â renderLeaderboard(lb)
switchTab('group')       â renderGroupTab(lb) â renderGroupLatestGame()
switchTab('h2h')         â initH2HTab() â renderH2H()
switchTab('games')       â filterGames() â renderGames()
switchTab('kobracket')   â renderKOBracket()
                            âââ fetchKOLiveData()
                            âââ _buildKODesktop() / _buildKOMobile()
                                âââ _buildKOMatchCard()
switchTab('gruppen')     â renderGruppen()
                            âââ fetchGrupClassStandings() â _grupClassCache
                            âââ _renderGruppenUI()
                                âââ calcTeamClassificationPoints(playerName, teamName)
switchTab('champions')   â renderChampions()
switchTab('stats')       â renderStats(lb)
switchTab('search')      â [oninput] doSearch() â showPlayerDetail()
switchTab('database')    â renderDatabase()
switchTab('changelog')   â [statisch, kein Render]
[Porra Card]             â showMyPorraCard() â buildLeaderboard()

refreshDashboard()
âââ await fetchGrupClassStandings()   â WICHTIG: muss awaited werden!
âââ await fetchESPN(...)
âââ buildLeaderboard() + Tab neu rendern
```

---

## 2. FUNKTIONS-REFERENZ (alphabetisch)

### `_buildKODesktop(rounds)`
- **Returns:** HTML-String (Desktop-Bracket, horizontal, zoom-fÃ¤hig)
- **Calls:** `_buildKOMatchCard()`
- **Aufgerufen von:** `renderKOBracket()`

### `_buildKOMobile(rounds)`
- **Returns:** HTML-String (Mobile-Bracket, vertikal)
- **Calls:** `_buildKOMatchCard()`
- **Aufgerufen von:** `renderKOBracket()`

### `_buildKOMatchCard(match, roundKey)`
- **Returns:** HTML-String (einzelne KO-Match-Card)
- **Aufgerufen von:** `_buildKODesktop()`, `_buildKOMobile()`

### `_crowdPick(gid)`
- **Params:** `gid` â Game-ID (Number oder String, beide akzeptiert)
- **Returns:** `{score, pct, label}` oder `null`
- **Reads:** `ALL_PREDICTIONS`

### `_koCcMap(teamName)`
- **Returns:** ISO Country Code (string) fÃ¼r Flagge
- **Aufgerufen von:** `_koTeamRow()`

### `_koTeamRow(team, score)`
- **Returns:** HTML-String (Team-Zeile im KO-Bracket)
- **Aufgerufen von:** `_buildKOMatchCard()`

### `_koZoomIn() / _koZoomOut() / _koZoomReset() / _koApplyZoom()`
- Desktop-Zoom fÃ¼r KO-Bracket

### `_renderGruppenUI()`
- Interne Render-Funktion fÃ¼r Gruppen-Tab
- **Reads:** `_grupClassCache`
- **Calls:** `calcTeamClassificationPoints()`
- **DOM schreibt:** `#gruppenContent`

### `buildLeaderboard()`
- **Returns:** Array; schreibt in `_lastLb`
- **Beinhaltet:** `classificationPts` â addiert zu `total`
- **â ï¸ Voraussetzung:** `_grupClassCache` muss befÃ¼llt sein

### `calcDisruptorLevel(g, a)`
- **Returns:** `'upset'` | `'chaos'` | `null`

### `calcGroupClassificationPoints(playerName, groupLetter)`
- **Returns:** Number (0, 1, oder 3)
- **Logik:** 3 Pkt exakte Position, 1 Pkt richtiges Team / falsche Pos, 0 sonst
- **Reads:** `_grupClassCache`, `ALL_GROUP_PREDICTIONS`
- **â ï¸ Voraussetzung:** `_grupClassCache` befÃ¼llt

### `calcPlayerScore(playerName)`
- **Returns:** `{pts, exact, diff, trend, bonus, classificationPts, total}`
- **Calls:** `calcGroupClassificationPoints()`

### `calcPointDist(gameId, s1, s2)`
- **Returns:** `{p3, p2, p1, p0, pct3, pct2, pct1, pct0}`

### `calcTeamClassificationPoints(playerName, teamName)`
- **Returns:** Number (0, 1, oder 3)
- **â ï¸ Normalisierungs-Map** erforderlich: ESPN-Cache = UPPERCASE + Sondernamen
  - `'South Korea'` â `'KOREA REP.'`
  - `'Ivory Coast'` â `'CÃTE D\'IVOIRE'`
  - `'Cape Verde'` â `'CABO VERDE'`
  - alle anderen: `.toUpperCase()`
- **Reads:** `ALL_GROUP_PREDICTIONS`, `_grupClassCache`
- **Aufgerufen von:** `_renderGruppenUI()`

### `doSearch(q)`
- **DOM schreibt:** `#searchResults`

### `fetchGrupClassStandings()`
- **Returns:** Promise (async)
- **Writes:** `_grupClassCache`
- **â ï¸ MUSS awaited werden** vor `buildLeaderboard()`

### `fetchKOLiveData()`
- **Returns:** Promise (async), ESPN KO-Spiele
- **Aufgerufen von:** `renderKOBracket()`

### `filterGames(f, btn)`
- **Calls:** `renderGames()`

### `fmtCountdown(isoStr)` / `fmtLiveStatus(a)`
- Hilfsfunktionen fÃ¼r Zeit-/Status-Formatierung

### `getActual(game)`
- **Returns:** `{status, s1, s2, ht1, ht2, clock, rc1, rc2, scoringEvents, â¦}` oder `null`
- **Reads:** `liveGames`

### `getDisruptorLabel(level)` / `getKickoffISO(game)` / `getMyGroups()` / `getSharedGroups(p)`
- Standard-Hilfsfunktionen

### `groupByKickoff(games, windowMs)`
- **Returns:** Array von Arrays

### `initDashboard()` / `initH2HTab()`
- Einstiegspunkte

### `matchCardFinished(g, a, lb)` â **FT Match Card**
- **Returns:** HTML-String (`.match-card`)
- **Calls:** `scoreGame()`, `calcPointDist()`, `getKickoffISO()`

### `matchCardLive(g, a)` â **Live Match Card**
- **Returns:** HTML-String (`.match-card`)
- **Calls:** `fmtLiveStatus`, `calcDisruptorLevel`, `teamLogo`, `calcPointDist`, `_crowdPick`, `scoreGameLive`

### `matchCardUpcoming(g)` â **Upcoming Match Card**
- **Returns:** HTML-String (`.match-card`)
- **Calls:** `getKickoffISO()`, `fmtCountdown()`, `_crowdPick()`

### `refreshDashboard()`
- **â ï¸ MUSS `await fetchGrupClassStandings()`** vor `buildLeaderboard()`
- Sonst: `classificationPts = 0` in `total`

### `renderChampions()`
- **DOM schreibt:** `#champGrid`, `#scorerGrid`

### `renderDatabase()`
- **DOM schreibt:** `#databaseContent`

### `renderGameTipBlock(game, actual, contextPlayers, isLive, lb)` â **Tip Block**
- **Returns:** HTML-String
- **CSS je Card:** `.correct-exact` | `.correct-diff` | `.correct-1x2` | `.wrong`

### `renderGames()`
- **DOM schreibt:** `#gamesGrid`

### `renderGroupLatestGame(members, lb)`
- **DOM schreibt:** `#groupLatestGame`

### `renderGroupTab(lb)`
- **DOM schreibt:** `#groupTabContent`
- Zeigt Klassifikationspunkte (ð-Spalte) aus `classificationPts`

### `renderGruppen()`
- **DOM schreibt:** `#gruppenContent`
- **Calls:** `fetchGrupClassStandings()`, `_renderGruppenUI()`
- Zeigt ESPN-Gruppenstandings + Team-Level ð Punkte

### `renderH2H()`
- **DOM schreibt:** `#h2hSelectorRows`, `#h2hSummary`, `#h2hGamesWrap`

### `renderKOBracket()`
- **DOM schreibt:** `#koBracketContent`
- **Calls:** `fetchKOLiveData()`, `_buildKODesktop()`, `_buildKOMobile()`
- Features: Desktop-Zoom, Mobile-Ansicht, Tipping-Integration

### `renderKPIs(lb)`
- **DOM schreibt:** `#kpiGrid`

### `renderKudos(lb)` / `renderLastNextMatch()` / `renderLatestGameSummary(lb)` / `renderUpcomingGamesSummary(lb)`
- Standard Overview-Renders

### `renderLeaderboard(lb)`
- **DOM schreibt:** `#lbBody`

### `renderLiveGamesSummary(lb)`
- **DOM schreibt:** `#liveGamesSummaryBlock`, `#liveGamesSummaryContent`

### `renderStats(lb)`
- **DOM schreibt:** `#accBars`, `#yourAccBars`, `#upsetGrid`, `#contrarianContent`, `#groupRankChart`, `#consensusContent`, `#splitContent`

### `scoreGame(tip, actual)` / `scoreGameLive(tip, actual)`
- **Returns:** 0 | 1 | 2 | 3

### `showGameDetail(gameId)` / `showMyPorraCard()` / `showPlayerDetail(name)`
- Detail-Ansichten

### `teamLogo(name, size)`
- **Returns:** HTML-String (`<img>` oder Emoji-Fallback)

---

## 3. DOM-ID REGISTER (Kurzreferenz)

| ID                        | Tab          | Schreibt                     |
|---------------------------|--------------|------------------------------|
| `accBars`                 | stats        | `renderStats`               |
| `champGrid`               | champions    | `renderChampions`           |
| `consensusContent`        | stats        | `renderStats`               |
| `contrarianContent`       | stats        | `renderStats`               |
| `databaseContent`         | database     | `renderDatabase`            |
| `dbGameFilter`            | database     | static                       |
| `dbGroupFilter`           | database     | static                       |
| `dbSearch`                | database     | static                       |
| `gameDetailContent`       | games        | `showGameDetail`            |
| `gameDetailPanel`         | games        | `showGameDetail`            |
| `gameDetailTitle`         | games        | `showGameDetail`            |
| `gamesGrid`               | games        | `renderGames`               |
| `groupLatestGame`         | group        | `renderGroupLatestGame`     |
| `groupRankChart`          | stats        | `renderStats`               |
| `groupSummaryContent`     | overview     | `renderGroupSummary`        |
| `groupTabContent`         | group        | `renderGroupTab`            |
| `gruppenContent`          | gruppen      | `_renderGruppenUI`          |
| `h2hAddBtn`               | h2h          | `renderH2H`                 |
| `h2hGamesWrap`            | h2h          | `renderH2H`                 |
| `h2hSummary`              | h2h          | `renderH2H`                 |
| `headerVersionBadge`      | global       | static                       |
| `koBracketContent`        | kobracket    | `renderKOBracket`           |
| `kpiGrid`                 | overview     | `renderKPIs`                |
| `kuDosSplit`              | overview     | `renderKudos`               |
| `lastMatchContent`        | overview     | `renderLastNextMatch`       |
| `latestGameSummaryContent`| overview     | `renderLatestGameSummary`   |
| `lbBody`                  | leaderboard  | `renderLeaderboard`         |
| `liveGamesSummaryBlock`   | overview     | `renderLiveGamesSummary`    |
| `nextMatchContent`        | overview     | `renderLastNextMatch`       |
| `porra-card-modal`        | global       | `showMyPorraCard`           |
| `scorerGrid`              | champions    | `renderChampions`           |
| `searchInput`             | search       | static                       |
| `searchResults`           | search       | `doSearch`                  |
| `setupModal`              | global       | static                       |
| `splitContent`            | stats        | `renderStats`               |
| `upcomingGamesSummaryContent` | overview | `renderUpcomingGamesSummary` |
| `upsetGrid`               | stats        | `renderStats`               |
| `yourAccBars`             | stats        | `renderStats`               |

---

## 4. GLOBALE VARIABLEN

| Variable              | Typ    | Inhalt                                               | Schreibt wer            |
|-----------------------|--------|------------------------------------------------------|-------------------------|
| `ALL_PREDICTIONS`     | Object | Tipps aller 154 Spieler `{name:{gameId:{g1,g2}}}`   | initial (hardcoded)     |
| `ALL_GROUP_PREDICTIONS` | Object | Gruppenphase-Tipps `{name:{pos:{1A,2A,â¦}}}`        | initial (hardcoded)     |
| `ALL_PARTICIPANTS`    | Array  | Spieler-Metadaten (Name, Gruppe, Champion, TS1, TS2) | initial (hardcoded)     |
| `ALL_GAMES`           | Array  | Spielplan 72 Spiele                                  | initial (hardcoded)     |
| `GROUP_DATA`          | Object | Porra-Gruppen â Mitglieder                           | initial (hardcoded)     |
| `USER`                | Object | `{player, group, lang, tz}`                          | `setupModal` submit     |
| `_lastLb`             | Array  | Letztes Leaderboard-Ergebnis                         | `buildLeaderboard()`   |
| `liveGames`           | Object | ESPN Live/FT-Daten `{key: actual, keyRev: actual}`   | ESPN-Fetch-Pipeline     |
| `_grupClassCache`     | Object | ESPN-Gruppenstandings `{A:[{name,pos,â¦}],â¦}`         | `fetchGrupClassStandings()` |
| `HARDCODED_RESULTS`   | Object | Hardcodierte FT-Ergebnisse ST1/ST2                   | initial (hardcoded)     |
| `BUILD_VERSION`       | String | z.B. `'v1.23.8'`                                     | Manuell je Push         |
| `BUILD_DATE`          | String | z.B. `'25.06.2026 08:00'`                            | Manuell je Push         |
| `WN_VERSION`          | String | z.B. `'v1.23'`                                       | Manuell bei Features    |

---

## 5. CSS-KLASSEN REGISTER (SchlÃ¼ssel-Klassen)

| Klasse                    | Kontext                 | Bedeutung                                    |
|---------------------------|-------------------------|----------------------------------------------|
| `.card` / `.card-title`   | global                  | Standard-Card / Ãberschrift                  |
| `.match-card`             | matchCard-Funktionen    | Basis-Klasse aller Spiel-Karten              |
| `.kpi-card`               | KPI Grid                | Einzelne KPI-Kachel                          |
| `.you-row` / `.you-tag`   | Leaderboard, global     | Eigene Zeile / "Du"-Badge                    |
| `.player-tip-card`        | `renderGameTipBlock`    | Tipp-Karte je Kontext-Spieler                |
| `.correct-exact`          | `.player-tip-card`      | 3 Punkte (exakt)                             |
| `.correct-diff`           | `.player-tip-card`      | 2 Punkte (Tordifferenz)                      |
| `.correct-1x2`            | `.player-tip-card`      | 1 Punkt (Tendenz)                            |
| `.wrong`                  | `.player-tip-card`      | 0 Punkte                                     |
| `.disruptor-badge`        | Live Match Card         | upset / chaos Badge                          |
| `.live-badge`             | global                  | Rotes "LIVE"-Badge                           |
| `.cd-pill` / `.cd-val`    | Upcoming Match Card     | Countdown-Pill                               |
| `.pill.pill-green`        | FT Match Card           | "FT"-Status-Pill                             |
| `.staging-banner`         | global                  | Roter Staging-Hinweis (nur staging-URL)      |
| `.tab-btn.active`         | Tab-Nav                 | Aktiver Tab                                  |
| `.ko-bracket-wrap`        | KO-Bracket Tab          | Wrapper fÃ¼r Bracket-Ansicht                  |
| `.ko-match-card`          | KO-Bracket Tab          | Einzelne KO-Match-Card                       |

---

## 6. TAB-DISPATCH REFERENZ

| Tab-ID       | Label                 | `switchTab()` ruft auf          |
|--------------|-----------------------|----------------------------------|
| `overview`   | ð Zusammenfassung    | `renderOverview()`              |
| `leaderboard`| ð Rangliste          | `buildLeaderboard()`            |
| `group`      | ð¥ Meine Gruppe       | `renderGroupTab()`              |
| `h2h`        | âï¸ Vergleich          | `initH2HTab()`                  |
| `games`      | â½ Spiele             | `filterGames()`                 |
| `kobracket`  | âï¸ KO-Bracket         | `renderKOBracket()`             |
| `gruppen`    | ðï¸ Gruppen            | `renderGruppen()`               |
| `champions`  | â­ Campeones          | `renderChampions()`             |
| `stats`      | ð Statistiken        | `renderStats(_lastLb)`          |
| `search`     | ð Suche              | passiv â `doSearch()` on input  |
| `database`   | ðï¸ Datenbasis         | `renderDatabase()`              |
| `changelog`  | ð Changelog          | statisch â kein Render           |

---

## 7. BEKANNTE OFFENE BUGS

| # | Bug | Prio | Fix-Ansatz |
|---|-----|------|------------|
| B1 | `calcTeamClassificationPoints`: ESPN UPPERCASE vs. Mixed-Case Tipper-Namen â immer 0 | ð´ | Normalisierungs-Map + `.toUpperCase()` |
| B2 | `total` im Ranking falsch: `classificationPts` = 0 wegen Timing | ð´ | `fetchGrupClassStandings()` awaiten vor `buildLeaderboard()` |
| B3 | Live-Button zeigt Ã2 | ð  | `Set` mit kanonischem Key |
| B4 | KPI âGespielt" zeigt falschen Wert | ð¢ | `TOTAL_GAMES = 72` hardcoden |