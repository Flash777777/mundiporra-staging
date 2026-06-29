# ⚽ Mundiporra 2026 — KO-Phase Backlog

> Letzte Aktualisierung: 30. Juni 2026
> Dashboard: https://flash777777.github.io/mundiporra-dashboard/
> Staging: https://flash777777.github.io/mundiporra-staging/

---

## 🔴 Bugs (offen)

| # | Bug | Diagnose | Fix-Ansatz | Prio |
|---|---|---|---|---|
| KO-1 | **"Letzte Spiele" zeigt noch Gruppenspiele** | Die "Letzte Spiele Zusammenfassung"-Logik filtert nach Gruppenphase-Game-IDs / Runden-Typ. Das erste KO-Spiel (Südafrika 0–1 Kanada, Game 73) wird nicht als "letztes Spiel" erkannt | Runden-Filter in der "Letzte Spiele"-Logik auf KO-Spiele ausweiten; sicherstellen dass KO-Games korrekt als abgeschlossen erkannt werden | 🔴 Hoch |
| KO-2 | **Upcoming Games: Keine Spielzeit in Karten + Header-Zeit falsch** | Header zeigt nur die Uhrzeit des ersten der angezeigten Spiele (z.B. "19:00 GMT+2" für Brasilien–Japan). Die einzelnen Spielkarten zeigen nur das Datum (z.B. "2026-06-29"), aber keine Uhrzeit. Deutschland–Paraguay läuft z.B. um 22:30, Niederlande–Marokko um 03:00 am Folgetag | (1) In jeder Spielkarte die Spielzeit aus dem Schedule anzeigen (lokalisiert gemäß User-Timezone-Setting); (2) Im Header nur "nächstes Spiel"-Zeit anzeigen oder ganz entfernen | 🔴 Hoch |
| KO-3 | **Kudos-Berechnung: Gleichstand (Tie) wird nicht korrekt aufgeteilt** | Regel: Platz 1 → 60%, Platz 2 → 30%, Platz 3 → 10%. Bei Gleichstand: kombiniertes Preisgeld proportional teilen. Aktuelle Situation: 1 Spieler Rang 1, 2 Spieler auf geteiltem Rang 2. Erwartet: Rang 1 = 60% (1848 Kudos), Rang 2 (2 Spieler) = (30%+10%)/2 = 20% each = 616 Kudos je. Angezeigt: 1848 / 924 / 308 — die beiden Rang-2-Spieler erhalten 30% und 10% separat statt je 20%. Die `prizeIdx`-Logik behandelt Gleichstandsspieler als sequenzielle Positionen statt kombinierte Prize-Slots zu teilen | Kudos-Berechnung: bei mehreren Spielern auf gleichem Rang die Prize-Slots für diesen Rang-Block zusammenfassen und gleichmäßig aufteilen | 🔴 Korrektheit |
| KO-4 | **KO-Bracket Changelog-Claim vs. Implementierung nicht verifiziert** | Changelog behauptet: "Bracket-Tab zeigt alle KO-Spiele mit Echtzeit-Ergebnissen, eigenen Tipps, Paarungsvorhersagen und Community-Verteilung — Update alle 60s". Zu verifizieren: ① Alle KO-Spiele korrekt angezeigt? ② Eigene Tipps pro Spiel sichtbar? ③ Paarungsvorhersagen implementiert oder nur geplant? ④ Community-Verteilung vorhanden? ⑤ Läuft tatsächlich 60s-Refresh für den Bracket-Tab? | Staging-HTML analysieren, Code gegen Changelog-Aussagen abgleichen, ggf. fehlende Features nachliefern oder Changelog korrigieren | 🟡 Integrität |

---

## 🟡 Features (geplant)

| # | Feature | Beschreibung | Prio |
|---|---|---|---|
| KO-F1 | **KO-Simulator** | Analog zum Gruppenphase-Simulator: KO-Spielergebnisse simulieren, Auswirkung auf Rangliste live berechnen. Berücksichtigt KO-Multiplikatoren (×2 bis ×6) | 🟡 Mittel |
| KO-F2 | **Countdown nächste KO-Spiele** | Wie im Gruppen-Modus: Countdown-Timer zum nächsten KO-Spiel auf dem Übersicht-Tab, mit Rundenbezeichnung (z.B. "Viertelfinale in 2h 15min") | 🟢 Low |
| KO-F3 | **Gruppen-Zusammenfassungen: alle Punkte-Klassen anzeigen** | In den verschiedenen Spiel-/Gruppen-Zusammenfassungen (z.B. "Letzte Spiele", "Meine Gruppe") werden aktuell nicht immer alle vier Punkte-Klassen (3 PKT / 2 PKT / 1 PKT / 0 PKT) angezeigt — leere Klassen werden weggelassen. Alle 4 Klassen sollen immer sichtbar sein, auch wenn eine Klasse 0 Spieler enthält, um die Verteilung vollständig ablesbar zu machen | 🟢 Low |

---

## ✅ Erledigt

| Version | Feature/Fix | Datum |
|---|---|---|
| v2.0.44 | KO Live Points implementiert | 27.06.2026 |
| v2.0.45 | KO-Leaderboard Sortierung + Mojibake Fix | 27.06.2026 |
| v2.0.46 | Champion-Change-Penalty (−5 Pts) + Adriel KO-Tips | 28.06.2026 |
| v2.0.47 | CC-Penalty Berechnungsbug behoben, KO-Modal einmalig-fix, CC-Spalte | 29.06.2026 |
