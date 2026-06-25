# Mundiporra 2026 — KO-Phase: Vollständige Planungsdokumentation

> Erstellt: 25. Juni 2026  
> Autor: Patrick Fichtner + Claude (AICOMP GPT-Assistent)  
> Zweck: Vollständige Referenz für die Implementierung der KO-Phase im Mundiporra 2026 Dashboard.  
> Diese Datei ermöglicht das nahtlose Wiederanknüpfen in einer neuen Konversation.

---

## 1. Ausgangssituation & Kontext

### Dashboard-Status vor KO-Phase
- Live-URL: https://flash777777.github.io/mundiporra-dashboard/
- Staging-URL: https://flash777777.github.io/mundiporra-staging/
- Aktuelle Version: ca. v1.19.x (Stand dieser Planungssession)
- Single-File-App: alles in `index.html` (HTML + CSS + JS)
- 154 Teilnehmer, 72 Gruppenspiele, Gruppenphase endet ~27./28. Juni 2026

### Zeitplan
- **25. Juni 2026:** Planungssession (dieser Zeitpunkt)
- **28. Juni 2026:** Alle Tipper müssen KO-Tipps abgegeben haben (enger Zeitraum zwischen letzten Gruppenspielen und Start R32)
- **28. oder 29. Juni 2026:** Nacho sendet konsolidiertes KO-Excel an Patrick
- **Ab 4. Juli 2026 ca.:** KO-Phase beginnt (R32)

---

## 2. Entscheidungen (endgültig getroffen)

### 2.1 Entwicklungsansatz: Lokale HTML-Kopie
**Entschieden:** Lokale HTML-Kopie statt Staging-First.

**Begründung:**
- KO-Phase ist kein inkrementeller Fix, sondern ein struktureller Umbau
- Neues Datenmodell, neue Scoring-Logik, mehrere neue Tabs
- Staging soll nicht tagelang im Halbzustand liegen
- Patrick testet lokal im Browser

**Workflow:**
1. Claude liefert HTML-Datei (lokal testbar)
2. Patrick testet, gibt Feedback
3. Iterativ verbessern
4. Wenn stabil → Push auf Staging → Patrick gibt grün → `go live porra`

---

## 3. Regelwerk KO-Phase (vollständig bestätigt)

### 3.1 Spielpunkte (nur wenn BEIDE Teams korrekt vorhergesagt)
| Ergebnis | Punkte (90 min) | × Rundenm-Multiplier |
|---|---|---|
| Exaktes Ergebnis | 3 | ✅ ja |
| Richtige Tordifferenz, falsches Ergebnis | 2 | ✅ ja |
| Nur richtige Tendenz (Sieg/Unentschieden) | 1 | ✅ ja |
| Falsch | 0 | — |

**Wichtig:** Punkte zählen NUR wenn beide Teams des Spiels korrekt vorhergesagt wurden. Wenn auch nur ein Team falsch ist → 0 Spielpunkte, unabhängig vom getippten Ergebnis.

**Wichtig:** Nur 90 Minuten zählen für Spielpunkte (kein Elfmeterschießen, keine Verlängerung für Spielpunkte).

### 3.2 Qualifikationspunkte
| Vorhersage | Punkte | × Multiplier |
|---|---|---|
| Ein Team für eine Runde korrekt vorhergesagt | +1 pro Team | ❌ NEIN — fix +1, nicht multipliziert |

**Bestätigt:** Pro Runde neu — wenn FRANCE in QF1, SF1 und F1 korrekt vorhergesagt wird, gibt es 3× +1. Konsistent mit dem Gruppenphase-Konzept.

**Hinweis:** In der Gruppenphase gibt es bereits Klassifikationspunkte (+1 pro qualifiziertes Team, +2 bei exakter Position). Diese sind im bestehenden Dashboard bereits implementiert. Die KO-Qualifikationspunkte sind konzeptionell dasselbe Prinzip, aber auf KO-Runden angewendet.

### 3.3 Scorer-Bonus (KO-Phase)
| | Punkte Basis | × Rundenm-Multiplier | Verlängerung | Elfmeter |
|---|---|---|---|---|
| TS1 trifft | +2 | ✅ ja (Spielmultiplier der Runde) | ✅ zählt | ❌ zählt nicht |
| TS2 trifft | +1 | ✅ ja (Spielmultiplier der Runde) | ✅ zählt | ❌ zählt nicht |

**Konkret:** Ein TS1-Tor im Halbfinale = +2 × 5 = +10 Punkte. Ein TS1-Tor im Finale (inkl. Verlängerung) = +2 × 7 = +14 Punkte.

### 3.4 Champion-Bonus
| Situation | Punkte |
|---|---|
| Champion korrekt vorhergesagt, Tipp NICHT geändert | +10 |
| Champion korrekt vorhergesagt, Tipp GEÄNDERT | +5 (Halbierung als Strafe) |
| Champion falsch | 0 |

**Champion Change:** Nacho trackt Änderungen. Im KO-Excel wird die Information über Änderungen enthalten sein (vermutlich als Flag oder in der CHAMPION CHANGE-Matrix aus dem Statistics-Sheet des Excels). Der Wert `champion_changed: true/false` wird beim Parsen des KO-Excels gesetzt.

### 3.5 Multiplier-Tabelle (final, alle Runden)
| Runde | Slot-Präfix | Anzahl Spiele | Multiplier |
|---|---|---|---|
| Round of 32 | R32_x (Benennung TBC) | 16 | ×2 |
| Round of 16 | R161–R168 | 8 | ×3 |
| Viertelfinale | QF1–QF4 | 4 | ×4 |
| Halbfinale | SF1–SF2 | 2 | ×5 |
| Spiel 3./4. Platz | `3er` | 1 | ×6 |
| Finale | `F1` | 1 | ×7 |

**Gesamtspiele gesamt:** 72 (Gruppenphase) + 32 (KO) = **104 Spiele**

---

## 4. Excel-Struktur (Analyse von Mundiporra 2026_v0.2.xlsx)

### 4.1 Bereits bekannte Sheet-Struktur
- `Punct`: Haupt-Sheet mit allen Tipps aller Tipper. Pro Zeile ein Tipper. Enthält Spalten für:
  - Spieler-Name, Punkte, TS1, TS2, Champion-Tipp, Gruppen-Zugehörigkeit
  - KO-Slot-Tipps (bereits vorhanden als Spalten, in v0.2 noch ungefüllt)
- `Inputs`: Spielplan mit UTC-Datum/Uhrzeit (72 Gruppenspiele)
- `TABLE`: Aktuelle Rangliste mit Bonus-Punkten; TS1/TS2-Namen in Cols D+E
- `Rules`: Multiplikatoren, Penalties, Sonderregeln
- `Goals`: Torjäger-Tracking
- `Statistics`: Komplexe Statistik-Matrix. Enthält bereits:
  - `KO STAGE - LONGEST FORECASTED PATH`
  - `FORECASTED FINAL`
  - `KO STAGE RESULTS`
  - `CHAMPION CHANGE` (Matrix: Original → Actual, d.h. wer von welchem Team zu welchem gewechselt hat)
- Gruppen-Sheets: Tipps pro Porra-Gruppe

### 4.2 KO-Slot-Benennung im Excel
Im `Punct`-Sheet sind folgende Slot-IDs direkt sichtbar:
```
R167, R168           → Round of 16, Spiele 7+8 (Runde hat R161–R168)
QF1, QF2, QF3, QF4  → Viertelfinale
SF1, SF2             → Halbfinale
3er                  → Spiel um Platz 3
F1                   → Finale
```
**R32-Slots:** Noch nicht sichtbar in der vorliegenden Excel-Version (ungefüllt). Die Benennung muss beim Eingang des KO-Excels am 28./29.6. bestätigt werden. Vermutung: durchnummeriert, möglicherweise `R321`–`R3216` oder ähnlich.

### 4.3 KO-Excel (kommt 28./29. Juni)
- **Struktur: identisch zum aktuellen Gruppen-Excel**
- Enthält alle Tipps aller 154 Tipper für alle KO-Spiele
- Pro Tipper: für jedes KO-Spiel (Slot) ein Team1-Tipp, Team2-Tipp, Ergebnis-Tipp
- Enthält Champion-Change-Information (ob geändert und von/zu welchem Team)
- Enthält ggf. aktualisierte TS1/TS2 (die Tipper können diese nicht mehr ändern, aber falls doch...)
- Slots sind **streng nach UTC-Datum sortiert** — das ist Nachos Ordnungsprinzip

### 4.4 Beobachtung: UTC-Sortierung vs. FIFA-Chronologie
Nacho sortiert die Slots im Excel nach UTC-Startzeit. Die FIFA kann davon abweichen (z.B. Nachholspiele, kurzfristige Umplanungen). Das bedeutet: Die Slot-Nummer `QF1` ist nicht garantiert dasselbe Spiel wie ESPN-Event-ID X. Wir brauchen eine Mapping-Logik.

### 4.5 Bereits aus dem Excel bekannte Champion-Change-Fälle (Statistics-Sheet)
Aus der v0.2 sichtbar (Beispiele):
- FRANCE → ENGLAND
- FRANCE → GERMANY (mehrfach)
- FRANCE → SPAIN
- etc.
Das zeigt: Viele Tipper haben ihren Champion-Tipp bereits geändert. Diese Info steckt in der `CHAMPION CHANGE`-Matrix im Statistics-Sheet.

---

## 5. Architektur-Design: Neue Datenstrukturen

### 5.1 Neue globale Variablen (nie umbenennen!)

```javascript
// KO-Tipps aller Tipper
const KO_PREDICTIONS = {
  "Don Patricio de la Porra": {
    champion: "FRANCE",
    champion_changed: false,
    slots: {
      "R32_1":  { t1: "GERMANY",  t2: "BRAZIL",   s1: 2, s2: 1 },
      "R161":   { t1: "FRANCE",   t2: "ENGLAND",  s1: 2, s2: 1 },
      "QF1":    { t1: "FRANCE",   t2: "GERMANY",  s1: 2, s2: 1 },
      "SF1":    { t1: "FRANCE",   t2: "SPAIN",    s1: 1, s2: 0 },
      "SF2":    { t1: "GERMANY",  t2: "BRAZIL",   s1: 2, s2: 1 },
      "3er":    { t1: "SPAIN",    t2: "BRAZIL",   s1: 2, s2: 1 },
      "F1":     { t1: "FRANCE",   t2: "GERMANY",  s1: 2, s2: 0 },
    }
  }
};

// KO-Spielplan
const KO_GAMES = [
  {
    id: 73,
    slot: "R32_1",
    round: "R32",
    multiplier: 2,
    home: "FRANCE",
    away: "MEXICO",
    homeScore: null,
    awayScore: null,
    date: "2026-07-04T18:00:00Z",
    status: "pre",
    espnId: null
  }
];

// Slot-Metadaten
const SLOT_META = {
  "R32_1":  { round: "R32",  multiplier: 2 },
  "R161":   { round: "R16",  multiplier: 3 },
  "QF1":    { round: "QF",   multiplier: 4 },
  "SF1":    { round: "SF",   multiplier: 5 },
  "3er":    { round: "3PL",  multiplier: 6 },
  "F1":     { round: "FIN",  multiplier: 7 },
};

// ESPN-Slot-Override
const SLOT_TO_ESPN_MAP = {};

// Phasen-Steuerung
const PHASE = 'GROUP'; // → nach Gruppenphase auf 'KO' setzen
```

### 5.2 Erweiterung bestehender Strukturen

```javascript
// ALL_GAMES bleibt unverändert (Gruppenspiele 1–72)
// KO_GAMES ist SEPARAT (nicht in ALL_GAMES reingemischt)
// Begründung: Unterschiedliche Scoring-Logik, unterschiedliche Datenquellen

// ALL_PREDICTIONS bleibt unverändert (Gruppenphase-Tipps)
// KO_PREDICTIONS ist SEPARAT
// Begründung: Wird aus separatem KO-Excel geladen, andere Struktur
```

---

## 6. Scoring-Algorithmus (Pseudocode / Implementierungsreferenz)

### 6.1 Haupt-Scoring-Funktion für KO

```javascript
function calcKOPoints(playerName) {
  const result = {
    ko_game_pts: 0,
    ko_qual_pts: 0,
    ko_scorer_pts: 0,
    champion_pts: 0,
    breakdown: {}
  };

  const pred = KO_PREDICTIONS[playerName];
  if (!pred) return result;

  for (const [slot, tip] of Object.entries(pred.slots)) {
    const game = KO_GAMES.find(g => g.slot === slot);
    if (!game || game.status !== 'FT') continue;

    const mult = SLOT_META[slot]?.multiplier ?? 1;
    const actualT1 = normalize(game.home);
    const actualT2 = normalize(game.away);
    const predT1   = normalize(tip.t1);
    const predT2   = normalize(tip.t2);

    // Qualifikationspunkte: fix +1, kein Multiplier
    const t1Correct = (predT1 === actualT1 || predT1 === actualT2);
    const t2Correct = (predT2 === actualT1 || predT2 === actualT2);
    let qualPts = 0;
    if (t1Correct) qualPts += 1;
    if (t2Correct && predT2 !== predT1) qualPts += 1;
    result.ko_qual_pts += qualPts;

    // Spielpunkte: nur wenn BEIDE Teams korrekt
    const bothTeamsCorrect = t1Correct && t2Correct && predT1 !== predT2;
    if (bothTeamsCorrect) {
      const gamePts = calcResultPoints(tip.s1, tip.s2, game.homeScore, game.awayScore);
      result.ko_game_pts += gamePts * mult;
      result.breakdown[slot] = { gamePts, mult, qualPts };
    } else {
      result.breakdown[slot] = { gamePts: 0, mult, qualPts };
    }
  }

  // Scorer-Bonus (Verlängerung zählt, Elfmeter nicht)
  for (const game of KO_GAMES) {
    if (game.status !== 'FT') continue;
    const mult = SLOT_META[game.slot]?.multiplier ?? 1;
    const ts1Goals = getPlayerGoalsInGame(pred.ts1, game, { excludeShootout: true });
    const ts2Goals = getPlayerGoalsInGame(pred.ts2, game, { excludeShootout: true });
    result.ko_scorer_pts += (ts1Goals * 2 + ts2Goals * 1) * mult;
  }

  // Champion-Bonus
  if (TOURNAMENT_FINISHED && WORLD_CHAMPION) {
    if (normalize(pred.champion) === normalize(WORLD_CHAMPION)) {
      result.champion_pts = pred.champion_changed ? 5 : 10;
    }
  }

  return result;
}
```

### 6.2 Gesamtpunkte-Berechnung

```javascript
function calcTotalPoints(playerName) {
  const gpPts = calcGroupPhasePoints(playerName);
  const koPts = calcKOPoints(playerName);

  return {
    gp_game_pts:    gpPts.game_pts,
    gp_scorer_pts:  gpPts.scorer_pts,
    gp_classif_pts: gpPts.classif_pts,
    ko_game_pts:    koPts.ko_game_pts,
    ko_qual_pts:    koPts.ko_qual_pts,
    ko_scorer_pts:  koPts.ko_scorer_pts,
    champion_pts:   koPts.champion_pts,
    total: gpPts.game_pts + gpPts.scorer_pts + gpPts.classif_pts
         + koPts.ko_game_pts + koPts.ko_qual_pts + koPts.ko_scorer_pts
         + koPts.champion_pts
  };
}
```

### 6.3 calcResultPoints (identisch mit Gruppenphase)

```javascript
function calcResultPoints(predH, predA, actualH, actualA) {
  if (predH === actualH && predA === actualA) return 3;
  const predDiff   = predH - predA;
  const actualDiff = actualH - actualA;
  if (predDiff === actualDiff) return 2;
  const predTend   = Math.sign(predDiff);
  const actualTend = Math.sign(actualDiff);
  if (predTend === actualTend) return 1;
  return 0;
}
```

---

## 7. ESPN API: Slot-Matching

### 7.1 Problem
- Nacho sortiert Slots nach UTC-Startzeit (Slot R32_1 = frühestes R32-Spiel UTC)
- FIFA kann davon abweichen (Nachholspiele, kurzfristige Änderungen)
- ESPN API hat eigene Event-IDs

### 7.2 Matching-Strategie
**Primär:** UTC-Sortierung als Anker
1. Alle R32-Spiele aus ESPN API nach Datum sortieren
2. Ersten ESPN-Event → R32_1, zweiten → R32_2, usw.

**Fallback:** Manueller Override via `SLOT_TO_ESPN_MAP`
- Bei FIFA-Abweichung: Patrick befüllt `SLOT_TO_ESPN_MAP` manuell
- Format: `{ "R32_1": "espn_event_id" }`

**Team-basierte Verifikation:** Nach dem Matching prüfen ob die Teams im ESPN-Event mit den Tipper-Tipps übereinstimmen — nicht als Hard-Block, aber als Debug-Ausgabe.

---

## 8. Tab-für-Tab Implementierungsplan

### 8.1 Header-Badge
- `PHASE === 'GROUP'` → „Gruppenphase"
- `PHASE === 'KO'` → „KO-Phase"

### 8.2 TAB 1 — Übersicht (#tab-overview)
- „Durchschnittliche Punkte pro Spiel": Basis = ALLE gespielten Spiele (72 Gruppe + gespielte KO)
- „Gespielte Spiele": TOTAL_GAMES = 104
- LAST RESULT CARD: muss KO_GAMES kennen
- NEXT MATCH CARD: muss KO_GAMES kennen
- LIVE GAMES SUMMARY BLOCK: muss KO_GAMES einschließen
- LATEST GAME SUMMARY + UPCOMING GAMES: muss KO_GAMES einschließen
- GROUP SUMMARY CARD: zeigt Gruppenphase-Ergebnisse historisch, keine Änderung nötig

### 8.3 TAB 2 — Rangliste (#tab-leaderboard)
Neue Punkte-Spalten:
| Spalte | Inhalt |
|---|---|
| GP Spiel | Gruppenphase Spielpunkte |
| GP Scorer | Gruppenphase Scorer-Bonus |
| GP Klassif. | Gruppenphase Klassifikationspunkte |
| KO Spiel | KO Spielpunkte (× Multiplier enthalten) |
| KO Qualif. | KO Qualifikationspunkte (fix +1) |
| KO Scorer | KO Scorer-Bonus (× Multiplier enthalten) |
| Champion | Champion-Bonus (5 oder 10) |
| **Gesamt** | Summe aller obigen |

### 8.4 TAB 3 — Meine Gruppe (#tab-group)
Analog TAB 2.

### 8.5 TAB 4 — H2H (#tab-h2h)
Analog TAB 2.

### 8.6 TAB 5 — Spiele (#tab-games)
- Neue Sektion KO-Spiele mit Filter-Tabs pro Runde
- Jede KO-Runde zeigt Multiplier-Badge (z.B. „×3")
- Wenn Teams noch nicht feststehen: Platzhalter

### 8.7 TAB 6 — KO-Bracket (#tab-kobracket)
- Visueller Turnierplan
- ESPN-API-Build: Teams füllen sich nach und nach ein
- Tipper-Tipp-Overlay für eingeloggten User
- Spiel um Platz 3 als eigenständiger Branch (parallel zum Finalbaum):
```
R32 → R16 → QF → SF → Finale
                    ↘ 3./4. Platz
```

### 8.8 TAB 7 — Gruppen (#tab-gruppen)
- Gruppenstandings historisch eingefroren
- Punkte-Breakdown um KO-Klassen erweitern

### 8.9 TAB 8 — Campeones (#tab-champions)
- Original-Tipp + ggf. geänderter Tipp anzeigen
- Bei Änderung: visuell kennzeichnen (durchgestrichen → neu)
- Punkteerwartung: „10 Punkte möglich" / „5 Punkte (geändert)"

### 8.10 TAB 9 — Statistiken (#tab-stats)
- Bis auf Weiteres: Leeren Placeholder mit Meldung „Statistiken werden für die KO-Phase überarbeitet"
- Oder: nur KO-kompatible Widgets (TOP SCORERS, GOLDEN BOOT)

### 8.11 TAB 10 — Suche (#tab-search)
Keine Änderung.

### 8.12 TAB 11 — Datenbasis (#tab-database)
- Neuer Block „KO-Tipps" analog zu ALL_PREDICTIONS

### 8.13 TAB 12 — Changelog (#tab-changelog)
Bleibt wie gehabt.

### 8.14 Simulator
- Muss KO-Runden mit Multiplier simulieren
- Eingabe: erwartete KO-Ergebnisse pro Slot
- Ausgabe: simulierter Endstand

---

## 9. Implementierungsphasen

### Phase 1 — Datenschicht (sofort, vor KO-Excel-Eingang)
1. Excel-Konverter für KO-Slots
2. `PHASE`-Variable (`'GROUP'` / `'KO'`)
3. `SLOT_META`-Map
4. `KO_GAMES`-Array (mit Platzhaltern)
5. `SLOT_TO_ESPN_MAP` (initial leer)

### Phase 2 — Scoring-Engine
1. `calcKOPoints()`
2. `buildLeaderboard()` erweitern
3. Champion-Change-Logik
4. `calcTotalPoints()` als zentrale Funktion

### Phase 3 — UI (Priorität hoch → niedrig)
1. Rangliste (TAB 2)
2. Übersicht-KPIs (TAB 1)
3. Spiele (TAB 5)
4. Campeones (TAB 8)
5. Meine Gruppe (TAB 3) + H2H (TAB 4)
6. Datenbasis (TAB 11)
7. Header-Badge
8. Statistiken (TAB 9) — ausblenden

### Phase 4 — ESPN-Matching & Live
1. KO-Spiele aus ESPN API laden
2. Slot-Matching-Logik
3. Live-Anzeige für KO-Spiele

### Phase 5 — KO-Bracket & Simulator
1. Bracket-Visualisierung
2. Tipper-Tipp-Overlay
3. Spiel-um-Platz-3-Branch
4. Simulator KO-Runden

---

## 10. Offene Punkte

### Geklärt ✅
- [x] Entwicklungsansatz: Lokale HTML-Kopie
- [x] Champion Change Penalty: 5 statt 10 Punkte
- [x] Qualifikationspunkte: fix +1, NICHT multipliziert
- [x] Qualifikationspunkte: pro Runde neu (kumulativ)
- [x] Scorer-Multiplier: derselbe wie das Spiel
- [x] Verlängerungstore: zählen für Scorer-Bonus
- [x] Elfmetertore: zählen NICHT
- [x] Spielpunkte: nur 90 Minuten
- [x] KO-Excel: kommt 28./29. Juni, Struktur identisch
- [x] Spiel um Platz 3: Teil des Turnierbaums (Slot `3er`, ×6)

### Offen ❓
- [ ] **R32-Slot-Benennung:** Wie benennt Nacho die 16 R32-Slots? Wird beim KO-Excel-Eingang klar.
- [ ] **Champion-Change-Kodierung im KO-Excel:** Boolean-Flag oder Vergleich Original vs. Aktuell?
- [ ] **ESPN API für KO:** Ob bestehende Scoreboard-API KO-Spiele liefert, muss nach 28.6. getestet werden.
- [ ] **TS1/TS2 im KO-Excel:** Können Tipper Torschützen-Tipps noch ändern? Vermutlich nicht.
- [ ] **Tie-Breaking in KO-Rangliste:** Dieselben Regeln wie Gruppenphase (total || pts || exact)?

---

## 11. Technische Fallstricke

### 11.1 Doppelzählung bei Qualifikationspunkten
```javascript
if (t2Correct && predT2 !== predT1) qualPts += 1; // Guard gegen Doppel-Team
```

### 11.2 Team-Name-Normalisierung
Bestehende `normalize()`-Funktion wiederverwenden + KO-spezifische Mappings ergänzen.

### 11.3 `game.id` Type Mismatch (bekannt)
`game.id` ist Number, KO-Predictions-Keys sind String → immer `String(game.id)`.

### 11.4 keyRev-Einträge in liveGames (bekannt)
Fix (Set für kanonische Keys) muss auch für KO-Spiele gelten.

### 11.5 ALL_GAMES vs. KO_GAMES — keine Vermischung
Strikt getrennt halten. Funktionen müssen explizit entscheiden welches Array sie verwenden.

### 11.6 Tab-IDs nicht umbenennen
Bestehende Tab-IDs erhalten. Neue Tabs (#tab-kobracket, #tab-gruppen) existieren bereits.

---

## 12. Versions-Planung

| Version | Milestone |
|---|---|
| `v2.0.0-ko-alpha` | Lokale Entwicklungsversion: Datenschicht + Scoring |
| `v2.0.0-ko-beta` | Lokale Entwicklungsversion: UI komplett |
| `v2.0.0` | Erstes stabiles KO-Release auf Staging |
| `v2.0.x` | Bug-Fixes nach erstem Live-Einsatz |

---

## 13. Patricks Dashboard-Angaben

- **Alias:** Don Patricio de la Porra
- **Champion-Tipp:** Frankreich 🇫🇷
- **Champion geändert:** Nein (Stand Planungssession 25.6.2026)
- **TS1:** Kylian Mbappé
- **TS2:** Harry Kane (geändert von Ronaldo)
- **Gruppen:** Aicomp, Patrick & Co

---

## 14. Referenz-Repos & Workflow

| | Repo | URL |
|---|---|---|
| 🟢 Live | `Flash777777/mundiporra-dashboard` | https://flash777777.github.io/mundiporra-dashboard/ |
| 🚧 Staging | `Flash777777/mundiporra-staging` | https://flash777777.github.io/mundiporra-staging/ |

- GitHub-Account mit Push-Rechten: `PaFiAIC`
- Live-Deploy nur mit: **`go live porra`**
- Push-Mechanismus: Git Blob API (UTF-8, NIEMALS btoa-Chunking)
- Alle index.html-Pushes: `index.html` + `UI_MAP.md` + `COMPONENT_REGISTRY.md` im selben Tree-Commit

---

*Dokument-Ende. Stand: 25. Juni 2026, Planungssession Patrick Fichtner + Claude.*
