# 📋 Mundiporra 2026 — Backlog

> Letzte Aktualisierung: 18. Juni 2026
> Dashboard: https://flash777777.github.io/mundiporra-dashboard/
> Staging: https://flash777777.github.io/mundiporra-staging/

---

## 🔴 Bugs (offen)

| # | Bug | Diagnose | Fix-Ansatz | Prio |
|---|---|---|---|---|
| 1 | **KPI Momentum** Diskrepanz | Fenster-Definition im Code unklar | Fenster-Größe prüfen + Tooltip ergänzen | 🟡 Mittel |

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

### ⏱️ Countdown-Timer — immer sichtbar *(Analyse ausstehend)*

> ⚠️ Countdown existiert bereits. Aktuelles Verhalten: wird ausgeblendet sobald ein Live-Spiel läuft. Gewünschtes Verhalten: **Countdown bleibt sichtbar parallel zum Live-Banner**. Vor der Umsetzung Code-Analyse der Sichtbarkeitslogik nötig.

---

### 🃏 Player Card + „Meine Porra-Karte" *(zusammengeführt)*

Ein kombiniertes Feature — **kein Doppelaufwand:**

| Aspekt | Details |
|---|---|
| **Für jeden Spieler** | Panini/FUT-Style Modal mit Stats (Rang, Punkte, Exakt-Rate, TS1/TS2, Champion) |
| **Für den eigenen Account** | Zusätzlich „Teilen"-Button → Export als Bild via Canvas API / `navigator.share()` |
| **Output** | In-App Modal + optionaler Download/WhatsApp-Share |

---

### Weitere Features

- **Phase 2 KO-Runden Scoring:** Gruppenklassifikations-Punkte nur wenn Position bestätigt
- **My Form:** `commCalibration` vereinfachen (Näherung `commCalibration ≈ commHit`)
- **Stats-Tab (10 Widgets):** Community-Tipp Badge, Populärster Tipp, POINTS ACHIEVED Chart, DAY WINNER, GROUPS EXPERTS, TOP SCORERS by GOALS, GOLDEN BOOT, CHAMPION CHANGE, UPS & DOWNS, GROUPS avg
- **Konfigurierbares Rang-Umfeld:** Slider/Dropdown im Setup-Modal für ±N Ränge

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

## 🏗️ v2.0 — KO-Phase (nach Gruppenphase)

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
| v1.18.8 | 🏅 Live-Tipp Badge (~Exakt/Tordiff/Tendenz) in `matchCardLive` |
| v1.18.7 | 💙 Tipp-Zeile (👤 Dein Tipp + 👥 Community) in `matchCardLive` |
| v1.18.6 | ⭐ Champions-Tab: alle TS1/TS2-Tipper + `<details>` für Champion-Tipper |
| v1.18.5 | 💙 Dein Tipp in FT-Spielkarten (Spiele-Tab + Overview) |
| v1.18.4 | 🔄 Force-Reload Modal (Loop-Fix, multilingual `version.json`) |
| v1.18.1–3 | 🔧 Simulator Rang-Fixes (scorerPts, simTotals), Champions-Tab Fix |
| v1.18.0 | ⚽ Kane-Elfmeter Fix (Penalty Scored), 7-Tage Lookback, scoringEvents-Merge |
| v1.17.17 | 🔥 Disruptor-Schwellen: Disruptor ≥ 70%, Chaos-Spiel ≥ 90% |
| v1.17.16 | 📊 Simulator Rang-Header (Rang aktuell → simuliert, Punkte-Delta) |
| v1.17.15 | 🔀 Live-Card Reihenfolge: Scorer → Ballbesitz → Punkteverteilung → Venue |
| v1.17.14 | 🔧 `ptDistHtml` ReferenceError Fix in `matchCardLive` |
| v1.17.0–13 | 🔧 ESPN API Fixes, Scorer-Logik, `getESPNDateParams`, Live-Count Bugs |
| v1.16.x | 🔥 Disruptor-Badge (Implementierung), Punkteverteilung Styling, What's New Modal |
| v1.15.x | 📊 Punkteverteilung Feature (Live + Simulator), Live-Karte nur eigene Gruppe |
| v1.14.5 | 🔧 Header-Versions-Badge Fix |
| v1.13.9 | 🔧 ESPN API Range-Key Fix (fehlender Bindestrich) |
| v1.13.8 | 🔧 Scorer-Doppelzählung Fix (kanonische Game-Keys) |
| v1.13.7 | 🔧 `Illegal return statement` Fix, `saveSetup` Fix |
| v1.13.6 | 🔧 ESPN Date Params Fix, Simulator `baseRankMap`, What's New Modal |
| — | ✅ Bug: Live-Button ×2 → `_canonKeys` Set-Zählung (v1.17.x) |
| — | ✅ Bug: KPI Pin-Icon → CSS `.kpi-pin-btn.pinned` (v1.17.x) |
| — | ✅ Bug: KPI „Gespielt" → `TOTAL_GAMES = 72` (v1.17.x) |
