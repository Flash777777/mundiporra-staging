# 🏆 Mundiporra 2026 — Backlog

> Letzte Aktualisierung: 21. Juni 2026
> Dashboard: https://flash777777.github.io/mundiporra-dashboard/
> Staging: https://flash777777.github.io/mundiporra-staging/

---

## 🔴 Bugs (offen)

| # | Bug | Diagnose | Fix-Ansatz | Prio |
|---|---|---|---|---|
| 1 | **KPI Momentum** Diskrepanz | Fenster-Definition im Code unklar | Fenstergröße prüfen + Tooltip ergänzen | 🟡 Mittel |

---

## 🟡 Features (geplant)

### ⚡ Upsetometer *(nur sichtbar für Don Patricio)*

Ein grafisches Widget (Live- und Simulator-Karte), das die „Überraschungsstärke" eines Spielergebnisses visualisiert.

**Konzept:**
- Horizontal-Balken 0–100 %
- Wert = gewichtetes Maß: % Spieler mit 0 Punkten + Abweichung vom meistgetippten Ergebnis
- Farb-Coding: Grün (< 30 %) → Gelb (30–60 %) → Orange (60–80 %) → Rot (> 80 %)
- Label: „Upset-Level: Niedrig / Mittel / Hoch / Extrem"
- **Sichtbarkeit:** Guard `USER.name === 'Don Patricio de la Porra'` — für alle anderen Spieler unsichtbar

**Beziehung zu Disruptor-Badge:**
- Upsetometer = kontinuierlich (Balken), Disruptor = diskret (Badge ab Schwellwert)
- Können parallel koexistieren

---

### ⚔️ H2H ohne Limit

Player-Cap entfernen. Dynamisch: Mobile 2–3, Desktop 2–10 Spieler gleichzeitig vergleichbar.

---

### 🌍 Ländernamen-Lokalisierung *(zurückgestellt — Risikoanalyse ausstehend)*

> ⚠️ Zurückgestellt. Ländernamen kommen aus mehreren Quellen (`ALL_GAMES`, ESPN API, `ALL_PREDICTIONS`) und werden an vielen Stellen gerendert (Spielkarten, Leaderboard, Simulator, Suche, Champions-Tab, H2H, Stats). Eine zentrale Country-Map wäre nötig — hohes Fehlerrisiko. Erst umsetzen wenn alle Rendering-Stellen vollständig kartiert sind.

---

### 💹 My Form vereinfachen

`commCalibration` vereinfachen (Näherung `commCalibration ≈ commHit`)

---

### 📊 Stats-Tab (10 Widgets)

Community-Tipp Badge, Populärster Tipp, POINTS ACHIEVED Chart, DAY WINNER, GROUPS EXPERTS, TOP SCORERS by GOALS, GOLDEN BOOT, CHAMPION CHANGE, UPS & DOWNS, GROUPS avg

---

### 🎛️ Konfigurierbares Rang-Umfeld

Slider/Dropdown im Setup-Modal für ±N Ränge

---

### 🔮 Potential Points *(Nacho-Wunsch)*

Für jeden Spieler: Maximale noch erzielbare Punkte berechnen → daraus den **bestmöglich noch erreichbaren Rang** ableiten.

**Logik:**
1. Für jeden Spieler: Maximalpunkte bei optimalen verbleibenden Ergebnissen berechnen
2. Für jeden anderen Spieler: Minimalpunkte (Worst-Case) annehmen
3. Best-Case-Rang = Rang des eigenen Maximums im Feld der Gegner-Worst-Cases

**Methoden:**
- **Method 1 — Greedy Pairwise (ab R32):** Für jede noch nicht gespielte Partie Exact = 3 Pkt + Scorer-Bonus annehmen
- **Method 2 — Exact Brute Force (ab QF):** Alle Ergebniskombinationen durchrechnen, globales Optimum ermitteln
- Browser ist schneller als Excel; Nacho wurde informiert

**Anzeige:**
- Pro Spieler: *„Bester möglicher Rang: #X (max. Y Punkte)"*
- Optional: Deltabadge zum aktuellen Rang (z.B. ↑12)

---

### 🤖 KO-Runden Workflow *(AI-assisted, Nacho)*

KI-gestützter Prozess zur Validierung und Konsolidierung der KO-Tipps aller 154 Spieler.

**Konzept:**
- Nacho erhält Excel-Abgaben der Teilnehmer → Terminal-Skript serialisiert zu Batches → Upload an AI Assistant
- AI prüft Vollständigkeit + Konformität gegen 154 Spieler → Fehler-Report → AI befüllt Master-Excel
- `submissions.json` im privaten GitHub-Repo als Persistenz-Layer
- System Prompt v5 erstellt (Error Catalogue: FMT, ID, SCR, TM, CHP, UNK)
- Master-Excel: `Mundiporra 2026_v0.2.xlsx` (Kike, VBA-basiert)
- KO-Deadline: 28. Juni 2026, strikte 10-Stunden-Frist

**Offen:**
- Match-ID-Nummerierung finalisieren
- Vollständige Teilnehmerliste als JSON
- Python-Extraktionsskript

---

### Weitere Features

- **Phase 2 KO-Runden Scoring:** Gruppenklassifikations-Punkte nur wenn Position bestätigt

---

## 🥚 Easter Eggs (geplant)

| Easter Egg | Auslöser | Effekt |
|---|---|---|
| 🃏 Don Patricio Modus | User wählt „Don Patricio de la Porra" im Setup | Goldener Rahmen + Konfetti-Animation |
| 🌧️ Matrix-Regen Finaltag | Datum 19. Juli 2026 | CSS Matrix-Regen-Hintergrund für 5s |
| 🔍 Geheimes Keyword | User tippt „porra" in Suche/Eingabe | Versteckte Nachricht / Animation |
| 🐕 Porra-Fakten | Inaktivität >2 Min oder spez. Button | Fun-Facts als Toast-Notification |

---

## 🚀 Long-Term / Phase 2

- 🌙 Dark Mode Toggle (CSS Custom Properties bereits mit `var(--bg)`, `var(--text)` vorbereitet)
- 📤 WhatsApp Schnellteilen (`navigator.share()` + Fallback)
- 🏅 Achievement/Badge System (Erste exakte Vorhersage, 3er-Serie, etc.)
- 📰 ESPN API Erweiterungen: News-Ticker, Assists/Cards/Shots/Saves Leaders, Game Report Snippet, Team Logos

---

## 🗓️ v2.0 — KO-Phase (nach Gruppenphase)

> **Trigger:** Nacho liefert neues Excel mit allen Gruppenphase-Ergebnissen + KO-Tipps aller 154 Spieler.
> Das Dashboard wird zu diesem Zeitpunkt als **v2.0** neu aufgesetzt.

| # | Feature / Fix | Details |
|---|---|---|
| 1 | **KO-Multiplikatoren** | `calcPoints()` um Runden-Multiplikator erweitern (AF ×2, VF ×3, HF ×4, P3 ×5, F ×6) — gilt für Spiel- UND Scorer-Punkte |
| 2 | **Champion Change Penalty** | Wer Champion geändert hat: nur +5 statt +10 bei Treffer — `champion_changed`-Feld + Bonus-Logik |
| 3 | **KO-Tipps aus neuem Excel** | Datenimport + Anpassung `ALL_PREDICTIONS`, `ALL_GAMES` für KO-Runden |
| 4 | **Gruppenklassifikations-Punkte** | Nur auszahlen wenn Gruppenposition offiziell bestätigt |

---

## ✅ Abgeschlossen

| Version | Feature / Fix |
|---|---|
| v1.19.15 | 🎉 Konfetti-Regen mit Nationalflaggen beim ESPN `LIVE`-Trigger (links Heim, rechts Gast); What's New Modal v1.20 |
| v1.19.15 | 🔧 „Team Luis Díaz" Mitglieder-Fix (7 Mitglieder korrekt eingepflegt) |
| v1.19.13 | 🔧 Porra-Karte Download: Font-Overlap Fix (`document.fonts.ready` vor `html-to-image`) |
| v1.19.12 | 🔧 Porra-Karte Download: Blank-Image Fix (Base64-Preload für Spielerfotos vor `html-to-image`) |
| v1.19.11 | 🔧 Porra-Karte Download: `html2canvas` → `html-to-image` (native Browser-Rendering, iOS Overlay) |
| v1.19.10 | 🔧 Porra-Karte TS2-Name abgeschnitten (CSS `flex-wrap`, zweizeiliges HTML-Template) |
| v1.19.8 | 🔧 Countdown-Timer bleibt sichtbar wenn erstes Spiel des Abends live geht |
| v1.19.7 | 🏷️ Porra-Karte Labels immer EN (DE/ES i18n), Champion/TS1/TS2 Fix, Download onclone |
| v1.19.6 | 🔧 Porra-Karte Stats-Fix (e.name, played/hitPct), Download USER.player |
| v1.19.5 | 🔧 Porra-Karte: alt="cc" Variable Fix |
| v1.19.4 | 🔧 Porra-Karte: Nationalität + Foto aus card_mapping.json (cc + img) |
| v1.19.3 | 🔧 Porra-Karte: Stats-Render Fix, i18n-Keys, USER.player als Alias |
| v1.19.2 | 🔧 Porra-Karte: async async SyntaxError Fix |
| v1.19.1 | 🔧 Porra-Karte: ALL_PARTICIPANTS-Lookup Fix, WN Modal entfernt |
| v1.19.0 | 🃏 **Panini-Karte „Meine Porra-Karte"** — Easter Egg, Vintage-Design, Admin Gallery |
| v1.18.8 | 🔵 Live-Tipp Badge (~Exakt/Tordiff/Tendenz) in `matchCardLive` |
| v1.18.7 | 🔵 Tipp-Zeile (🤍 Dein Tipp + 🫶 Community) in `matchCardLive` |
| v1.18.6 | ⭐ Champions-Tab: alle TS1/TS2-Tipper + `<details>` für Champion-Tipper |
| v1.18.5 | 🔧 Dein Tipp in FT-Spielkarten (Spiele-Tab + Overview) |
| v1.18.4 | 🔧 Force-Reload Modal (Loop-Fix, multilingual `version.json`) |
| v1.18.1–3 | 🔧 Simulator Rang-Fixes (scorerPts, simTotals), Champions-Tab Fix |
| v1.18.0 | ⚽ Kane-Elfmeter Fix (Penalty Scored), 7-Tage Lookback, scoringEvents-Merge |
| v1.17.17 | 🥊 Disruptor-Schwellen: Disruptor ≥ 70%, Chaos-Spiel ≥ 90% |
| v1.17.16 | 🔧 Simulator Rang-Header (Rang aktuell → simuliert, Punkte-Delta) |
| v1.17.15 | 🔧 Live-Card Reihenfolge: Scorer → Ballbesitz → Punkteverteilung → Venue |
| v1.17.14 | 🔧 `ptDistHtml` ReferenceError Fix in `matchCardLive` |
| v1.17.0–13 | 🔧 ESPN API Fixes, Scorer-Logik, `getESPNDateParams`, Live-Count Bugs |
| v1.16.x | 🥊 Disruptor-Badge (Implementierung), Punkteverteilung Styling, What's New Modal |
| v1.15.x | 🔧 Punkteverteilung Feature (Live + Simulator), Live-Karte nur eigene Gruppe |
| v1.14.5 | 🔧 Header-Versions-Badge Fix |
| v1.13.9 | 🔧 ESPN API Range-Key Fix (fehlender Bindestrich) |
| v1.13.8 | 🔧 Scorer-Doppelzählung Fix (kanonische Game-Keys) |
| v1.13.7 | 🔧 `Illegal return statement` Fix, `saveSetup` Fix |
| v1.13.6 | 🔧 ESPN Date Params Fix, Simulator `baseRankMap`, What's New Modal |
| ✅ | ✅ Bug: Live-Button ×2 — `_canonKeys` Set-Zählung (v1.17.x) |
| ✅ | ✅ Bug: KPI Pin-Icon — CSS `.kpi-pin-btn.pinned` (v1.17.x) |
| ✅ | ✅ Bug: KPI „Gespielt" — `TOTAL_GAMES = 72` (v1.17.x) |


---

## 🔧 Implementierungs-Details: Group Standings Tab (v1.21)

> **Stand: 21.06.2026** — Code-Analyse vollständig. Alle str_replace-Anker, I18N-Keys, JS-Code und Versions-Targets dokumentiert. Nächste Session beginnt direkt mit dem Push.

### Ziel-Versionen
| Variable | Aktuell | Ziel |
|---|---|---|
| BUILD_VERSION | v1.19.15 | v1.21.0 |
| BUILD_DATE | 20.06.2026 23:30 | aktuelles Datum + Uhrzeit einsetzen |
| WN_VERSION | v1.20 | v1.21 |
| HTML-Größe (Basis) | 1.419.617 Bytes | nach Insert: > 1.450.000 erwarten |

### ESPN Standings API
- URL: https://site.api.espn.com/apis/v2/sports/soccer/fifa.world/standings
- Timeout: 8000ms | Cache: 60s (_gruppenData + _gruppenFetchTime)
- Response: data.children[] — 12 Einträge (Gruppe A bis L)
  - .name "Group A" | .abbreviation "A"
  - .standings.entries[] sortiert nach Rang
    - .team.displayName → immer durch normalizeTeam() normalisieren
    - .stats[] mit {name, value}: wins, losses, ties, pointsFor (Tore), pointsAgainst (Gegentore), points, gamesPlayed
    - .note.color: "green" / "yellow" / "red"
    - .note.text: "Qualified" / "Playoff" / "Eliminated"

### str_replace Anker — 6 Änderungen

#### [1] Desktop Tab-Button (nach Spiele, vor Campeones)
OLD-Anker (eindeutig): class="tab-btn" data-tab="champions" onclick="switchTab('champions')">⭐ Campeones</button>
NEW (Gruppen-Button davor + champions-Button behalten):
<button class="tab-btn" data-tab="gruppen" onclick="switchTab('gruppen')">🗂️ Gruppen</button>
    <button class="tab-btn" data-tab="champions" onclick="switchTab('champions')">⭐ Campeones</button>

#### [2] Mobile Nav-Button (nach Spiele, vor Campeones)
OLD-Anker: onclick="switchTab('champions')" data-tab="champions"><span class="nav-icon">⭐</span><span class="nav-label">Campeones</span>
NEW:
onclick="switchTab('gruppen')" data-tab="gruppen"><span class="nav-icon">🗂️</span><span class="nav-label">Gruppen</span></button>
    <button class="mobile-nav-btn" onclick="switchTab('champions')" data-tab="champions"><span class="nav-icon">⭐</span><span class="nav-label">Campeones</span>

#### [3] Tab-Panel (vor Champions-Tab)
OLD-Anker (eindeutig): <!-- ══════════════ CHAMPIONS TAB ══════════════ -->
NEW: Gruppen-Panel davor einfügen (kompletter HTML-Block, dann Champions-Kommentar folgt)

#### [4] switchTab-Erweiterung
OLD: if (tabId === 'h2h') initH2HTab();
NEW: if (tabId === 'h2h') initH2HTab();
  if (tabId === 'gruppen') renderGruppen();

#### [5] WN_ITEMS
OLD-Anker: const WN_ITEMS = [
  // v1.20 items
  { key: 'wn_confetti',    icon: '🎉', highlight: true },
NEW: v1.21-Item + divider davor einfügen

#### [6] BUILD_VERSION + WN_VERSION
OLD: const BUILD_VERSION = 'v1.19.15';
const BUILD_DATE    = '20.06.2026 23:30';
OLD: const WN_VERSION = 'v1.20';

### I18N Keys — ANKER pro Sprache
- EN: vor wn_confetti:'🎉 <strong>Confetti Rain
- DE: vor wn_confetti:'🎉 <strong>Konfetti-Regen   (Pos ~1.375.583)
- ES: vor wn_confetti:'🎉 <strong>Lluvia de Confeti  (Pos ~1.378.313)

EN-Keys:
tab_gruppen:'🗂️ Gruppen', gruppen_title:'🗂️ Group Standings', gruppen_loading:'Loading standings…', gruppen_error:'Failed to load standings', gruppen_nodata:'No data available', gruppen_group:'Group', gruppen_team:'Team', gruppen_gp:'GP', gruppen_wins:'W', gruppen_draws:'D', gruppen_losses:'L', gruppen_goals:'GF:GA', gruppen_gd:'GD', gruppen_pts:'PTS', gruppen_my_champ:'Champion', gruppen_need:'needs max', gruppen_games_played:'played',
wn_gruppen:'🗂️ <strong>Group Standings</strong>: new tab with all 12 groups in real-time — qualification 🟢🟡🔴, live badge 🔴, group leader crown 👑, your Champion highlighted.',

DE-Keys:
tab_gruppen:'🗂️ Gruppen', gruppen_title:'🗂️ Gruppenphase', gruppen_loading:'Lade Tabellen…', gruppen_error:'Tabellen nicht verfügbar', gruppen_nodata:'Keine Daten', gruppen_group:'Gruppe', gruppen_team:'Team', gruppen_gp:'Sp', gruppen_wins:'S', gruppen_draws:'U', gruppen_losses:'N', gruppen_goals:'T:GT', gruppen_gd:'TD', gruppen_pts:'Pkt', gruppen_my_champ:'Champion', gruppen_need:'braucht max.', gruppen_games_played:'gespielt',
wn_gruppen:'🗂️ <strong>Gruppenphase</strong>: neuer Tab mit allen 12 Gruppen in Echtzeit — Quali-Ampel 🟢🟡🔴, Live-Badge 🔴, Tabellenführer-Krone 👑, Champion-Team hervorgehoben.',

ES-Keys:
tab_gruppen:'🗂️ Grupos', gruppen_title:'🗂️ Fase de Grupos', gruppen_loading:'Cargando tablas…', gruppen_error:'Tablas no disponibles', gruppen_nodata:'Sin datos', gruppen_group:'Grupo', gruppen_team:'Equipo', gruppen_gp:'PJ', gruppen_wins:'G', gruppen_draws:'E', gruppen_losses:'P', gruppen_goals:'GF:GC', gruppen_gd:'DG', gruppen_pts:'Pts', gruppen_my_champ:'Campeón', gruppen_need:'necesita max.', gruppen_games_played:'jugados',
wn_gruppen:'🗂️ <strong>Fase de Grupos</strong>: nueva pestaña con los 12 grupos en tiempo real — semáforo 🟢🟡🔴, badge LIVE 🔴, corona al líder 👑, Campeón destacado.',

### renderGruppen() — Einfügeort: vor letztem </script> (~Pos 1.417.098)

Variablen: let _gruppenData = null; let _gruppenFetchTime = 0;

Funktion renderGruppen():
1. getElementById('gruppenContent') + getElementById('gruppenJumpBar')
2. Loading-Spinner anzeigen
3. ESPN API fetch mit 60s Cache
4. data.children[] iterieren
5. Jump-Buttons aus .abbreviation rendern
6. Pro Gruppe: card-div mit id="grp-N"
7. Pro Entry: qualiDot (note.color), isLive (liveGames-Check via normalizeTeam), crown (ri===0), isMyChamp (normalizeTeam(champion)), needsHtml (remaining>0 && noteColor yellow/red)
8. Table: Spalten Quali | Team | GP | W | D | L | GF:GA | GD | PTS

Vollständiger Code — in einfachen Strings (keine Template-Literals), weil index.html selbst Template-Literals enthält.
String-Konkatenation verwenden: '<tr>' + ... + '</tr>' etc.
liveGames-Key-Format: team1-team2 (normalisiert), _rev-Einträge via !liveGames[k]._rev ausschließen.

### Changelog-Eintrag — vor v1.19.15-Karte einfügen
Karte-Titel: v1.21.0 — 21. Juni 2026 (Feature)
Inhalt: Group Standings Tab — neuer Tab mit allen 12 Gruppen (A–L) in Echtzeit via ESPN API: Punkte, W/U/N, Tore, TD, Quali-Ampel 🟢🟡🔴, Live-Badge 🔴, Tabellenführer-Krone 👑, Champion-Team hervorgehoben, Sprungbuttons.

### Code-Positionen in index.html
| Element | Position |
|---|---|
| function normalizeTeam( | ~1.257.178 |
| function renderGroupTab( | ~1.315.828 |
| let liveGames = {} | früh im Script |
| letztes </script> | ~1.417.098 |
| I18N en:{ | ~1.372.942 |
| I18N de:{ | ~1.375.583 |
| I18N es:{ | ~1.378.313 |
| Changelog v1.19.15 Karte | ~61.260 |
