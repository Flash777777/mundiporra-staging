# ⚽ Mundiporra 2026 — KO-Phase Backlog

> Letzte Aktualisierung: 30. Juni 2026
> Dashboard: https://flash777777.github.io/mundiporra-dashboard/
> Staging: https://flash777777.github.io/mundiporra-staging/

---

## 🔴 Bugs (offen)

| # | Bug | Diagnose | Fix-Ansatz | Prio |
|---|---|---|---|---|
| KO-5 | **matchCardKOLive: Kein Perioden-Label bei Verlängerung/Elfmeter** | `matchCardKOLive()` zeigt nur `live.clock + "'"` als Status-Text (z.B. "93'"), nutzt aber **nicht** `fmtLiveStatus()`. Das ESPN-Feld `live.statusLabel` (= `shootout`, `extra_time`, `first_half`, `second_half`) wird zwar korrekt befüllt, aber in der Karte nie ausgewertet. Gruppenphase-Live-Karte zeigt korrekt „🥅 Elfmeter" / „⏱ Verlängerung" / „1. HZ" / „2. HZ" — KO-Karte nicht. i18n-Keys `live_extra_time`, `live_shootout`, `live_first_half`, `live_second_half` existieren bereits in EN/DE/ES. | Fix: In `matchCardKOLive()` `liveLabel` via `fmtLiveStatus({status:'LIVE', statusLabel: live.statusLabel, clock: live.clock})` berechnen statt nur `clock + "'"` | 🟡 UX |
| ~~KO-3~~ | ~~**Kudos-Berechnung: Gleichstand (Tie) wird nicht korrekt aufgeteilt**~~ | **✅ Closed/Verified (v2.0.57)** — Code-Review ergab: `calcKudos()` implementiert Tie-Splitting bereits korrekt via `prizeIdx`-Loop. Backlog-Eintrag war ein Überbleibsel aus Gruppenphase. Kein Fix nötig. | — | ~~🔴 Korrektheit~~ |

---

## 🟡 Features (geplant)

| # | Feature | Beschreibung | Prio |
|---|---|---|---|
| KO-F1 | **KO-Simulator** | Analog zum Gruppenphase-Simulator: KO-Spielergebnisse simulieren, Auswirkung auf Rangliste live berechnen. Berücksichtigt KO-Multiplikatoren (×2 bis ×6) | 🟡 Mittel |
| ~~KO-F3~~ | **Gruppen-Ansichten: KO-Spalten analog Ranking** | ✅ **Fixed v2.0.57** — renderGroupTab() + renderGroupSummary() mit KO-Branch: zeigt GP⚽/GP🎯/GP🏅/KO⚽/KO🎯/🔴/🏆/⚠️ analog Leaderboard; Übersicht zeigt alle Gruppen | ~~🟢 Low~~ |

---

## ✅ Erledigt

| Version | Feature/Fix | Datum |
|---|---|---|
| v2.0.44 | KO Live Points implementiert | 27.06.2026 |
| v2.0.45 | KO-Leaderboard Sortierung + Mojibake Fix | 27.06.2026 |
| v2.0.46 | Champion-Change-Penalty (−5 Pts) + Adriel KO-Tips | 28.06.2026 |
| v2.0.47 | CC-Penalty Berechnungsbug behoben, KO-Modal einmalig-fix, CC-Spalte | 29.06.2026 |
| v2.0.55 | KO-2: Upcoming Games — Zeit + Countdown in Karten + Header | 30.06.2026 |
| v2.0.56 | KO-1: Letzte Spiel-Zusammenfassung zeigt KO-Spiele mit echtem Tip-Grid (renderKOTipBlock) | 30.06.2026 |
| — | KO-4: Analyse abgeschlossen — Changelog korrekt bis auf Nuance: 60s-Refresh aktualisiert Live-Daten global, Bracket re-rendert bei Tab-Aktivierung. Kein Fix nötig. | 30.06.2026 |
| — | KO-F2: Countdown bereits vollständig implementiert — fmtCountdown() + cd-pill in matchCardKOUpcoming() | 30.06.2026 |
