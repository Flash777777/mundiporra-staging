# Ã°ÂÂÂ Mundiporra 2026 Ã¢ÂÂ Backlog

> Letzte Aktualisierung: 18. Juni 2026
> Dashboard: https://flash777777.github.io/mundiporra-dashboard/
> Staging: https://flash777777.github.io/mundiporra-staging/

---

## Ã°ÂÂÂ´ Bugs (offen)

| # | Bug | Diagnose | Fix-Ansatz | Prio |
|---|---|---|---|---|
| 2 | **Porra-Karte TS2-Name abgeschnitten** | Stats-Zeile zu schmal, langer Name überläuft | CSS: `overflow:hidden;text-overflow:ellipsis` auf Stats-Wert-Span, oder Schrift kleiner | 🟢 Low |
| 3 | **Porra-Karte Download** schlägt fehl | `html2canvas createPattern` Fehler trotz `onclone` — SVG-Grain in `::after` wird nicht korrekt ignoriert | Grain-`::after` per `onclone` auf `display:none` setzen; alternativ nativen Canvas-Download ohne html2canvas | 🟡 Mittel |
| 1 | **KPI Momentum** Diskrepanz | Fenster-Definition im Code unklar | Fenster-GrÃÂ¶ÃÂe prÃÂ¼fen + Tooltip ergÃÂ¤nzen | Ã°ÂÂÂ¡ Mittel |

---

## Ã°ÂÂÂ¡ Features (geplant)

### Ã¢ÂÂ¡ Upsetometer *(nur sichtbar fÃÂ¼r Don Patricio)*

Ein grafisches Widget (Live- und Simulator-Karte), das die Ã¢ÂÂÃÂberraschungsstÃÂ¤rke" eines Spielergebnisses visualisiert.

**Konzept:**
- Horizontal-Balken 0Ã¢ÂÂ100 %
- Wert = gewichtetes MaÃÂ: % Spieler mit 0 Punkten + Abweichung vom meistgetippten Ergebnis
- Farb-Coding: GrÃÂ¼n (< 30 %) Ã¢ÂÂ Gelb (30Ã¢ÂÂ60 %) Ã¢ÂÂ Orange (60Ã¢ÂÂ80 %) Ã¢ÂÂ Rot (> 80 %)
- Label: Ã¢ÂÂUpset-Level: Niedrig / Mittel / Hoch / Extrem"
- **Sichtbarkeit:** Guard `USER.name === 'Don Patricio de la Porra'` Ã¢ÂÂ fÃÂ¼r alle anderen Spieler unsichtbar

**Beziehung zu Disruptor-Badge:**
- Upsetometer = kontinuierlich (Balken), Disruptor = diskret (Badge ab Schwellwert)
- KÃÂ¶nnen parallel koexistieren

---

### Ã¢ÂÂÃ¯Â¸Â H2H ohne Limit

Player-Cap entfernen. Dynamisch: Mobile 2Ã¢ÂÂ3, Desktop 2Ã¢ÂÂ10 Spieler gleichzeitig vergleichbar.

---

### Ã°ÂÂÂ LÃÂ¤ndernamen-Lokalisierung *(zurÃÂ¼ckgestellt Ã¢ÂÂ Risikoanalyse ausstehend)*

> Ã¢ÂÂ Ã¯Â¸Â ZurÃÂ¼ckgestellt. LÃÂ¤ndernamen kommen aus mehreren Quellen (`ALL_GAMES`, ESPN API, `ALL_PREDICTIONS`) und werden an vielen Stellen gerendert (Spielkarten, Leaderboard, Simulator, Suche, Champions-Tab, H2H, Stats). Eine zentrale Country-Map wÃÂ¤re nÃÂ¶tig Ã¢ÂÂ hohes Fehlerrisiko. Erst umsetzen wenn alle Rendering-Stellen vollstÃÂ¤ndig kartiert sind.

---

### Ã¢ÂÂ±Ã¯Â¸Â Countdown-Timer Ã¢ÂÂ immer sichtbar *(Analyse ausstehend)*

> Ã¢ÂÂ Ã¯Â¸Â Countdown existiert bereits. Aktuelles Verhalten: wird ausgeblendet sobald ein Live-Spiel lÃÂ¤uft. GewÃÂ¼nschtes Verhalten: **Countdown bleibt sichtbar parallel zum Live-Banner**. Vor der Umsetzung Code-Analyse der Sichtbarkeitslogik nÃÂ¶tig.

---

### Ã°ÂÂÂ Player Card + Ã¢ÂÂMeine Porra-Karte" *(zusammengefÃÂ¼hrt)*

Ein kombiniertes Feature Ã¢ÂÂ **kein Doppelaufwand:**

| Aspekt | Details |
|---|---|
| **FÃÂ¼r jeden Spieler** | Panini/FUT-Style Modal mit Stats (Rang, Punkte, Exakt-Rate, TS1/TS2, Champion) |
| **FÃÂ¼r den eigenen Account** | ZusÃÂ¤tzlich Ã¢ÂÂTeilen"-Button Ã¢ÂÂ Export als Bild via Canvas API / `navigator.share()` |
| **Output** | In-App Modal + optionaler Download/WhatsApp-Share |

---

### Weitere Features

- **Phase 2 KO-Runden Scoring:** Gruppenklassifikations-Punkte nur wenn Position bestÃÂ¤tigt
- **My Form:** `commCalibration` vereinfachen (NÃÂ¤herung `commCalibration Ã¢ÂÂ commHit`)
- **Stats-Tab (10 Widgets):** Community-Tipp Badge, PopulÃÂ¤rster Tipp, POINTS ACHIEVED Chart, DAY WINNER, GROUPS EXPERTS, TOP SCORERS by GOALS, GOLDEN BOOT, CHAMPION CHANGE, UPS & DOWNS, GROUPS avg
- **Konfigurierbares Rang-Umfeld:** Slider/Dropdown im Setup-Modal fÃÂ¼r ÃÂ±N RÃÂ¤nge

---

## Ã°ÂÂ¥Â Easter Eggs (geplant)

| Easter Egg | AuslÃÂ¶ser | Effekt |
|---|---|---|
| Ã°ÂÂÂ Don Patricio Modus | User wÃÂ¤hlt Ã¢ÂÂDon Patricio de la Porra" im Setup | Goldener Rahmen + Konfetti-Animation |
| Ã°ÂÂÂ§Ã¯Â¸Â Matrix-Regen Finaltag | Datum 19. Juli 2026 | CSS Matrix-Regen-Hintergrund fÃÂ¼r 5s |
| Ã°ÂÂÂ Geheimes Keyword | User tippt Ã¢ÂÂporra" in Suche/Eingabe | Versteckte Nachricht / Animation |
| Ã°ÂÂÂ Porra-Fakten | InaktivitÃÂ¤t >2 Min oder spez. Button | Fun-Facts als Toast-Notification |

---

## Ã°ÂÂÂ Long-Term / Phase 2

- Ã°ÂÂÂ Dark Mode Toggle (CSS Custom Properties bereits mit `var(--bg)`, `var(--text)` vorbereitet)
- Ã°ÂÂÂ¤ WhatsApp Schnellteilen (`navigator.share()` + Fallback)
- Ã°ÂÂÂ Achievement/Badge System (Erste exakte Vorhersage, 3er-Serie, etc.)
- Ã°ÂÂÂ° ESPN API Erweiterungen: News-Ticker, Assists/Cards/Shots/Saves Leaders, Game Report Snippet, Team Logos

---

## Ã°ÂÂÂÃ¯Â¸Â v2.0 Ã¢ÂÂ KO-Phase (nach Gruppenphase)

> **Trigger:** Nacho liefert neues Excel mit allen Gruppenphase-Ergebnissen + KO-Tipps aller 154 Spieler.
> Das Dashboard wird zu diesem Zeitpunkt als **v2.0** neu aufgesetzt.

| # | Feature / Fix | Details |
|---|---|---|
| 1 | **KO-Multiplikatoren** | `calcPoints()` um Runden-Multiplikator erweitern (AF ÃÂ2, VF ÃÂ3, HF ÃÂ4, P3 ÃÂ5, F ÃÂ6) Ã¢ÂÂ gilt fÃÂ¼r Spiel- UND Scorer-Punkte |
| 2 | **Champion Change Penalty** | Wer Champion geÃÂ¤ndert hat: nur +5 statt +10 bei Treffer Ã¢ÂÂ `champion_changed`-Feld + Bonus-Logik |
| 3 | **KO-Tipps aus neuem Excel** | Datenimport + Anpassung `ALL_PREDICTIONS`, `ALL_GAMES` fÃÂ¼r KO-Runden |
| 4 | **Gruppenklassifikations-Punkte** | Nur auszahlen wenn Gruppenposition offiziell bestÃÂ¤tigt |

---

## Ã¢ÂÂ Abgeschlossen

| Version | Feature / Fix |
|---|---|
| v1.19.7 | ð·ï¸ Porra-Karte Labels immer EN (DE/ES i18n), Champion/TS1/TS2 Fix, Download onclone |
| v1.19.6 | ð Porra-Karte Stats-Fix (e.name, played/hitPct), Download USER.player |
| v1.19.5 | ð Porra-Karte: alt="cc" Variable Fix |
| v1.19.4 | ð Porra-Karte: NationalitÃ¤t + Foto aus card_mapping.json (cc + img) |
| v1.19.3 | ð Porra-Karte: Stats-Render Fix, i18n-Keys, USER.player als Alias |
| v1.19.2 | ð Porra-Karte: async async SyntaxError Fix |
| v1.19.1 | ð Porra-Karte: ALL_PARTICIPANTS-Lookup Fix, WN Modal entfernt |
| v1.19.0 | ð **Panini-Karte âMeine Porra-Karte"** â Easter Egg, Vintage-Design, Admin Gallery |
| v1.18.8 | Ã°ÂÂÂ Live-Tipp Badge (~Exakt/Tordiff/Tendenz) in `matchCardLive` |
| v1.18.7 | Ã°ÂÂÂ Tipp-Zeile (Ã°ÂÂÂ¤ Dein Tipp + Ã°ÂÂÂ¥ Community) in `matchCardLive` |
| v1.18.6 | Ã¢Â­Â Champions-Tab: alle TS1/TS2-Tipper + `<details>` fÃÂ¼r Champion-Tipper |
| v1.18.5 | Ã°ÂÂÂ Dein Tipp in FT-Spielkarten (Spiele-Tab + Overview) |
| v1.18.4 | Ã°ÂÂÂ Force-Reload Modal (Loop-Fix, multilingual `version.json`) |
| v1.18.1Ã¢ÂÂ3 | Ã°ÂÂÂ§ Simulator Rang-Fixes (scorerPts, simTotals), Champions-Tab Fix |
| v1.18.0 | Ã¢ÂÂ½ Kane-Elfmeter Fix (Penalty Scored), 7-Tage Lookback, scoringEvents-Merge |
| v1.17.17 | Ã°ÂÂÂ¥ Disruptor-Schwellen: Disruptor Ã¢ÂÂ¥ 70%, Chaos-Spiel Ã¢ÂÂ¥ 90% |
| v1.17.16 | Ã°ÂÂÂ Simulator Rang-Header (Rang aktuell Ã¢ÂÂ simuliert, Punkte-Delta) |
| v1.17.15 | Ã°ÂÂÂ Live-Card Reihenfolge: Scorer Ã¢ÂÂ Ballbesitz Ã¢ÂÂ Punkteverteilung Ã¢ÂÂ Venue |
| v1.17.14 | Ã°ÂÂÂ§ `ptDistHtml` ReferenceError Fix in `matchCardLive` |
| v1.17.0Ã¢ÂÂ13 | Ã°ÂÂÂ§ ESPN API Fixes, Scorer-Logik, `getESPNDateParams`, Live-Count Bugs |
| v1.16.x | Ã°ÂÂÂ¥ Disruptor-Badge (Implementierung), Punkteverteilung Styling, What's New Modal |
| v1.15.x | Ã°ÂÂÂ Punkteverteilung Feature (Live + Simulator), Live-Karte nur eigene Gruppe |
| v1.14.5 | Ã°ÂÂÂ§ Header-Versions-Badge Fix |
| v1.13.9 | Ã°ÂÂÂ§ ESPN API Range-Key Fix (fehlender Bindestrich) |
| v1.13.8 | Ã°ÂÂÂ§ Scorer-DoppelzÃÂ¤hlung Fix (kanonische Game-Keys) |
| v1.13.7 | Ã°ÂÂÂ§ `Illegal return statement` Fix, `saveSetup` Fix |
| v1.13.6 | Ã°ÂÂÂ§ ESPN Date Params Fix, Simulator `baseRankMap`, What's New Modal |
| Ã¢ÂÂ | Ã¢ÂÂ Bug: Live-Button ÃÂ2 Ã¢ÂÂ `_canonKeys` Set-ZÃÂ¤hlung (v1.17.x) |
| Ã¢ÂÂ | Ã¢ÂÂ Bug: KPI Pin-Icon Ã¢ÂÂ CSS `.kpi-pin-btn.pinned` (v1.17.x) |
| Ã¢ÂÂ | Ã¢ÂÂ Bug: KPI Ã¢ÂÂGespielt" Ã¢ÂÂ `TOTAL_GAMES = 72` (v1.17.x) |
