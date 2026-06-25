# ⚙️ Mundiporra Dashboard — Component Registry
> Technische Vollreferenz inkl. Render-Chain für Claude
> Stand: v1.23.13 · Repo: `Flash777777/mundiporra-staging` + `mundiporra-dashboard`
> ⚠️ PFLICHT: Diese Datei wird bei jedem Push zu `index.html` im selben Commit aktualisiert.

---

## 1. RENDER-CHAIN (Call Graph)

```
initDashboard()
└── populateSetupModal()
    └── [User submits Setup Modal]
        ├── fetchGrupClassStandings()   → befüllt _grupClassCache (await!)
        ├── buildLeaderboard()          → schreibt _lastLb (inkl. classificationPts)
        └── switchTab('overview')
            └── [alle Overview-Renders]

switchTab('overview')
├── renderKPIs(lb)
│   └── getActual(game)
├── renderLastNextMatch()
│   ├── groupByKickoff(games, windowMs)
│   ├── matchCardFinished(g, a, lb)
│   ├── matchCardLive(g, a)
│   └── matchCardUpcoming(g)
├── renderLiveGamesSummary(lb)
├── renderLatestGameSummary(lb)
├── renderUpcomingGamesSummary(lb)
├── renderGroupSummary(lb)
└── renderKudos(lb)

switchTab('leaderboard') → buildLeaderboard() → renderLeaderboard(lb)
switchTab('group')       → renderGroupTab(lb) → renderGroupLatestGame()
switchTab('h2h')         → initH2HTab() → renderH2H()
switchTab('games')       → filterGames() → renderGames()
switchTab('kobracket')   → renderKOBracket()
                            └── fetchKOLiveData()
                            └── _buildKODesktop() / _buildKOMobile()
                                └── _buildKOMatchCard()
switchTab('gruppen')     → renderGruppen()
                            └── fetchGrupClassStandings() → _grupClassCache
                            └── _renderGruppenUI()
                                └── calcTeamClassificationPoints(playerName, teamName)
switchTab('champions')   → renderChampions()
switchTab('stats')       → renderStats(lb)
switchTab('search')      → [oninput] doSearch() → showPlayerDetail()
switchTab('database')    → renderDatabase()
switchTab('changelog')   → [statisch, kein Render]
[Porra Card]             → showMyPorraCard() → buildLeaderboard()

refreshDashboard()
├── await fetchGrupClassStandings()   ← WICHTIG: muss awaited werden!
├── await fetchESPN(...)
└── buildLeaderboard() + Tab neu rendern
```

---

## 2. FUNKTIONS-REFERENZ (alphabetisch)

### `_buildKODesktop(rounds)`
- **Returns:** HTML-String (Desktop-Bracket, horizontal, zoom-fähig)
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
- **Params:** `gid` — Game-ID (Number oder String, beide akzeptiert)
- **Returns:** `{score, pct, label}` oder `null`
- **Reads:** `ALL_PREDICTIONS`

### `_koCcMap(teamName)`
- **Returns:** ISO Country Code (string) für Flagge
- **Aufgerufen von:** `_koTeamRow()`

### `_koTeamRow(team, score)`
- **Returns:** HTML-String (Team-Zeile im KO-Bracket)
- **Aufgerufen von:** `_buildKOMatchCard()`

### `_koZoomIn() / _koZoomOut() / _koZoomReset() / _koApplyZoom()`
- Desktop-Zoom für KO-Bracket

### `_renderGruppenUI()`
- Interne Render-Funktion für Gruppen-Tab
- **Reads:** `_grupClassCache`
- **Calls:** `calcTeamClassificationPoints()`
- **DOM schreibt:** `#gruppenContent`

### `buildLeaderboard()`
- **Returns:** Array; schreibt in `_lastLb`
- **Beinhaltet:** `classificationPts` → addiert zu `total`
- **⚠️ Voraussetzung:** `_grupClassCache` muss befüllt sein

### `calcDisruptorLevel(g, a)`
- **Returns:** `'upset'` | `'chaos'` | `null`

### `calcGroupClassificationPoints(playerName, groupLetter)`
- **Returns:** Number (0, 1, oder 3)
- **Logik:** 3 Pkt exakte Position, 1 Pkt richtiges Team / falsche Pos, 0 sonst
- **Reads:** `_grupClassCache`, `ALL_GROUP_PREDICTIONS`
- **⚠️ Voraussetzung:** `_grupClassCache` befüllt

### `calcPlayerScore(playerName)`
- **Returns:** `{pts, exact, diff, trend, bonus, classificationPts, total}`
- **Calls:** `calcGroupClassificationPoints()`

### `calcPointDist(gameId, s1, s2)`
- **Returns:** `{p3, p2, p1, p0, pct3, pct2, pct1, pct0}`

### `calcTeamClassificationPoints(playerName, teamName)`
- **Returns:** Number (0, 1, oder 3)
- **⚠️ Normalisierungs-Map** erforderlich: ESPN-Cache = UPPERCASE + Sondernamen
  - `'South Korea'` → `'KOREA REP.'`
  - `'Ivory Coast'` → `'CÔTE D\'IVOIRE'`
  - `'Cape Verde'` → `'CABO VERDE'`
  - alle anderen: `.toUpperCase()`
- **Reads:** `ALL_GROUP_PREDICTIONS`, `_grupClassCache`
- **Aufgerufen von:** `_renderGruppenUI()`

### `doSearch(q)`
- **DOM schreibt:** `#searchResults`

### `fetchGrupClassStandings()`
- **Returns:** Promise (async)
- **Writes:** `_grupClassCache`
- **⚠️ MUSS awaited werden** vor `buildLeaderboard()`

### `fetchKOLiveData()`
- **Returns:** Promise (async), ESPN KO-Spiele
- **Aufgerufen von:** `renderKOBracket()`

### `filterGames(f, btn)`
- **Calls:** `renderGames()`

### `fmtCountdown(isoStr)` / `fmtLiveStatus(a)`
- Hilfsfunktionen für Zeit-/Status-Formatierung

### `getActual(game)`
- **Returns:** `{status, s1, s2, ht1, ht2, clock, rc1, rc2, scoringEvents, …}` oder `null`
- **Reads:** `liveGames`

### `getDisruptorLabel(level)` / `getKickoffISO(game)` / `getMyGroups()` / `getSharedGroups(p)`
- Standard-Hilfsfunktionen

### `groupByKickoff(games, windowMs)`
- **Returns:** Array von Arrays

### `initDashboard()` / `initH2HTab()`
- Einstiegspunkte

### `matchCardFinished(g, a, lb)` — **FT Match Card**
- **Returns:** HTML-String (`.match-card`)
- **Calls:** `scoreGame()`, `calcPointDist()`, `getKickoffISO()`

### `matchCardLive(g, a)` — **Live Match Card**
- **Returns:** HTML-String (`.match-card`)
- **Calls:** `fmtLiveStatus`, `calcDisruptorLevel`, `teamLogo`, `calcPointDist`, `_crowdPick`, `scoreGameLive`

### `matchCardUpcoming(g)` — **Upcoming Match Card**
- **Returns:** HTML-String (`.match-card`)
- **Calls:** `getKickoffISO()`, `fmtCountdown()`, `_crowdPick()`

### `refreshDashboard()`
- **⚠️ MUSS `await fetchGrupClassStandings()`** vor `buildLeaderboard()`
- Sonst: `classificationPts = 0` in `total`

### `renderChampions()`
- **DOM schreibt:** `#champGrid`, `#scorerGrid`

### `renderDatabase()`
- **DOM schreibt:** `#databaseContent`

### `renderGameTipBlock(game, actual, contextPlayers, isLive, lb)` — **Tip Block**
- **Returns:** HTML-String
- **CSS je Card:** `.correct-exact` | `.correct-diff` | `.correct-1x2` | `.wrong`

### `renderGames()`
- **DOM schreibt:** `#gamesGrid`

### `renderGroupLatestGame(members, lb)`
- **DOM schreibt:** `#groupLatestGame`

### `renderGroupTab(lb)`
- **DOM schreibt:** `#groupTabContent`
- Zeigt Klassifikationspunkte (🏅-Spalte) aus `classificationPts`

### `renderGruppen()`
- **DOM schreibt:** `#gruppenContent`
- **Calls:** `fetchGrupClassStandings()`, `_renderGruppenUI()`
- Zeigt ESPN-Gruppenstandings + Team-Level 🏅 Punkte

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
| `ALL_GROUP_PREDICTIONS` | Object | Gruppenphase-Tipps `{name:{pos:{1A,2A,…}}}`        | initial (hardcoded)     |
| `ALL_PARTICIPANTS`    | Array  | Spieler-Metadaten (Name, Gruppe, Champion, TS1, TS2) | initial (hardcoded)     |
| `ALL_GAMES`           | Array  | Spielplan 72 Spiele                                  | initial (hardcoded)     |
| `GROUP_DATA`          | Object | Porra-Gruppen → Mitglieder                           | initial (hardcoded)     |
| `USER`                | Object | `{player, group, lang, tz}`                          | `setupModal` submit     |
| `_lastLb`             | Array  | Letztes Leaderboard-Ergebnis                         | `buildLeaderboard()`   |
| `liveGames`           | Object | ESPN Live/FT-Daten `{key: actual, keyRev: actual}`   | ESPN-Fetch-Pipeline     |
| `_grupClassCache`     | Object | ESPN-Gruppenstandings `{A:[{name,pos,…}],…}`         | `fetchGrupClassStandings()` |
| `HARDCODED_RESULTS`   | Object | Hardcodierte FT-Ergebnisse ST1/ST2                   | initial (hardcoded)     |
| `BUILD_VERSION`       | String | z.B. `'v1.23.8'`                                     | Manuell je Push         |
| `BUILD_DATE`          | String | z.B. `'25.06.2026 08:00'`                            | Manuell je Push         |
| `WN_VERSION`          | String | z.B. `'v1.23'`                                       | Manuell bei Features    |

---

## 5. CSS-KLASSEN REGISTER (Schlüssel-Klassen)

| Klasse                    | Kontext                 | Bedeutung                                    |
|---------------------------|-------------------------|----------------------------------------------|
| `.card` / `.card-title`   | global                  | Standard-Card / Überschrift                  |
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
| `.ko-bracket-wrap`        | KO-Bracket Tab          | Wrapper für Bracket-Ansicht                  |
| `.ko-match-card`          | KO-Bracket Tab          | Einzelne KO-Match-Card                       |

---

## 6. TAB-DISPATCH REFERENZ

| Tab-ID       | Label                 | `switchTab()` ruft auf          |
|--------------|-----------------------|----------------------------------|
| `overview`   | 📋 Zusammenfassung    | `renderOverview()`              |
| `leaderboard`| 🏆 Rangliste          | `buildLeaderboard()`            |
| `group`      | 👥 Meine Gruppe       | `renderGroupTab()`              |
| `h2h`        | ⚔️ Vergleich          | `initH2HTab()`                  |
| `games`      | ⚽ Spiele             | `filterGames()`                 |
| `kobracket`  | ⚔️ KO-Bracket         | `renderKOBracket()`             |
| `gruppen`    | 🏟️ Gruppen            | `renderGruppen()`               |
| `champions`  | ⭐ Campeones          | `renderChampions()`             |
| `stats`      | 📊 Statistiken        | `renderStats(_lastLb)`          |
| `search`     | 🔍 Suche              | passiv — `doSearch()` on input  |
| `database`   | 🗄️ Datenbasis         | `renderDatabase()`              |
| `changelog`  | 📝 Changelog          | statisch — kein Render           |

---

## 7. BEKANNTE OFFENE BUGS

| # | Bug | Prio | Fix-Ansatz |
|---|-----|------|------------|
| B1 | `calcTeamClassificationPoints`: ESPN UPPERCASE vs. Mixed-Case Tipper-Namen → immer 0 | 🔴 | Normalisierungs-Map + `.toUpperCase()` |
| B2 | `total` im Ranking falsch: `classificationPts` = 0 wegen Timing | 🔴 | `fetchGrupClassStandings()` awaiten vor `buildLeaderboard()` |
| B3 | Live-Button zeigt ×2 | 🟠 | `Set` mit kanonischem Key |
| B4 | KPI „Gespielt" zeigt falschen Wert | 🟢 | `TOTAL_GAMES = 72` hardcoden |