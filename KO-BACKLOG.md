# ⚽ Mundiporra 2026 — KO-Phase Backlog

> Letzte Aktualisierung: 30. Juni 2026
> Dashboard: https://flash777777.github.io/mundiporra-dashboard/
> Staging: https://flash777777.github.io/mundiporra-staging/

---

## 🔴 Bugs (offen)

| # | Bug | Diagnose | Fix-Ansatz | Prio |
|---|---|---|---|---|
| KO-5 | **matchCardKOLive: Kein Perioden-Label bei Verlängerung/Elfmeter** | `matchCardKOLive()` zeigt nur `live.clock + "'"` als Status-Text (z.B. "93'"), nutzt aber **nicht** `fmtLiveStatus()`. Das ESPN-Feld `live.statusLabel` (= `shootout`, `extra_time`, `first_half`, `second_half`) wird zwar korrekt befüllt, aber in der Karte nie ausgewertet. Gruppenphase-Live-Karte zeigt korrekt „🥅 Elfmeter" / „⏱ Verlängerung" / „1. HZ" / „2. HZ" — KO-Karte nicht. i18n-Keys `live_extra_time`, `live_shootout`, `live_first_half`, `live_second_half` existieren bereits in EN/DE/ES. | Fix: In `matchCardKOLive()` `liveLabel` via `fmtLiveStatus({status:'LIVE', statusLabel: live.statusLabel, clock: live.clock})` berechnen statt nur `clock + "'"` | 🟡 UX |
| ~~KO-3~~ | ~~**Kudos-Berechnung: Gleichstand (Tie) wird nicht korrekt aufgeteilt**~~ | Regel: Platz 1 → 60%, Platz 2 → 30%, Platz 3 → 10%. Bei Gleichstand: kombiniertes Preisgeld proportional teilen. Aktuelle Situation: 1 Spieler Rang 1, 2 Spieler auf geteiltem Rang 2. Erwartet: Rang 1 = 60% (1848 Kudos), Rang 2 (2 Spieler) = (30%+10%)/2 = 20% each = 616 Kudos je. Angezeigt: 1848 / 924 / 308 — die beiden Rang-2-Spieler erhalten 30% und 10% separat statt je 20%. Die `prizeIdx`-Logik behandelt Gleichstandsspieler als sequenzielle Positionen statt kombinierte Prize-Slots zu teilen | Kudos-Berechnung: bei mehreren Spielern auf gleichem Rang die Prize-Slots für diesen Rang-Block zusammenfassen und gleichmäßig aufteilen | 🔴 Korrektheit |

---

## 🟡 Features (geplant)

| # | Feature | Beschreibung | Prio |
|---|---|---|---|
| KO-F1 | **KO-Simulator** | Analog zum Gruppenphase-Simulator: KO-Spielergebnisse simulieren, Auswirkung auf Rangliste live berechnen. Berücksichtigt KO-Multiplikatoren (×2 bis ×6) | 🟡 Mittel |
| KO-F3 | **Gruppen-Zusammenfassungen: alle Punkte-Klassen anzeigen** | In den verschiedenen Spiel-/Gruppen-Zusammenfassungen werden aktuell nicht immer alle vier Punkte-Klassen (3 PKT / 2 PKT / 1 PKT / 0 PKT) angezeigt — leere Klassen werden weggelassen. Alle 4 Klassen sollen immer sichtbar sein, auch wenn eine Klasse 0 Spieler enthält | 🟢 Low |

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
