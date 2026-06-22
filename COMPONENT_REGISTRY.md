# ⚙️ Mundiporra Dashboard — Component Registry
> Technische Vollreferenz inkl. Render-Chain für Claude
> Stand: v1.21.3 · Repo: `Flash777777/mundiporra-staging` + `mundiporra-dashboard`
> ⚠️ PFLICHT: Diese Datei wird bei jedem Push zu `index.html` im selben Commit aktualisiert.

---

## 1. RENDER-CHAIN (Call Graph)

```
initDashboard()
└── populateSetupModal()
    └── [User submits Setup Modal]
        ├── buildLeaderboard()          → schreibt _lastLb
        └── switchTab('overview')
            └── [alle Overview-Renders]

switchTab('overview')
├── renderKPIs(lb)
│   └── getActual(game)
├── renderLastNextMatch()
│   ├── groupByKickoff(games, windowMs)
│   │   └── getKickoffISO(game)
│   ├── matchCardFinished(g, a, lb)
│   │   ├── scoreGame(tip, actual)
│   │   └── calcPointDist(gameId, s1, s2)
│   ├── matchCardLive(g, a)
│   │   ├── fmtLiveStatus(a)
│   │   ├── calcDisruptorLevel(g, a)
│   │   │   └── calcPointDist(gameId, s1, s2)
│   │   ├── getDisruptorLabel(level)
│   │   ├── teamLogo(name, size)
│   │   ├── redCardHtml(count)
│   │   ├── calcPointDist(gameId, s1, s2)
│   │   ├── _crowdPick(gid)
│   │   └── scoreGameLive(tip, actual)
│   └── matchCardUpcoming(g)
│       ├── fmtCountdown(isoStr)
│       └── _crowdPick(gid)
├── renderLiveGamesSummary(lb)
│   ├── getActual(game)
│   ├── getMyGroups()
│   └── renderGameTipBlock(game, actual, ctx, isLive, lb)
│       ├── getMyGroups()
│       ├── fmtLiveStatus(a)
│       ├── scoreGame(tip, actual)
│       ├── scoreGameLive(tip, actual)
│       ├── getSharedGroups(playerName)
│       │   └── getMyGroups()
│       ├── _crowdPick(gid)
│       └── calcPointDist(gameId, s1, s2)
├── renderLatestGameSummary(lb)
│   ├── getActual(game), groupByKickoff(), renderGameTipBlock()
├── renderUpcomingGamesSummary(lb)
│   ├── getActual(game), getKickoffISO(), groupByKickoff(), renderGameTipBlock()
├── renderGroupSummary(lb)
│   └── getMyGroups()
└── renderKudos(lb)

switchTab('leaderboard') → buildLeaderboard() → renderLeaderboard(lb) → getMyGroups()
switchTab('group')       → renderGroupTab(lb) → getMyGroups(), renderGroupLatestGame()
                            └── renderGroupLatestGame(members, lb)
                                └── getActual, getKickoffISO, groupByKickoff, renderGameTipBlock
switchTab('h2h')         → initH2HTab() → renderH2H() → getActual()
switchTab('games')       → filterGames() → renderGames()
                            └── getActual, getKickoffISO, fmtLiveStatus, _crowdPick, scoreGame
                            └── [click] showGameDetail() → getActual, renderGameTipBlock
switchTab('champions')   → renderChampions()
switchTab('stats')       → renderStats(lb) → getActual(), scoreGame()
switchTab('search')      → [oninput] doSearch() → showPlayerDetail() → getActual, scoreGame
switchTab('database')    → renderDatabase() → getActual()
switchTab('changelog')   → [statisch, kein Render]
[Porra Card]             → showMyPorraCard() → buildLeaderboard()
```

---

## 2. FUNKTIONS-REFERENZ (alphabetisch)

### `_crowdPick(gid)`
- **Params:** `gid` — Game-ID (Number oder String, beide akzeptiert)
- **Returns:** `{score, pct, label}` oder `null`
- **Reads:** `ALL_PREDICTIONS`
- **Aufgerufen von:** `matchCardLive`, `matchCardUpcoming`, `renderGames`, `renderGameTipBlock`

### `buildLeaderboard()`
- **Returns:** Array; schreibt in `_lastLb`
- **Reads:** `ALL_PARTICIPANTS`; **Writes:** `_lastLb`
- **Aufgerufen von:** `switchTab('leaderboard')`, `showMyPorraCard()`

### `calcDisruptorLevel(g, a)`
- **Returns:** `'upset'` | `'chaos'` | `null`
- **Calls:** `calcPointDist()`
- **Aufgerufen von:** `matchCardLive`

### `calcPointDist(gameId, s1, s2)`
- **Returns:** `{p3, p2, p1, p0, pct3, pct2, pct1, pct0}`
- **Reads:** `ALL_PREDICTIONS`
- **Aufgerufen von:** `matchCardLive`, `matchCardFinished`, `renderGameTipBlock`, `calcDisruptorLevel`

### `doSearch(q)`
- **DOM schreibt:** `#searchResults`
- **Calls:** `showPlayerDetail()`
- **Aufgerufen von:** Search-Tab `oninput`

### `filterGames(f, btn)`
- **Calls:** `renderGames()`
- **Aufgerufen von:** Games-Tab Filter-Buttons

### `fmtCountdown(isoStr)`
- **Returns:** String ("2h 34m") oder `null`
- **Aufgerufen von:** `matchCardUpcoming`

### `fmtLiveStatus(a)`
- **Returns:** HTML-String ("45'" / "HZ" / "90'+3'")
- **Aufgerufen von:** `matchCardLive`, `renderGames`, `renderGameTipBlock`

### `getActual(game)`
- **Returns:** `{status, s1, s2, ht1, ht2, clock, rc1, rc2, scoringEvents, …}` oder `null`
- **Reads:** `liveGames`
- **Aufgerufen von:** fast alle Render-Funktionen

### `getDisruptorLabel(level)`
- **Reads:** `USER` (für Sprache)
- **Aufgerufen von:** `matchCardLive`

### `getKickoffISO(game)`
- **Returns:** ISO-String oder `null`
- **Calls:** `getActual()`

### `getMyGroups()`
- **Returns:** Array von Gruppen-Namen des aktuellen Users
- **Reads:** `USER`

### `getSharedGroups(playerName)`
- **Returns:** gemeinsame Gruppen von User + playerName
- **Calls:** `getMyGroups()`

### `groupByKickoff(games, windowMs)`
- **Returns:** Array von Arrays (Spielgruppen je Kickoff-Slot)
- **Calls:** `getKickoffISO()`
- **Typisches windowMs:** 8h = 28800000

### `initDashboard()`
- **Calls:** `populateSetupModal()`

### `initH2HTab()`
- **Calls:** `renderH2H()`

### `matchCardFinished(g, a, lb)` — **FT Match Card**
- **Returns:** HTML-String (`.match-card`)
- **Reads:** `ALL_PREDICTIONS`, `USER`
- **Calls:** `scoreGame()`, `calcPointDist()`, `getKickoffISO()`
- **Elemente:** Card-Gradient, Points-Badge, FT-Pill, My Tip + Label, Punkteverteilung

### `matchCardLive(g, a)` — **Live Match Card**
- **Returns:** HTML-String (`.match-card`)
- **Reads:** `ALL_PREDICTIONS`, `USER`
- **Calls:** `fmtLiveStatus`, `calcDisruptorLevel`, `getDisruptorLabel`, `teamLogo`, `redCardHtml`, `calcPointDist`, `_crowdPick`, `scoreGameLive`, `getKickoffISO`
- **Elemente:** Disruptor Badge, Logos, Live Score, HZ-Score, Red Cards, Scorer Events Grid, My/Community Tip Row (blau), Punkteverteilung

### `matchCardUpcoming(g)` — **Upcoming Match Card**
- **Returns:** HTML-String (`.match-card`)
- **Reads:** `ALL_PREDICTIONS`, `USER`
- **Calls:** `getKickoffISO()`, `fmtCountdown()`, `_crowdPick()`
- **Elemente:** Teams, Countdown Pill (`.cd-pill`), My/Community Tip Row

### `renderChampions()`
- **Reads:** `ALL_PREDICTIONS`, `ALL_PARTICIPANTS`, `USER`
- **DOM schreibt:** `#champGrid`, `#scorerGrid`

### `renderDatabase()`
- **Reads:** `ALL_PREDICTIONS`, `ALL_PARTICIPANTS`, `ALL_GAMES`, `GROUP_DATA`, `USER`
- **DOM liest:** `#dbSearch`, `#dbGroupFilter`, `#dbGameFilter`, `#dbGameSelect`
- **DOM schreibt:** `#databaseContent`
- **Calls:** `getActual()`

### `renderGameTipBlock(game, actual, contextPlayers, isLive, lb)` — **Tip Block**
- **Returns:** HTML-String (kein `.match-card` — Spieler-Tipp-Liste)
- **Reads:** `ALL_PREDICTIONS`, `GROUP_DATA`, `USER`
- **Calls:** `getMyGroups`, `fmtLiveStatus`, `scoreGame`, `scoreGameLive`, `getSharedGroups`, `_crowdPick`, `calcPointDist`
- **CSS je Card:** `.correct-exact` | `.correct-diff` | `.correct-1x2` | `.wrong`
- **Aufgerufen von:** `renderLiveGamesSummary`, `renderLatestGameSummary`, `renderUpcomingGamesSummary`, `renderGroupLatestGame`, `showGameDetail`

### `renderGames()`
- **Reads:** `ALL_PREDICTIONS`, `ALL_GAMES`, `USER`
- **DOM schreibt:** `#gamesGrid`
- **Calls:** `getActual`, `getKickoffISO`, `fmtLiveStatus`, `_crowdPick`, `scoreGame`, `showGameDetail`

### `renderGroupLatestGame(members, lb)`
- **DOM schreibt:** `#groupLatestGame`
- **Calls:** `getActual`, `getKickoffISO`, `groupByKickoff`, `renderGameTipBlock`

### `renderGroupSummary(lb)`
- **DOM schreibt:** `#groupSummaryTitle`, `#groupSummaryContent`
- **Calls:** `getMyGroups()`

### `renderGroupTab(lb)`
- **Reads:** `GROUP_DATA`, `USER`
- **DOM schreibt:** `#groupTabContent`
- **Calls:** `getMyGroups()`, `renderGroupLatestGame()`

### `renderH2H()`
- **Reads:** `ALL_PREDICTIONS`, `ALL_GAMES`, `USER`, `_lastLb`
- **DOM schreibt:** `#h2hSelectorRows`, `#h2hAddBtn`, `#h2hPlayerCount`, `#h2hSummary`, `#h2hGamesWrap`
- **Calls:** `getActual()`

### `renderKPIs(lb)`
- **Reads:** `ALL_GAMES`, `USER`, `_lastLb`
- **DOM schreibt:** `#kpiGrid`, `#kpiCollapsWrap`, `#kpiToggleBtn`
- **Calls:** `getActual()`

### `renderKudos(lb)`
- **DOM schreibt:** `#kuDosSplit`

### `renderLastNextMatch()`
- **Reads:** `ALL_GAMES`, `_lastLb`
- **DOM schreibt:** `#lastMatchTitle`, `#lastMatchContent`, `#nextMatchTitle`, `#nextMatchContent`
- **Calls:** `getActual`, `getKickoffISO`, `groupByKickoff`, `matchCardFinished`, `matchCardLive`, `matchCardUpcoming`

### `renderLatestGameSummary(lb)`
- **Reads:** `ALL_GAMES`
- **DOM schreibt:** `#latestGameSummaryContent`, `#latestGameSummaryTitle`
- **Calls:** `getActual`, `groupByKickoff`, `renderGameTipBlock`

### `renderLeaderboard(lb)`
- **Reads:** `GROUP_DATA`, `USER`
- **DOM schreibt:** `#lbBody`
- **Calls:** `getMyGroups()`

### `renderLiveGamesSummary(lb)`
- **Reads:** `ALL_GAMES`, `GROUP_DATA`, `USER`, `liveGames`
- **DOM schreibt:** `#liveGamesSummaryBlock` (display), `#liveGamesSummaryContent`
- **Calls:** `getActual`, `getMyGroups`, `renderGameTipBlock`
- **Besonderheit:** Zeigt nur Gruppen-Mitglieder + USER

### `renderStats(lb)`
- **Reads:** `ALL_PREDICTIONS`, `ALL_GAMES`, `GROUP_DATA`, `USER`
- **DOM schreibt:** `#accBars`, `#yourAccTitle`, `#yourAccBars`, `#upsetGrid`, `#contrarianContent`, `#groupRankChart`, `#consensusContent`, `#splitContent`
- **Calls:** `getActual()`, `scoreGame()`

### `renderUpcomingGamesSummary(lb)`
- **Reads:** `ALL_GAMES`
- **DOM schreibt:** `#upcomingGamesSummaryContent`, `#upcomingGamesSummaryTitle`
- **Calls:** `getActual`, `getKickoffISO`, `groupByKickoff`, `renderGameTipBlock`

### `scoreGame(tip, actual)`
- **Returns:** `0` | `1` | `2` | `3`
- **Aufgerufen von:** `matchCardFinished`, `renderGames`, `renderGameTipBlock`, `renderStats`, `showPlayerDetail`

### `scoreGameLive(tip, actual)`
- **Returns:** `0` | `1` | `2` | `3` | `null`
- **Aufgerufen von:** `matchCardLive`, `renderGameTipBlock`

### `showGameDetail(gameId)`
- **Reads:** `ALL_PREDICTIONS`, `ALL_GAMES`, `_lastLb`
- **DOM schreibt:** `#gameDetailTitle`, `#gameDetailContent`, `#gameDetailPanel` (visible)
- **Calls:** `getActual()`, `renderGameTipBlock()`

### `showMyPorraCard()`
- **Reads:** `USER`, `_lastLb`
- **DOM schreibt:** `#porra-card-modal`, `#porra-card-modal-card`, `#porraCardNameEl`
- **Calls:** `buildLeaderboard()`

### `showPlayerDetail(name)`
- **Reads:** `ALL_PREDICTIONS`, `ALL_PARTICIPANTS`, `ALL_GAMES`
- **DOM schreibt:** `#searchResults`
- **Calls:** `getActual()`, `scoreGame()`

### `teamLogo(name, size)`
- **Returns:** HTML-String (`<img>` oder Emoji-Fallback)
- **Aufgerufen von:** `matchCardLive`

---

## 3. DOM-ID REGISTER (Kurzreferenz)

| ID                        | Tab          | Schreibt                    |
|---------------------------|--------------|-----------------------------|
| `accBars`                 | stats        | `renderStats`               |
| `champGrid`               | champions    | `renderChampions`           |
| `consensusContent`        | stats        | `renderStats`               |
| `contrarianContent`       | stats        | `renderStats`               |
| `databaseContent`         | database     | `renderDatabase`            |
| `dbGameFilter`            | database     | static (filter select)      |
| `dbGroupFilter`           | database     | static (filter select)      |
| `dbSearch`                | database     | static (input)              |
| `gameDetailContent`       | games        | `showGameDetail`            |
| `gameDetailPanel`         | games        | `showGameDetail`            |
| `gameDetailTitle`         | games        | `showGameDetail`            |
| `gamesGrid`               | games        | `renderGames`               |
| `groupLatestGame`         | group        | `renderGroupLatestGame`     |
| `groupRankChart`          | stats        | `renderStats`               |
| `groupSummaryContent`     | overview     | `renderGroupSummary`        |
| `groupSummaryTitle`       | overview     | `renderGroupSummary`        |
| `groupTabContent`         | group        | `renderGroupTab`            |
| `h2hAddBtn`               | h2h          | `renderH2H`                 |
| `h2hGamesWrap`            | h2h          | `renderH2H`                 |
| `h2hPlayerCount`          | h2h          | `renderH2H`                 |
| `h2hSelectorRows`         | h2h          | `renderH2H`                 |
| `h2hSummary`              | h2h          | `renderH2H`                 |
| `headerVersionBadge`      | global       | static                      |
| `kpiCollapsWrap`          | overview     | `renderKPIs`                |
| `kpiGrid`                 | overview     | `renderKPIs`                |
| `kpiToggleBtn`            | overview     | `renderKPIs`                |
| `kuDosSplit`              | overview     | `renderKudos`               |
| `lastMatchContent`        | overview     | `renderLastNextMatch`       |
| `lastMatchTitle`          | overview     | `renderLastNextMatch`       |
| `latestGameSummaryContent`| overview     | `renderLatestGameSummary`   |
| `latestGamesBody`         | overview     | collapse-toggle             |
| `lbBody`                  | leaderboard  | `renderLeaderboard`         |
| `liveGamesSummaryBlock`   | overview     | `renderLiveGamesSummary`    |
| `liveGamesSummaryContent` | overview     | `renderLiveGamesSummary`    |
| `nextMatchContent`        | overview     | `renderLastNextMatch`       |
| `nextMatchTitle`          | overview     | `renderLastNextMatch`       |
| `porra-card-modal`        | global       | `showMyPorraCard`           |
| `porra-card-modal-card`   | global       | `showMyPorraCard`           |
| `scorerGrid`              | champions    | `renderChampions`           |
| `searchInput`             | search       | static                      |
| `searchResults`           | search       | `doSearch`                  |
| `setupModal`              | global       | static                      |
| `splitContent`            | stats        | `renderStats`               |
| `upcomingGamesSummaryContent` | overview | `renderUpcomingGamesSummary` |
| `upcomingGamesBody`       | overview     | collapse-toggle             |
| `upsetGrid`               | stats        | `renderStats`               |
| `yourAccBars`             | stats        | `renderStats`               |

---

## 4. GLOBALE VARIABLEN

| Variable           | Typ    | Inhalt                                               | Schreibt wer          |
|--------------------|--------|------------------------------------------------------|-----------------------|
| `ALL_PREDICTIONS`  | Object | Tipps aller 154 Spieler `{name:{gameId:{g1,g2}}}`  | initial (hardcoded)   |
| `ALL_PARTICIPANTS` | Array  | Spieler-Metadaten (Name, Gruppe, Champion, TS1, TS2) | initial (hardcoded)   |
| `ALL_GAMES`        | Array  | Spielplan 72 Spiele `{id, team1, team2, group, …}`  | initial (hardcoded)   |
| `GROUP_DATA`       | Object | Porra-Gruppen → Mitglieder `{Gruppe:[Namen]}`       | initial (hardcoded)   |
| `USER`             | Object | `{player, group, lang, tz}` aktiver User             | `setupModal` submit  |
| `_lastLb`          | Array  | Letztes Leaderboard-Ergebnis                         | `buildLeaderboard()` |
| `liveGames`        | Object | ESPN Live/FT-Daten `{key: actual, keyRev: actual}`   | ESPN-Fetch-Pipeline   |
| `HARDCODED_RESULTS`| Object | Hardcodierte FT-Ergebnisse ST1/ST2                   | initial (hardcoded)   |
| `BUILD_VERSION`    | String | z.B. `'v1.19.15'`                                    | Manuell je Push       |
| `BUILD_DATE`       | String | z.B. `'20.06.2026 14:30'`                            | Manuell je Push       |
| `WN_VERSION`       | String | z.B. `'v1.19'` (Modal-Trigger)                       | Manuell bei Features  |

---

## 5. CSS-KLASSEN REGISTER (Schlüssel-Klassen)

| Klasse                    | Kontext                 | Bedeutung                                    |
|---------------------------|-------------------------|----------------------------------------------|
| `.card` / `.card-title` | global                  | Standard-Card / Überschrift                  |
| `.match-card`             | matchCard-Funktionen    | Basis-Klasse aller Spiel-Karten              |
| `.kpi-card`               | KPI Grid                | Einzelne KPI-Kachel                          |
| `.kpi-pin-btn.pinned`     | KPI Grid                | Fixierter Pin (`color: var(--accent)`)       |
| `.you-row` / `.you-tag`   | Leaderboard, global     | Eigene Zeile hervorgehoben / "Du"-Badge      |
| `.player-tip-card`        | `renderGameTipBlock`    | Tipp-Karte je Kontext-Spieler                |
| `.correct-exact`          | `.player-tip-card`      | 3 Punkte (exakt)                             |
| `.correct-diff`           | `.player-tip-card`      | 2 Punkte (Tordifferenz)                      |
| `.correct-1x2`            | `.player-tip-card`      | 1 Punkt (Tendenz)                            |
| `.wrong`                  | `.player-tip-card`      | 0 Punkte                                     |
| `.badge-exact/diff/trend/wrong` | Games-Tab        | Tipp-Bewertungs-Badges                       |
| `.disruptor-badge`        | Live Match Card         | upset / chaos Badge                          |
| `.disruptor-badge.blink`  | Live Match Card         | Blinkt ab Minute 75 (chaos)                  |
| `.live-badge`             | global                  | Rotes "LIVE"-Badge                           |
| `.match-status-live`      | Live Match Card         | Live-Status-Anzeige                          |
| `.rank-badge`             | `renderGameTipBlock`    | "#N" Rang-Badge                              |
| `.group-tag`              | `renderGameTipBlock`    | Gruppen-Kürzel-Tag                           |
| `.cd-pill` / `.cd-val`    | Upcoming Match Card     | Countdown-Pill (Live-Update via `data-kickoff`) |
| `.pill.pill-green`        | FT Match Card           | "FT"-Status-Pill                             |
| `.staging-banner`         | global                  | Roter Staging-Hinweis (nur staging-URL)      |
| `.tab-btn.active`         | Tab-Nav                 | Aktiver Tab                                  |

---

## 6. TAB-DISPATCH REFERENZ

| Tab-ID       | Label                 | `switchTab()` ruft auf          |
|--------------|-----------------------|----------------------------------|
| `overview`   | 📋 Zusammenfassung    | `renderOverview()`              |
| `leaderboard`| 🏆 Rangliste          | `buildLeaderboard()`            |
| `group`      | 👥 Meine Gruppe       | `renderGroupTab()`              |
| `h2h`        | ⚔️ Vergleich          | `initH2HTab()`                  |
| `games`      | ⚽ Spiele             | `filterGames()`                 |
| `champions`  | ⭐ Campeones          | `renderChampions()`             |
| `stats`      | 📊 Statistiken        | `renderStats(_lastLb)`          |
| `search`     | 🔍 Suche              | passiv — `doSearch()` on input  |
| `database`   | 🗄️ Datenbasis         | `renderDatabase()`              |
| `changelog`  | 📝 Changelog          | statisch — kein Render           |
