# Mundiporra 2026 — KO-Phase: Vollständige Planungsdokumentation

> Erstellt: 25. Juni 2026  
> Zuletzt aktualisiert: 26. Juni 2026 (v2.0.27-ko-alpha)  
> Autor: Patrick Fichtner + Claude (AICOMP GPT-Assistent)  
> Zweck: Vollständige Referenz für die Implementierung der KO-Phase im Mundiporra 2026 Dashboard.  
> Diese Datei ermöglicht das nahtlose Wiederanknüpfen in einer neuen Konversation.

---

## 1. Ausgangssituation & Kontext

### Dashboard-Status vor KO-Phase
- Live-URL: https://flash777777.github.io/mundiporra-dashboard/
- Staging-URL: https://flash777777.github.io/mundiporra-staging/
- Aktuelle lokale Entwicklungsversion: **v2.0.27-ko-alpha**
- Single-File-App: alles in `index.html` (HTML + CSS + JS)
- 154 Teilnehmer, 72 Gruppenspiele, Gruppenphase endet ~27./28. Juni 2026

### Zeitplan
- **25. Juni 2026:** Planungssession
- **26. Juni 2026:** Lokale Entwicklung v2.0.0 → v2.0.27-ko-alpha (dieser Stand)
- **28. Juni 2026:** KO-Tipps-Deadline für alle Tipper
- **28. oder 29. Juni 2026:** Nacho sendet konsolidiertes KO-Excel an Patrick
- **Ab 4. Juli 2026 ca.:** KO-Phase beginnt (R32)

---

## 2. Entscheidungen (endgültig getroffen)

### 2.1 Entwicklungsansatz: Lokale HTML-Kopie
**Entschieden:** Lokale HTML-Kopie statt Staging-First.

**Workflow:**
1. Claude liefert HTML-Datei (lokal testbar)
2. Patrick testet, gibt Feedback
3. Iterativ verbessern
4. Wenn stabil → Push auf Staging → Patrick gibt grün → `go live porra`

---

## 3. Regelwerk KO-Phase (vollständig bestätigt & implementiert)

### 3.1 Spielpunkte
| Ergebnis | Punkte (90 min) | × Rundenmultiplier |
|---|---|---|
| Exaktes Ergebnis | 3 | ✅ ja |
| Richtige Tordifferenz | 2 | ✅ ja |
| Nur richtige Tendenz | 1 | ✅ ja |
| Falsch | 0 | — |

**Wichtig:** Nur 90 Minuten zählen (kein Elfmeterschießen, keine Verlängerung).  
**R32-Sonderregel (v2.0.23):** Im R32 werden Spielpunkte immer vergeben, unabhängig ob die Paarung korrekt vorhergesagt wurde.

### 3.2 Qualifikationspunkte — ⚠️ ENTFERNT (v2.0.22)
`ko_qual_pts` vollständig aus Scoring, Rangliste und allen UIs entfernt.

### 3.3 Scorer-Bonus
| | Basis | × Multiplier | Verlängerung | Elfmeter |
|---|---|---|---|---|
| TS1 trifft | +2 | ✅ ja | ✅ zählt | ❌ zählt nicht |
| TS2 trifft | +1 | ✅ ja | ✅ zählt | ❌ zählt nicht |

### 3.4 Champion-Bonus
| Situation | Punkte |
|---|---|
| Korrekt, Tipp NICHT geändert | +10 |
| Korrekt, Tipp GEÄNDERT | +5 |
| Falsch | 0 |

### 3.5 Multiplier-Tabelle
| Runde | Slot-Präfix | Spiele | Multiplier |
|---|---|---|---|
| Round of 32 | R32x | 16 | ×2 |
| Round of 16 | R161–R168 | 8 | ×3 |
| Viertelfinale | QF1–QF4 | 4 | ×4 |
| Halbfinale | SF1–SF2 | 2 | ×5 |
| Spiel 3./4. Platz | `3er` | 1 | ×6 |
| Finale | `F1` | 1 | ×7 |

---

## 4. Excel-Struktur

### 4.1 KO-Excel (kommt 28./29. Juni) — ⏳ AUSSTEHEND
- Enthält alle Tipps aller 154 Tipper für alle KO-Spiele
- Pro Tipper: für jedes KO-Spiel (Slot) Team1-Tipp, Team2-Tipp, Ergebnis-Tipp
- Enthält Champion-Change-Information
- Slots streng nach UTC-Datum sortiert
- Teamnames: `UPPERCASE, teils abgekürzt`

### 4.2 Bekannte Slot-IDs (aus v0.2)
```
R167, R168 → Round of 16 (7+8)
QF1–QF4   → Viertelfinale
SF1–SF2   → Halbfinale
3er        → Spiel um Platz 3
F1         → Finale
```
**R32-Slots:** Benennung TBC — wird beim KO-Excel-Eingang bestätigt.

---

## 5. Implementierte Datenstrukturen

### 5.1 Globale Variablen (nie umbenennen!)
```javascript
let KO_PREDICTIONS = {};   // KO-Tipps aller Tipper (slot-basiert)
let KO_GAMES = [];         // KO-Spielplan
let _koLive = {};          // ESPN Live-Daten für KO-Spiele
let PHASE = 'GROUP';       // 'GROUP' | 'KO'
const SLOT_META = { ... }; // Multiplier pro Slot
const SLOT_TO_ESPN_MAP = {}; // Manueller ESPN-ID-Override
```

### 5.2 KO_GAMES Struktur
```javascript
{
  slot: 'SF1', round: 'SF', roundLabel: 'Halbfinale', multiplier: 5,
  home: 'BRAZIL', away: 'ENGLAND',
  homeScore: 1, awayScore: 1,       // Endstand inkl. ET
  homeScore90: 1, awayScore90: 1,   // 90-min Score (für Scoring)
  isAET: false, isPEN: true,
  status: 'FT',                     // 'pre' | 'LIVE' | 'FT'
  date: '2026-07-14', espnId: '...'
}
```

### 5.3 _koLive Struktur (seit v2.0.27 vollständig)
```javascript
{
  t1Name, t1Abbrev, t1Score, t1Score90, t1Cc,
  t2Name, t2Abbrev, t2Score, t2Score90, t2Cc,
  isLive, isFinal, isAET, isPEN, isScheduled,
  clock, pos1, pos2, rc1, rc2, ht1, ht2, scoringEvents
}
```

### 5.4 KO_PREDICTIONS Struktur
```javascript
{
  "Don Patricio de la Porra": {
    champion: "FRANCE",
    champion_changed: false,
    slots: {
      "R321": { t1: "FRANCE", t2: "SENEGAL", s1: 2, s2: 1 },
      "QF1":  { t1: "FRANCE", t2: "GERMANY", s1: 2, s2: 1 }
    }
  }
}
```

---

## 6. Implementierungsstand (Stand: 26. Juni 2026, v2.0.27-ko-alpha)

### 6.1 Versions-History KO-Alpha
| Version | Was |
|---|---|
| v2.0.0 | Basis: Datenschicht, Scoring-Engine, i18n-Grundgerüst |
| v2.0.19 | KO-Bracket Tab, User Tips, Community Insights |
| v2.0.20 | H2H KO-Mode (Dual-Mode Option A) |
| v2.0.21 | H2H i18n-Keys, GP-Sektion Chevron-Fix |
| v2.0.22 | ko_qual_pts vollständig entfernt |
| v2.0.23 | R32-Sonderregel: pairingOk für R32 immer true |
| v2.0.24 | 90-min Score: fetchKOLiveData AET/PEN-Handling, homeScore90, AET/PEN-Badges |
| v2.0.25 | Stats-Tab KO-Mode, Search-Tab KO-Mode, 12 neue i18n-Keys |
| v2.0.26 | matchCardKOLive() (roter Rand, Torschützen, Live-Minute, PKT-Boxen) |
| v2.0.27 | fetchKOLiveData: scoringEvents, rc, clock, ht, pos in _koLive |

### 6.2 Feature-Status

#### ✅ Implementiert & visuell bestätigt (Screenshot)
| Feature | Version |
|---|---|
| Übersicht-Tab: KO Finished (Pts-Badge, AET/PEN-Badge, 90-min-Hint, PKT-Boxen) | v2.0.24/25 |
| Übersicht-Tab: KO Live (roter Rand, Torschützen TV-Style, Rote Karte, Minute, HZ, PKT-Boxen) | v2.0.27 |
| Punkteverteilung GP-Karten (matchCardFinished, matchCardLive) | v1.x |

#### ✅ Implementiert (Code-Review bestätigt, kein visueller Bug)
| Feature | Version |
|---|---|
| Datenschicht (KO_GAMES, KO_PREDICTIONS, SLOT_META) | v2.0.0 |
| Scoring-Engine (calcKOPoints, calcResultPtsKO, Multiplier) | v2.0.0 |
| Champion Change Penalty (+5/+10) | v2.0.0 |
| KO-Leaderboard Spalten | v2.0.0 |
| Übersicht-Tab KPIs | v2.0.0 |
| matchCardKOUpcoming (Slot, Runde, Multiplikator, Mein Tipp) | v2.0.0 |
| fetchKOLiveData (90-min Score via /summary, scoringEvents, rc, clock, ht, pos) | v2.0.24/27 |
| R32-Sonderregel (pairingOk immer true) | v2.0.23 |
| ko_qual_pts entfernt | v2.0.22 |
| calcKOPointDist (PKT-Boxen KO-Karten mit Multiplier) | v2.0.25 |

#### 🟡 Implementiert — lokaler visueller Test ausstehend
| Feature | Version | Test-Script |
|---|---|---|
| KO-Bracket Tab (Visualisierung, User Tips, Community Insights) | v2.0.19 | Abschnitt 7.2 |
| Games-Tab KO-Mode (Filter, Karten, showKOGameDetail) | v2.0.19 | Abschnitt 7.3 |
| Stats-Tab KO-Mode (Upset, Contrarian, Consensus/Split) | v2.0.25 | Abschnitt 7.4 |
| Search-Tab KO-Mode (KO-Block, Champion-Pick, KO-Pts-Badge) | v2.0.25 | Abschnitt 7.5 |
| H2H KO-Mode (Dual-Mode: KO-Breakdown + kollabierbare GP-Sektion) | v2.0.21 | Abschnitt 7.6 |

#### ⏳ Blocking — warten auf KO-Excel (28./29. Juni)
| Feature | Abhängigkeit |
|---|---|
| parseKOExcel() Dry-Run | KO-Master-Excel von Nacho/Kike |
| R32-Slot-Benennung bestätigen | KO-Excel |
| Champion-Change-Kodierung bestätigen | KO-Excel |
| ESPN API für KO-Spiele testen | KO-Phase-Start (4.7.) |

---

## 7. Test-Scripts (Konsole, lokal)

### 7.1 Übersicht-Tab — ✅ ERLEDIGT (26.6.)
Getestet: KO Finished (Normal/AET/PEN), KO Live (Torschützen, Rote Karte, PKT-Boxen), KO Upcoming.

### 7.2 KO-Bracket Tab — ⏳ AUSSTEHEND
```javascript
PHASE = 'KO';
KO_GAMES = [
  { slot:'R321', round:'R32', roundLabel:'Round of 32', multiplier:2,
    home:'FRANCE', away:'SENEGAL', homeScore:2, awayScore:1,
    homeScore90:2, awayScore90:1, isAET:false, isPEN:false,
    status:'FT', date:'2026-07-04', espnId:'999901' },
  { slot:'QF1', round:'QF', roundLabel:'Viertelfinale', multiplier:4,
    home:'GERMANY', away:'ARGENTINA', homeScore:null, awayScore:null,
    status:'pre', date:'2026-07-11', espnId:'999902' },
  { slot:'SF1', round:'SF', roundLabel:'Halbfinale', multiplier:5,
    home:'TBD', away:'TBD', homeScore:null, awayScore:null,
    status:'pre', date:'2026-07-14', espnId:null },
  { slot:'F1', round:'FIN', roundLabel:'Finale', multiplier:7,
    home:'TBD', away:'TBD', homeScore:null, awayScore:null,
    status:'pre', date:'2026-07-19', espnId:null }
];
KO_PREDICTIONS['Don Patricio de la Porra'] = {
  champion: 'FRANCE', champion_changed: false,
  slots: {
    R321: { t1:'FRANCE', t2:'SENEGAL', s1:2, s2:1 },
    QF1:  { t1:'GERMANY', t2:'ARGENTINA', s1:1, s2:0 },
    SF1:  { t1:'GERMANY', t2:'BRAZIL', s1:2, s2:1 },
    F1:   { t1:'FRANCE', t2:'GERMANY', s1:2, s2:0 }
  }
};
switchTab('kobracket');
// Prüfen: Bracket-Visualisierung, Mein-Tipp-Badge, Community Insights
```

### 7.3 Games-Tab KO-Mode — ⏳ AUSSTEHEND
```javascript
// KO_GAMES + KO_PREDICTIONS wie in 7.2 setzen, dann:
switchTab('games');
// Prüfen: Filter-Tabs (R32/R16/QF/SF/3er/Final), Multiplikator-Badge,
//         Karten-Anzeige, showKOGameDetail aufrufen:
showKOGameDetail('R321');
```

### 7.4 Stats-Tab KO-Mode — ⏳ AUSSTEHEND
```javascript
PHASE = 'KO';
// KO_GAMES mit mind. 1x FT + mehrere Tipper:
KO_PREDICTIONS['Tipper A'] = { slots: { R321: { t1:'SENEGAL', t2:'FRANCE', s1:1, s2:2 } } };
KO_PREDICTIONS['Tipper B'] = { slots: { R321: { t1:'FRANCE', t2:'SENEGAL', s1:3, s2:0 } } };
switchTab('stats');
// Prüfen: Upset-Sektion, Contrarian-Sektion, Consensus/Split-Sektion,
//         dynamische Tab-Titel in DE/EN/ES
```

### 7.5 Search-Tab KO-Mode — ⏳ AUSSTEHEND
```javascript
// KO_GAMES + KO_PREDICTIONS setzen, dann:
switchTab('search');
// "Don Patricio" suchen → showPlayerDetail aufrufen
// Prüfen: KO-Block unter GP-Tabelle, Champion-Pick, Gesamt-KO-Pts-Badge
```

### 7.6 H2H KO-Mode — ⏳ AUSSTEHEND (Re-Test nach Patches)
```javascript
// KO_GAMES + KO_PREDICTIONS setzen, dann:
switchTab('h2h');
// Zwei Spieler auswählen
// Prüfen: KO-Breakdown oben (offen), GP-Sektion kollabierbar, KO-Spiele zuerst
```

---

## 8. Technische Fallstricke (bekannt & gelöst)

| Fallstrick | Lösung | Version |
|---|---|---|
| 90-min Score für Spielpunkte | homeScore90/awayScore90 via /summary API | v2.0.24 |
| AET/PEN: falscher Score für Scoring | fetchKOLiveData holt 90-min linescores | v2.0.24 |
| calcResultPtsKO falscher Aufruf in matchCardKOFinished | Fix | v2.0.24 |
| _koSlotInsights Lookup-Bug + Team-Name-Normalisierung | Fix | v2.0.24 |
| matchCardKOFinished Scoring-Bug | Fix | v2.0.24 |
| const → let für KO_GAMES/KO_PREDICTIONS | Fix | v2.0.24 |
| H2H i18n-Keys fehlend | Fix | v2.0.21 |
| ko_qual_pts in Scoring/UI | Entfernt | v2.0.22 |
| SyntaxError, Console Test Errors, Double-Trophy | Fix | v2.0.24 |
| KO-Live-Karte fehlte (matchCardKOFinished für LIVE genutzt) | matchCardKOLive() | v2.0.26 |
| _koLive hatte keine scoringEvents/clock/ht/pos | fetchKOLiveData erweitert | v2.0.27 |
| calcKOPointDist fehlte (PKT-Boxen in KO-Karten) | calcKOPointDist() | v2.0.25 |
| Gelbe Karten (yc) in matchCardKOLive | fetchKOLiveData parsed yc nicht → kein Problem | v2.0.27 |
| game.id Type Mismatch (Number vs. String) | String(game.id) durchgängig | v2.0.0 |

---

## 9. Patricks Dashboard-Angaben
- **Alias:** Don Patricio de la Porra
- **Champion-Tipp:** Frankreich 🇫🇷
- **Champion geändert:** Nein
- **TS1:** Kylian Mbappé
- **TS2:** Harry Kane (geändert von Ronaldo)
- **Gruppen:** Aicomp, Patrick & Co

---

## 10. Referenz-Repos & Workflow
| | Repo | URL |
|---|---|---|
| 🟢 Live | `Flash777777/mundiporra-dashboard` | https://flash777777.github.io/mundiporra-dashboard/ |
| 🚧 Staging | `Flash777777/mundiporra-staging` | https://flash777777.github.io/mundiporra-staging/ |

- GitHub-Account mit Push-Rechten: `PaFiAIC`
- Live-Deploy nur mit: **`go live porra`**
- Push-Mechanismus: Git Blob API (UTF-8, NIEMALS btoa-Chunking)
- Alle index.html-Pushes: `index.html` + `UI_MAP.md` + `COMPONENT_REGISTRY.md` im selben Tree-Commit

---

*Dokument-Ende. Stand: 26. Juni 2026, v2.0.27-ko-alpha — Patrick Fichtner + Claude.*
