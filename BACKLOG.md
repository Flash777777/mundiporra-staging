# ð Mundiporra 2026 â Backlog

> Letzte Aktualisierung: 18. Juni 2026
> Dashboard: https://flash777777.github.io/mundiporra-dashboard/
> Staging: https://flash777777.github.io/mundiporra-staging/

---

## ð´ Bugs (offen)

| # | Bug | Diagnose | Fix-Ansatz | Prio |
|---|---|---|---|---|
| 1 | **KPI Momentum** Diskrepanz | Fenster-Definition im Code unklar | Fenster-GrÃ¶Ãe prÃ¼fen + Tooltip ergÃ¤nzen | ð¡ Mittel |

---

## ð¡ Features (geplant)

### â¡ Upsetometer *(nur sichtbar fÃ¼r Don Patricio)*

Ein grafisches Widget (Live- und Simulator-Karte), das die âÃberraschungsstÃ¤rke" eines Spielergebnisses visualisiert.

**Konzept:**
- Horizontal-Balken 0â100 %
- Wert = gewichtetes MaÃ: % Spieler mit 0 Punkten + Abweichung vom meistgetippten Ergebnis
- Farb-Coding: GrÃ¼n (< 30 %) â Gelb (30â60 %) â Orange (60â80 %) â Rot (> 80 %)
- Label: âUpset-Level: Niedrig / Mittel / Hoch / Extrem"
- **Sichtbarkeit:** Guard `USER.name === 'Don Patricio de la Porra'` â fÃ¼r alle anderen Spieler unsichtbar

**Beziehung zu Disruptor-Badge:**
- Upsetometer = kontinuierlich (Balken), Disruptor = diskret (Badge ab Schwellwert)
- KÃ¶nnen parallel koexistieren

---

### âï¸ H2H ohne Limit

Player-Cap entfernen. Dynamisch: Mobile 2â3, Desktop 2â10 Spieler gleichzeitig vergleichbar.

---

### ð LÃ¤ndernamen-Lokalisierung *(zurÃ¼ckgestellt â Risikoanalyse ausstehend)*

> â ï¸ ZurÃ¼ckgestellt. LÃ¤ndernamen kommen aus mehreren Quellen (`ALL_GAMES`, ESPN API, `ALL_PREDICTIONS`) und werden an vielen Stellen gerendert (Spielkarten, Leaderboard, Simulator, Suche, Champions-Tab, H2H, Stats). Eine zentrale Country-Map wÃ¤re nÃ¶tig â hohes Fehlerrisiko. Erst umsetzen wenn alle Rendering-Stellen vollstÃ¤ndig kartiert sind.

---

### â±ï¸ Countdown-Timer â immer sichtbar *(Analyse ausstehend)*

> â ï¸ Countdown existiert bereits. Aktuelles Verhalten: wird ausgeblendet sobald ein Live-Spiel lÃ¤uft. GewÃ¼nschtes Verhalten: **Countdown bleibt sichtbar parallel zum Live-Banner**. Vor der Umsetzung Code-Analyse der Sichtbarkeitslogik nÃ¶tig.

---

### ð Player Card + âMeine Porra-Karte" *(zusammengefÃ¼hrt)*

Ein kombiniertes Feature â **kein Doppelaufwand:**

| Aspekt | Details |
|---|---|
| **FÃ¼r jeden Spieler** | Panini/FUT-Style Modal mit Stats (Rang, Punkte, Exakt-Rate, TS1/TS2, Champion) |
| **FÃ¼r den eigenen Account** | ZusÃ¤tzlich âTeilen"-Button â Export als Bild via Canvas API / `navigator.share()` |
| **Output** | In-App Modal + optionaler Download/WhatsApp-Share |

---

### Weitere Features

- **Phase 2 KO-Runden Scoring:** Gruppenklassifikations-Punkte nur wenn Position bestÃ¤tigt
- **My Form:** `commCalibration` vereinfachen (NÃ¤herung `commCalibration â commHit`)
- **Stats-Tab (10 Widgets):** Community-Tipp Badge, PopulÃ¤rster Tipp, POINTS ACHIEVED Chart, DAY WINNER, GROUPS EXPERTS, TOP SCORERS by GOALS, GOLDEN BOOT, CHAMPION CHANGE, UPS & DOWNS, GROUPS avg
- **Konfigurierbares Rang-Umfeld:** Slider/Dropdown im Setup-Modal fÃ¼r Â±N RÃ¤nge

---

## ð¥ Easter Eggs (geplant)

| Easter Egg | AuslÃ¶ser | Effekt |
|---|---|---|
| ð Don Patricio Modus | User wÃ¤hlt âDon Patricio de la Porra" im Setup | Goldener Rahmen + Konfetti-Animation |
| ð§ï¸ Matrix-Regen Finaltag | Datum 19. Juli 2026 | CSS Matrix-Regen-Hintergrund fÃ¼r 5s |
| ð Geheimes Keyword | User tippt âporra" in Suche/Eingabe | Versteckte Nachricht / Animation |
| ð Porra-Fakten | InaktivitÃ¤t >2 Min oder spez. Button | Fun-Facts als Toast-Notification |

---

## ð Long-Term / Phase 2

- ð Dark Mode Toggle (CSS Custom Properties bereits mit `var(--bg)`, `var(--text)` vorbereitet)
- ð¤ WhatsApp Schnellteilen (`navigator.share()` + Fallback)
- ð Achievement/Badge System (Erste exakte Vorhersage, 3er-Serie, etc.)
- ð° ESPN API Erweiterungen: News-Ticker, Assists/Cards/Shots/Saves Leaders, Game Report Snippet, Team Logos

---

## ðï¸ v2.0 â KO-Phase (nach Gruppenphase)

> **Trigger:** Nacho liefert neues Excel mit allen Gruppenphase-Ergebnissen + KO-Tipps aller 154 Spieler.
> Das Dashboard wird zu diesem Zeitpunkt als **v2.0** neu aufgesetzt.

| # | Feature / Fix | Details |
|---|---|---|
| 1 | **KO-Multiplikatoren** | `calcPoints()` um Runden-Multiplikator erweitern (AF Ã2, VF Ã3, HF Ã4, P3 Ã5, F Ã6) â gilt fÃ¼r Spiel- UND Scorer-Punkte |
| 2 | **Champion Change Penalty** | Wer Champion geÃ¤ndert hat: nur +5 statt +10 bei Treffer â `champion_changed`-Feld + Bonus-Logik |
| 3 | **KO-Tipps aus neuem Excel** | Datenimport + Anpassung `ALL_PREDICTIONS`, `ALL_GAMES` fÃ¼r KO-Runden |
| 4 | **Gruppenklassifikations-Punkte** | Nur auszahlen wenn Gruppenposition offiziell bestÃ¤tigt |

---

## â Abgeschlossen

| Version | Feature / Fix |
|---|---|
| v1.19.7 | 🏷️ Porra-Karte Labels immer EN (DE/ES i18n), Champion/TS1/TS2 Fix, Download onclone |
| v1.19.6 | 🃏 Porra-Karte Stats-Fix (e.name, played/hitPct), Download USER.player |
| v1.19.5 | 🃏 Porra-Karte: alt="cc" Variable Fix |
| v1.19.4 | 🃏 Porra-Karte: Nationalität + Foto aus card_mapping.json (cc + img) |
| v1.19.3 | 🃏 Porra-Karte: Stats-Render Fix, i18n-Keys, USER.player als Alias |
| v1.19.2 | 🃏 Porra-Karte: async async SyntaxError Fix |
| v1.19.1 | 🃏 Porra-Karte: ALL_PARTICIPANTS-Lookup Fix, WN Modal entfernt |
| v1.19.0 | 🃏 **Panini-Karte „Meine Porra-Karte"** — Easter Egg, Vintage-Design, Admin Gallery |
| v1.18.8 | ð Live-Tipp Badge (~Exakt/Tordiff/Tendenz) in `matchCardLive` |
| v1.18.7 | ð Tipp-Zeile (ð¤ Dein Tipp + ð¥ Community) in `matchCardLive` |
| v1.18.6 | â­ Champions-Tab: alle TS1/TS2-Tipper + `<details>` fÃ¼r Champion-Tipper |
| v1.18.5 | ð Dein Tipp in FT-Spielkarten (Spiele-Tab + Overview) |
| v1.18.4 | ð Force-Reload Modal (Loop-Fix, multilingual `version.json`) |
| v1.18.1â3 | ð§ Simulator Rang-Fixes (scorerPts, simTotals), Champions-Tab Fix |
| v1.18.0 | â½ Kane-Elfmeter Fix (Penalty Scored), 7-Tage Lookback, scoringEvents-Merge |
| v1.17.17 | ð¥ Disruptor-Schwellen: Disruptor â¥ 70%, Chaos-Spiel â¥ 90% |
| v1.17.16 | ð Simulator Rang-Header (Rang aktuell â simuliert, Punkte-Delta) |
| v1.17.15 | ð Live-Card Reihenfolge: Scorer â Ballbesitz â Punkteverteilung â Venue |
| v1.17.14 | ð§ `ptDistHtml` ReferenceError Fix in `matchCardLive` |
| v1.17.0â13 | ð§ ESPN API Fixes, Scorer-Logik, `getESPNDateParams`, Live-Count Bugs |
| v1.16.x | ð¥ Disruptor-Badge (Implementierung), Punkteverteilung Styling, What's New Modal |
| v1.15.x | ð Punkteverteilung Feature (Live + Simulator), Live-Karte nur eigene Gruppe |
| v1.14.5 | ð§ Header-Versions-Badge Fix |
| v1.13.9 | ð§ ESPN API Range-Key Fix (fehlender Bindestrich) |
| v1.13.8 | ð§ Scorer-DoppelzÃ¤hlung Fix (kanonische Game-Keys) |
| v1.13.7 | ð§ `Illegal return statement` Fix, `saveSetup` Fix |
| v1.13.6 | ð§ ESPN Date Params Fix, Simulator `baseRankMap`, What's New Modal |
| â | â Bug: Live-Button Ã2 â `_canonKeys` Set-ZÃ¤hlung (v1.17.x) |
| â | â Bug: KPI Pin-Icon â CSS `.kpi-pin-btn.pinned` (v1.17.x) |
| â | â Bug: KPI âGespielt" â `TOTAL_GAMES = 72` (v1.17.x) |
