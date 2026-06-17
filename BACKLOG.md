# 📋 Mundiporra 2026 — Backlog

> Letzte Aktualisierung: 17. Juni 2026  
> Dashboard: https://flash777777.github.io/mundiporra-dashboard/  
> Staging: https://flash777777.github.io/mundiporra-staging/

---

## 🔴 Bugs (offen)

| # | Bug | Diagnose | Fix-Ansatz | Prio |
|---|---|---|---|---|
| 1 | **Live-Button zeigt ×2** | `liveGames` speichert `key` + `keyRev`, `liveCount` zählt beide | `Set` mit kanonischem Key (alphabetisch sortiert) oder `_rev: true` Flag | 🟠 High |
| 2 | **KPI Pin-Icon** nicht unterscheidbar | Kein CSS für `.kpi-pin-btn.pinned` | `.pinned { color: var(--accent); opacity: 1; }` + Icon-Wechsel | 🟢 Low |
| 3 | **KPI „Gespielt"** zeigt `11 ✓ / 60 →` statt `11 / 72` | Zählt `ALL_GAMES.length` statt Gesamtzahl | Hardcode `TOTAL_GAMES = 72` | 🟢 Low |
| 4 | **KPI Momentum** Diskrepanz: Claude −2 vs. Dashboard −19 | Fenster-Definition unterschiedlich | Fenster-Größe im Code prüfen + Tooltip | 🟡 Mittel |
| 5 | **KO-Multiplikatoren** fehlen | Excel-Regeln dokumentiert, nicht implementiert | `calcPoints()` mit Multiplikator je Runde erweitern | 🔴 Korrektheit |
| 6 | **Champion Change Penalty** fehlt | 5 statt 10 Punkte bei Champion-Wechsel | `champion_changed`-Feld + Bonus-Logik anpassen | 🔴 Korrektheit |

---

## 🟡 Features (geplant)

### 🔥 Disruptor-Potential Badge *(Medium Prio)*

**Idee:** Live-Match-Karten bekommen ein Badge, das auf starke Rangverschiebungen, wenige Punktegewinner oder Top-10-Disruption hinweist.

**Badge-Level:**

| Badge | Trigger | Bedingung |
|---|---|---|
| 🔥 **Disruptor** | Viele Spieler gehen leer aus | ≥ 65% der Spieler erhalten 0 Punkte |
| 💀 **Chaos-Spiel** | Extremes Durcheinander | ≥ 82% der Spieler erhalten 0 Punkte |
| ⬆️ **Upgrade** | Top-10 Disruption | ≥ 4 aktuelle Top-10-Spieler fallen aus den Top-10 → hebt "Disruptor" auf "Chaos-Spiel" |

**Sonderregel — 0:0-Gate:**
- Das Badge wird bei einem 0:0-Spielstand **nur ausgelöst wenn Spielminute ≥ 70**
- Verhindert False Positives zu Spielbeginn

**Implementierung (Schätzung: ~1 Push):**
```javascript
// Neue Hilfsfunktionen:
function calcTop10Disruption(game, s1, s2) { ... }
// Zählt wie viele der aktuellen Top-10 bei diesem Ergebnis aus den Top-10 fallen würden

function calcDisruptorLevel(game, actual) {
  const dist = calcPointDist(game.id, actual.s1, actual.s2);
  const pct0 = dist.pct0;
  const disruption = calcTop10Disruption(game, actual.s1, actual.s2);
  
  if (actual.s1 === 0 && actual.s2 === 0 && (actual.minute || 0) < 70) return null; // 0:0-Gate
  
  let level = null;
  if (pct0 >= 65) level = 'disruptor';
  if (pct0 >= 82) level = 'chaos';
  if (level === 'disruptor' && disruption >= 4) level = 'chaos'; // Top-10 Upgrade
  
  return level;
}
```

**Badge-HTML** (im `matchCardLive` Header):
- 🔥 Disruptor: oranges Badge mit Flammen-Icon
- 💀 Chaos-Spiel: rotes Badge mit Skull-Icon + leichter Pulsanimation

---

### ⚡ Upsetometer *(Low-Medium Prio)*

**Idee:** Ein grafisches Widget (Live- und Simulator-Karte), das die "Überraschungsstärke" eines Spielergebnisses visualisiert — wie sehr weicht das aktuelle/simulierte Ergebnis vom Community-Konsens ab?

**Konzept:**
- Horizontal-Balken von 0% bis 100%
- Wert = gewichtetes Maß aus: % Spieler mit 0 Punkten + Abweichung vom meistgetippten Ergebnis
- Farb-Coding: Grün (< 30%) → Gelb (30–60%) → Orange (60–80%) → Rot (> 80%)
- Label: "Upset-Level: Niedrig / Mittel / Hoch / Extrem"

**Beziehung zu Disruptor-Badge:**
- Upsetometer ist **kontinuierlich** (Balken), Disruptor ist **diskret** (Badge ab Schwellwert)
- Können parallel existieren oder das Upsetometer ersetzt den Badge
- Entscheidung steht noch aus

**Implementierung (Schätzung: ~1–2 Pushes):**
- Neue Funktion `calcUpsetLevel(gameId, s1, s2)` → Score 0–100
- HTML-Widget mit `<div class="upset-bar">` + CSS-Gradient
- Integration in `renderGameTipBlock` neben Punkteverteilung

---

### Weitere Features

- **Phase 2 KO-Runden Scoring:** Gruppenklassifikations-Punkte nur wenn Position bestätigt
- **H2H ohne Limit:** Player-Cap entfernen; Dynamisch Mobile 2–3, Desktop 2–10
- **Simulator:** Ländernamen lokalisieren
- **My Form:** `commCalibration` vereinfachen (Näherung `commCalibration ≈ commHit`)
- **Stats-Tab (10 Widgets):** Community-Tipp Badge, Populärster Tipp, POINTS ACHIEVED Chart, DAY WINNER, GROUPS EXPERTS, TOP SCORERS by GOALS, GOLDEN BOOT, CHAMPION CHANGE, UPS & DOWNS, GROUPS avg
- **Konfigurierbares Rang-Umfeld:** Slider/Dropdown im Setup-Modal für ±N Ränge
- **Countdown-Timer:** Nächstes Spiel auf Übersicht-Tab
- **Player Card Visualization:** Panini/FUT-Style Modal

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
- 🃏 „Meine Porra-Karte" (PDF/Image Export via Canvas API)
- 📰 ESPN API Erweiterungen: News-Ticker, Assists/Cards/Shots/Saves Leaders, Game Report Snippet, Team Logos

---

## ✅ Abgeschlossen (Auszug)

| Version | Feature / Fix |
|---|---|
| v1.16.0 | Punkteverteilung Styling, What's New Modal (DE/EN/ES) |
| v1.15.2 | Scoring-Guard: `calcPointDist` nutzt `_calcScore()` statt `scoreGame()` |
| v1.15.1 | Live-Karte zeigt nur eigene Gruppe; Simulator Punkteverteilung |
| v1.15.0 | Punkteverteilung Feature (Live + Simulator Karten) |
| v1.14.5 | Header-Versions-Badge Fix (doppelte ID entfernt) |
| v1.13.9 | ESPN API Range-Key Fix (fehlender Bindestrich) |
| v1.13.8 | Scorer-Doppelzählung Fix (Set für kanonische Game-Keys) |
| v1.13.7 | `Illegal return statement` Fix, `saveSetup` Fix |
| v1.13.6 | ESPN Date Params Fix, Simulator baseRankMap, What's New Modal |
