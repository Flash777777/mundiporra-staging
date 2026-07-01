# ÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¯ÃÂÃÂ¸ÃÂÃÂ Mundiporra Dashboard ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ Component Registry
> Technische Vollreferenz inkl. Render-Chain fÃÂÃÂÃÂÃÂ¼r Claude
> Stand: v2.0.69 · Repo: `Flash777777/mundiporra-staging` + `mundiporra-dashboard`
> ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ ÃÂÃÂ¯ÃÂÃÂ¸ÃÂÃÂ PFLICHT: Diese Datei wird bei jedem Push zu `index.html` im selben Commit aktualisiert.

---

## 1. RENDER-CHAIN (Call Graph)

```
initDashboard()
ÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂ populateSetupModal()
    ÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂ [User submits Setup Modal]
        ÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂ fetchGrupClassStandings()   ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ befÃÂÃÂÃÂÃÂ¼llt _grupClassCache (await!)
        ÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂ buildLeaderboard()          ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ schreibt _lastLb (inkl. classificationPts)
        ÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂ switchTab('overview')
            ÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂ [alle Overview-Renders]

switchTab('overview')
ÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂ renderKPIs(lb)
ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ   ÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂ getActual(game)
ÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂ renderLastNextMatch()
ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ   ÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂ groupByKickoff(games, windowMs)
ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ   ÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂ matchCardFinished(g, a, lb)
ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ   ÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂ matchCardLive(g, a)
ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ   ÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂ matchCardUpcoming(g)
ÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂ renderLiveGamesSummary(lb)
ÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂ renderLatestGameSummary(lb)
ÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂ renderUpcomingGamesSummary(lb)
ÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂ renderGroupSummary(lb)
ÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂ renderKudos(lb)

switchTab('leaderboard') ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ buildLeaderboard() ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ renderLeaderboard(lb)
switchTab('group')       ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ renderGroupTab(lb) ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ renderGroupLatestGame()
switchTab('h2h')         ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ initH2HTab() ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ renderH2H()
switchTab('games')       ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ filterGames() ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ renderGames()
switchTab('kobracket')   ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ renderKOBracket()
                            ÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂ fetchKOLiveData()
                            ÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂ _buildKODesktop() / _buildKOMobile()
                                ÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂ _buildKOMatchCard()
switchTab('gruppen')     ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ renderGruppen()
                            ÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂ fetchGrupClassStandings() ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ _grupClassCache
                            ÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂ _renderGruppenUI()
                                ÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂ calcTeamClassificationPoints(playerName, teamName)
switchTab('champions')   ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ renderChampions()
switchTab('stats')       ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ renderStats(lb)
switchTab('search')      ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ [oninput] doSearch() ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ showPlayerDetail()
switchTab('database')    ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ renderDatabase()
switchTab('changelog')   ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ [statisch, kein Render]
[Porra Card]             ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ showMyPorraCard() ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ buildLeaderboard()

refreshDashboard()
ÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂ await fetchGrupClassStandings()   ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ WICHTIG: muss awaited werden!
ÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂ await fetchESPN(...)
ÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¢ÃÂÃÂÃÂÃÂ buildLeaderboard() + Tab neu rendern
```

---

## 2. FUNKTIONS-REFERENZ (alphabetisch)

### `_buildKODesktop(rounds)`
- **Returns:** HTML-String (Desktop-Bracket, horizontal, zoom-fÃÂÃÂÃÂÃÂ¤hig)
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
- **Params:** `gid` ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ Game-ID (Number oder String, beide akzeptiert)
- **Returns:** `{score, pct, label}` oder `null`
- **Reads:** `ALL_PREDICTIONS`

### `_koCcMap(teamName)`
- **Returns:** ISO Country Code (string) fÃÂÃÂÃÂÃÂ¼r Flagge
- **Aufgerufen von:** `_koTeamRow()`

### `_koTeamRow(team, score)`
- **Returns:** HTML-String (Team-Zeile im KO-Bracket)
- **Aufgerufen von:** `_buildKOMatchCard()`

### `_koZoomIn() / _koZoomOut() / _koZoomReset() / _koApplyZoom()`
- Desktop-Zoom fÃÂÃÂÃÂÃÂ¼r KO-Bracket

### `_renderGruppenUI()`
- Interne Render-Funktion fÃÂÃÂÃÂÃÂ¼r Gruppen-Tab
- **Reads:** `_grupClassCache`
- **Calls:** `calcTeamClassificationPoints()`
- **DOM schreibt:** `#gruppenContent`

### `buildLeaderboard()`
- **Returns:** Array; schreibt in `_lastLb`
- **Beinhaltet:** `classificationPts` ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ addiert zu `total`
- **ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ ÃÂÃÂ¯ÃÂÃÂ¸ÃÂÃÂ Voraussetzung:** `_grupClassCache` muss befÃÂÃÂÃÂÃÂ¼llt sein

### `calcDisruptorLevel(g, a)`
- **Returns:** `'upset'` | `'chaos'` | `null`

### `calcGroupClassificationPoints(playerName, groupLetter)`
- **Returns:** Number (0, 1, oder 3)
- **Logik:** 3 Pkt exakte Position, 1 Pkt richtiges Team / falsche Pos, 0 sonst
- **Reads:** `_grupClassCache`, `ALL_GROUP_PREDICTIONS`
- **ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ ÃÂÃÂ¯ÃÂÃÂ¸ÃÂÃÂ Voraussetzung:** `_grupClassCache` befÃÂÃÂÃÂÃÂ¼llt

### `calcPlayerScore(playerName)`
- **Returns:** `{pts, exact, diff, trend, bonus, classificationPts, total}`
- **Calls:** `calcGroupClassificationPoints()`

### `calcPointDist(gameId, s1, s2)`
- **Returns:** `{p3, p2, p1, p0, pct3, pct2, pct1, pct0}`

### `calcTeamClassificationPoints(playerName, teamName)`
- **Returns:** Number (0, 1, oder 3)
- **ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ ÃÂÃÂ¯ÃÂÃÂ¸ÃÂÃÂ Normalisierungs-Map** erforderlich: ESPN-Cache = UPPERCASE + Sondernamen
  - `'South Korea'` ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ `'KOREA REP.'`
  - `'Ivory Coast'` ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ `'CÃÂÃÂÃÂÃÂTE D\'IVOIRE'`
  - `'Cape Verde'` ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ `'CABO VERDE'`
  - alle anderen: `.toUpperCase()`
- **Reads:** `ALL_GROUP_PREDICTIONS`, `_grupClassCache`
- **Aufgerufen von:** `_renderGruppenUI()`

### `doSearch(q)`
- **DOM schreibt:** `#searchResults`

### `fetchGrupClassStandings()`
- **Returns:** Promise (async)
- **Writes:** `_grupClassCache`
- **ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ ÃÂÃÂ¯ÃÂÃÂ¸ÃÂÃÂ MUSS awaited werden** vor `buildLeaderboard()`

### `fetchKOLiveData()`
- **Returns:** Promise (async), ESPN KO-Spiele
- **Aufgerufen von:** `renderKOBracket()`

### `filterGames(f, btn)`
- **Calls:** `renderGames()`

### `fmtCountdown(isoStr)` / `fmtLiveStatus(a)`
- Hilfsfunktionen fÃÂÃÂÃÂÃÂ¼r Zeit-/Status-Formatierung

### `getActual(game)`
- **Returns:** `{status, s1, s2, ht1, ht2, clock, rc1, rc2, scoringEvents, ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ¦}` oder `null`
- **Reads:** `liveGames`

### `getDisruptorLabel(level)` / `getKickoffISO(game)` / `getMyGroups()` / `getSharedGroups(p)`
- Standard-Hilfsfunktionen

### `groupByKickoff(games, windowMs)`
- **Returns:** Array von Arrays

### `initDashboard()` / `initH2HTab()`
- Einstiegspunkte

### `matchCardFinished(g, a, lb)` ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ **FT Match Card**
- **Returns:** HTML-String (`.match-card`)
- **Calls:** `scoreGame()`, `calcPointDist()`, `getKickoffISO()`

### `matchCardLive(g, a)` ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ **Live Match Card**
- **Returns:** HTML-String (`.match-card`)
- **Calls:** `fmtLiveStatus`, `calcDisruptorLevel`, `teamLogo`, `calcPointDist`, `_crowdPick`, `scoreGameLive`

### `matchCardUpcoming(g)` ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ **Upcoming Match Card**
- **Returns:** HTML-String (`.match-card`)
- **Calls:** `getKickoffISO()`, `fmtCountdown()`, `_crowdPick()`

### `refreshDashboard()`
- **ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ ÃÂÃÂ¯ÃÂÃÂ¸ÃÂÃÂ MUSS `await fetchGrupClassStandings()`** vor `buildLeaderboard()`
- Sonst: `classificationPts = 0` in `total`

### `renderChampions()`
- **DOM schreibt:** `#champGrid`, `#scorerGrid`

### `renderDatabase()`
- **DOM schreibt:** `#databaseContent`

### `renderGameTipBlock(game, actual, contextPlayers, isLive, lb)` ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ **Tip Block**
- **Returns:** HTML-String
- **CSS je Card:** `.correct-exact` | `.correct-diff` | `.correct-1x2` | `.wrong`

### `renderGames()`
- **DOM schreibt:** `#gamesGrid`

### `renderGroupLatestGame(members, lb)`
- **DOM schreibt:** `#groupLatestGame`

### `renderGroupTab(lb)`
- **DOM schreibt:** `#groupTabContent`
- Zeigt Klassifikationspunkte (ÃÂÃÂ°ÃÂÃÂÃÂÃÂÃÂÃÂ-Spalte) aus `classificationPts`

### `renderGruppen()`
- **DOM schreibt:** `#gruppenContent`
- **Calls:** `fetchGrupClassStandings()`, `_renderGruppenUI()`
- Zeigt ESPN-Gruppenstandings + Team-Level ÃÂÃÂ°ÃÂÃÂÃÂÃÂÃÂÃÂ Punkte

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
| `ALL_GROUP_PREDICTIONS` | Object | Gruppenphase-Tipps `{name:{pos:{1A,2A,ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ¦}}}`        | initial (hardcoded)     |
| `ALL_PARTICIPANTS`    | Array  | Spieler-Metadaten (Name, Gruppe, Champion, TS1, TS2) | initial (hardcoded)     |
| `ALL_GAMES`           | Array  | Spielplan 72 Spiele                                  | initial (hardcoded)     |
| `GROUP_DATA`          | Object | Porra-Gruppen ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ Mitglieder                           | initial (hardcoded)     |
| `USER`                | Object | `{player, group, lang, tz}`                          | `setupModal` submit     |
| `_lastLb`             | Array  | Letztes Leaderboard-Ergebnis                         | `buildLeaderboard()`   |
| `liveGames`           | Object | ESPN Live/FT-Daten `{key: actual, keyRev: actual}`   | ESPN-Fetch-Pipeline     |
| `_grupClassCache`     | Object | ESPN-Gruppenstandings `{A:[{name,pos,ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ¦}],ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ¦}`         | `fetchGrupClassStandings()` |
| `HARDCODED_RESULTS`   | Object | Hardcodierte FT-Ergebnisse ST1/ST2                   | initial (hardcoded)     |
| `BUILD_VERSION`       | String | z.B. `'v1.23.8'`                                     | Manuell je Push         |
| `BUILD_DATE`          | String | z.B. `'25.06.2026 08:00'`                            | Manuell je Push         |
| `WN_VERSION`          | String | z.B. `'v1.23'`                                       | Manuell bei Features    |

---

## 5. CSS-KLASSEN REGISTER (SchlÃÂÃÂÃÂÃÂ¼ssel-Klassen)

| Klasse                    | Kontext                 | Bedeutung                                    |
|---------------------------|-------------------------|----------------------------------------------|
| `.card` / `.card-title`   | global                  | Standard-Card / ÃÂÃÂÃÂÃÂberschrift                  |
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
| `.ko-bracket-wrap`        | KO-Bracket Tab          | Wrapper fÃÂÃÂÃÂÃÂ¼r Bracket-Ansicht                  |
| `.ko-match-card`          | KO-Bracket Tab          | Einzelne KO-Match-Card                       |

---

## 6. TAB-DISPATCH REFERENZ

| Tab-ID       | Label                 | `switchTab()` ruft auf          |
|--------------|-----------------------|----------------------------------|
| `overview`   | ÃÂÃÂ°ÃÂÃÂÃÂÃÂÃÂÃÂ Zusammenfassung    | `renderOverview()`              |
| `leaderboard`| ÃÂÃÂ°ÃÂÃÂÃÂÃÂÃÂÃÂ Rangliste          | `buildLeaderboard()`            |
| `group`      | ÃÂÃÂ°ÃÂÃÂÃÂÃÂÃÂÃÂ¥ Meine Gruppe       | `renderGroupTab()`              |
| `h2h`        | ÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¯ÃÂÃÂ¸ÃÂÃÂ Vergleich          | `initH2HTab()`                  |
| `games`      | ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ½ Spiele             | `filterGames()`                 |
| `kobracket`  | ÃÂÃÂ¢ÃÂÃÂÃÂÃÂÃÂÃÂ¯ÃÂÃÂ¸ÃÂÃÂ KO-Bracket         | `renderKOBracket()`             |
| `gruppen`    | ÃÂÃÂ°ÃÂÃÂÃÂÃÂÃÂÃÂÃÂÃÂ¯ÃÂÃÂ¸ÃÂÃÂ Gruppen            | `renderGruppen()`               |
| `champions`  | ÃÂÃÂ¢ÃÂÃÂ­ÃÂÃÂ Campeones          | `renderChampions()`             |
| `stats`      | ÃÂÃÂ°ÃÂÃÂÃÂÃÂÃÂÃÂ Statistiken        | `renderStats(_lastLb)`          |
| `search`     | ÃÂÃÂ°ÃÂÃÂÃÂÃÂÃÂÃÂ Suche              | passiv ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ `doSearch()` on input  |
| `database`   | ÃÂÃÂ°ÃÂÃÂÃÂÃÂÃÂÃÂÃÂÃÂ¯ÃÂÃÂ¸ÃÂÃÂ Datenbasis         | `renderDatabase()`              |
| `changelog`  | ÃÂÃÂ°ÃÂÃÂÃÂÃÂÃÂÃÂ Changelog          | statisch ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ kein Render           |

---

## 7. BEKANNTE OFFENE BUGS

| # | Bug | Prio | Fix-Ansatz |
|---|-----|------|------------|
| B1 | `calcTeamClassificationPoints`: ESPN UPPERCASE vs. Mixed-Case Tipper-Namen ÃÂÃÂ¢ÃÂÃÂÃÂÃÂ immer 0 | ÃÂÃÂ°ÃÂÃÂÃÂÃÂÃÂÃÂ´ | Normalisierungs-Map + `.toUpperCase()` |
| B2 | `total` im Ranking falsch: `classificationPts` = 0 wegen Timing | ÃÂÃÂ°ÃÂÃÂÃÂÃÂÃÂÃÂ´ | `fetchGrupClassStandings()` awaiten vor `buildLeaderboard()` |
| B3 | Live-Button zeigt ÃÂÃÂÃÂÃÂ2 | ÃÂÃÂ°ÃÂÃÂÃÂÃÂÃÂÃÂ  | `Set` mit kanonischem Key |
| B4 | KPI ÃÂÃÂ¢ÃÂÃÂÃÂÃÂGespielt" zeigt falschen Wert | ÃÂÃÂ°ÃÂÃÂÃÂÃÂÃÂÃÂ¢ | `TOTAL_GAMES = 72` hardcoden |