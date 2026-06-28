# Ã°ÂÂÂºÃ¯Â¸Â Mundiporra Dashboard Ã¢ÂÂ UI Map
> Kanonische Komponentennamen fÃÂ¼r Patrick Ã¢ÂÂ Claude Kommunikation
> Stand: v1.23.20 ÃÂ· Repo: `Flash777777/mundiporra-staging` + `mundiporra-dashboard`

**Konvention:** `Kanonischer Name` Ã¢ÂÂ `fn()` / `#id` / `.class`
Wenn Patrick "X" sagt Ã¢ÂÂ Claude adressiert exakt den Code hinter "X". Keine Interpretation.

---

## GLOBALE SHELL

```
Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ
Ã¢ÂÂ  STAGING BANNER          .staging-banner                Ã¢ÂÂ  Ã¢ÂÂ nur staging-URL sichtbar
Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ
Ã¢ÂÂ  HEADER                                                 Ã¢ÂÂ
Ã¢ÂÂ    App-Titel (statisch)  Version Badge  #headerVersionBadge Ã¢ÂÂ
Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ
Ã¢ÂÂ  TAB-NAV BAR                                            Ã¢ÂÂ
Ã¢ÂÂ  [Ã°ÂÂÂ Zusammenfassung] [Ã°ÂÂÂ Rangliste] [Ã°ÂÂÂ¥ Gruppe]        Ã¢ÂÂ
Ã¢ÂÂ  [Ã¢ÂÂÃ¯Â¸Â Vergleich] [Ã¢ÂÂ½ Spiele] [Ã¢ÂÂÃ¯Â¸Â Bracket] [Ã°ÂÂÂÃ¯Â¸Â Gruppen]   Ã¢ÂÂ
Ã¢ÂÂ  [Ã¢Â­Â Campeones] [Ã°ÂÂÂ Statistiken] [Ã°ÂÂÂ Suche]             Ã¢ÂÂ
Ã¢ÂÂ  [Ã°ÂÂÂÃ¯Â¸Â Datenbasis] [Ã°ÂÂÂ Log]                               Ã¢ÂÂ
Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ
```

### Globale Modals (immer verfÃÂ¼gbar, tab-unabhÃÂ¤ngig)

| Kanonischer Name     | ID / Funktion         | ÃÂffnet sich wennÃ¢ÂÂ¦                     |
|----------------------|-----------------------|---------------------------------------|
| **Setup Modal**      | `#setupModal`         | Erstaufruf / kein User gesetzt        |
| **Force Reload Modal** | `#forceReloadModal` | User klickt Reload-Button             |
| **Sanity Modal**     | `#sanityModal`        | Datenvalidierungsfehler               |
| **Porra Card Modal** | `#porra-card-modal`   | `showMyPorraCard()` aufgerufen        |

---

## TAB 1 Ã¢ÂÂ Ã°ÂÂÂ Zusammenfassung (`#tab-overview`)

```
Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ
Ã¢ÂÂ  KPI GRID                           #kpiGrid            Ã¢ÂÂ
Ã¢ÂÂ  Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ ...     Ã¢ÂÂ
Ã¢ÂÂ  Ã¢ÂÂ Rang Ã¢ÂÂ Ã¢ÂÂ Pts  Ã¢ÂÂ Ã¢ÂÂ Form Ã¢ÂÂ Ã¢ÂÂMomt. Ã¢ÂÂ Ã¢ÂÂRÃÂ¼ckstÃ¢ÂÂ         Ã¢ÂÂ
Ã¢ÂÂ  Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ         Ã¢ÂÂ
Ã¢ÂÂ  [Toggle: Mehr/Weniger KPIs]                            Ã¢ÂÂ
Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ
Ã¢ÂÂ  Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ  Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ Ã¢ÂÂ
Ã¢ÂÂ  Ã¢ÂÂ  LAST RESULT CARD    Ã¢ÂÂ  Ã¢ÂÂ  NEXT MATCH CARD         Ã¢ÂÂ Ã¢ÂÂ
Ã¢ÂÂ  Ã¢ÂÂ  #lastMatchCard      Ã¢ÂÂ  Ã¢ÂÂ  #nextMatchCard          Ã¢ÂÂ Ã¢ÂÂ
Ã¢ÂÂ  Ã¢ÂÂ  Ã¢ÂÂ FT Match Card(s)  Ã¢ÂÂ  Ã¢ÂÂ  Ã¢ÂÂ Live/Upcoming Card(s) Ã¢ÂÂ Ã¢ÂÂ
Ã¢ÂÂ  Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ  Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ Ã¢ÂÂ
Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ
Ã¢ÂÂ  LIVE GAMES SUMMARY BLOCK           #liveGamesSummaryBlock Ã¢ÂÂ
Ã¢ÂÂ  (nur sichtbar wenn Ã¢ÂÂ¥1 Spiel LIVE)                      Ã¢ÂÂ
Ã¢ÂÂ  Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ   Ã¢ÂÂ
Ã¢ÂÂ  Ã¢ÂÂ  Ã°ÂÂÂ´ Live Ã¢ÂÂ N Spiele  (animiert)                  Ã¢ÂÂ   Ã¢ÂÂ
Ã¢ÂÂ  Ã¢ÂÂ  Ã¢ÂÂ Tip Block (je Live-Spiel, nur Gruppe + User)  Ã¢ÂÂ   Ã¢ÂÂ
Ã¢ÂÂ  Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ   Ã¢ÂÂ
Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ
Ã¢ÂÂ  Ã¢ÂÂ¼ LATEST GAME SUMMARY (collapsible) #latestGamesBody   Ã¢ÂÂ
Ã¢ÂÂ  Ã¢ÂÂ¼ UPCOMING GAMES SUMMARY (collapsible) #upcomingGamesBody Ã¢ÂÂ
Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ
Ã¢ÂÂ  Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ  Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ Ã¢ÂÂ
Ã¢ÂÂ  Ã¢ÂÂ  GROUP SUMMARY CARD  Ã¢ÂÂ  Ã¢ÂÂ  KUDOS POOL CARD         Ã¢ÂÂ Ã¢ÂÂ
Ã¢ÂÂ  Ã¢ÂÂ  #groupSummaryContentÃ¢ÂÂ  Ã¢ÂÂ  #kuDosSplit             Ã¢ÂÂ Ã¢ÂÂ
Ã¢ÂÂ  Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ  Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ Ã¢ÂÂ
Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ
```

| Kanonischer Name              | Funktion / ID                         | Beschreibung                              |
|-------------------------------|---------------------------------------|-------------------------------------------|
| **KPI Grid**                  | `renderKPIs()` / `#kpiGrid`           | Kennzahlen-Kacheln (Rang, Pts, FormÃ¢ÂÂ¦)     |
| **KPI Toggle**                | `#kpiCollapsWrap` / `#kpiToggleBtn`   | Mehr/Weniger KPIs ein-/ausblenden         |
| **Last Result Card**          | `#lastMatchCard` / `#lastMatchContent`| Letzter abgeschlossener Spieltag-Slot     |
| **Next Match Card**           | `#nextMatchCard` / `#nextMatchContent`| NÃÂ¤chster Kick-off oder laufende Spiele    |
| **Live Games Summary Block**  | `#liveGamesSummaryBlock`              | Erscheint nur wenn Ã¢ÂÂ¥1 Spiel LIVE          |
| **Latest Game Summary**       | `#latestGamesBody` (collapsible)      | Letzte abgeschlossene Spiele (aufklappbar)|
| **Upcoming Games Summary**    | `#upcomingGamesBody` (collapsible)    | NÃÂ¤chste Spiele (aufklappbar)              |
| **Group Summary Card**        | `#groupSummaryContent`                | Mini-Leaderboard der eigenen Gruppe       |
| **Kudos Pool Card**           | `#kuDosSplit`                         | Preisgeld-Verteilungs-Balken              |

---

## TAB 2 Ã¢ÂÂ Ã°ÂÂÂ Rangliste (`#tab-leaderboard`)

| Kanonischer Name          | Funktion / ID                | Beschreibung                   |
|---------------------------|------------------------------|--------------------------------|
| **Leaderboard Table**     | `renderLeaderboard()` / `#lbTable` / `#lbBody` | VollstÃÂ¤ndige Rangliste aller 154 Spieler |
| **You-Legend**            | `#lbYouLegend` / `#lbYouTag` | Legende fÃÂ¼r eigene Zeile       |

---

## TAB 3 Ã¢ÂÂ Ã°ÂÂÂ¥ Meine Gruppe (`#tab-group`)

| Kanonischer Name              | Funktion / ID                  | Beschreibung                      |
|-------------------------------|--------------------------------|-----------------------------------|
| **Group Tab Leaderboard**     | `renderGroupTab()` / `#groupTabContent` | Gruppen-interne Rangliste inkl. Klassifikationspunkte (Ã°ÂÂÂ) |
| **Latest Game in Group**      | `renderGroupLatestGame()` / `#groupLatestGame` | Letztes Spiel mit Gruppen-Tipps |

---

## TAB 4 Ã¢ÂÂ Ã¢ÂÂÃ¯Â¸Â Vergleich / H2H (`#tab-h2h`)

| Kanonischer Name          | Funktion / ID               | Beschreibung                        |
|---------------------------|-----------------------------|-------------------------------------|
| **H2H Player Selectors**  | `#h2hSelectorRows` / `#h2hAddBtn` | Spieler-Auswahl-Zeilen        |
| **H2H Summary Table**     | `#h2hSummary`               | Punkte-Vergleich je Kategorie       |
| **H2H Games Table**       | `#h2hGamesWrap`             | Spiel-fÃÂ¼r-Spiel Vergleich           |

---

## TAB 5 Ã¢ÂÂ Ã¢ÂÂ½ Spiele (`#tab-games`)

| Kanonischer Name      | Funktion / ID                   | Beschreibung                         |
|-----------------------|---------------------------------|--------------------------------------|
| **Games Grid**        | `renderGames()` / `#gamesGrid`  | Spiel-Kacheln mit Tipp-Badge         |
| **Game Detail Panel** | `showGameDetail()` / `#gameDetailPanel` | Aufklappbares Detail aller Tipps |

---

## TAB 6 Ã¢ÂÂ Ã¢ÂÂÃ¯Â¸Â KO-Bracket (`#tab-kobracket`) Ã¢ÂÂ NEU seit v1.23.0

```
Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ
Ã¢ÂÂ  KO BRACKET VIEW         #koBracketContent              Ã¢ÂÂ
Ã¢ÂÂ  Desktop: horizontales Bracket-Layout (zoom-fÃÂ¤hig)      Ã¢ÂÂ
Ã¢ÂÂ  Mobile:  vertikales Bracket-Layout                     Ã¢ÂÂ
Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ
Ã¢ÂÂ  Runden: Achtelfinale Ã¢ÂÂ Viertelfinale Ã¢ÂÂ Halbfinale      Ã¢ÂÂ
Ã¢ÂÂ           Ã¢ÂÂ Spiel um Platz 3 Ã¢ÂÂ Finale                   Ã¢ÂÂ
Ã¢ÂÂ  Jede Matchcard: Team A vs Team B, Ergebnis/Tipp        Ã¢ÂÂ
Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ
```

| Kanonischer Name          | Funktion / ID                   | Beschreibung                          |
|---------------------------|---------------------------------|---------------------------------------|
| **KO Bracket Container**  | `renderKOBracket()` / `#koBracketContent` | Gesamter Bracket-View         |
| **KO Match Card**         | `_buildKOMatchCard()`           | Einzelne Match-Card im Bracket        |
| **KO Desktop Layout**     | `_buildKODesktop()`             | Desktop-Bracket (horizontal, zoom)    |
| **KO Mobile Layout**      | `_buildKOMobile()`              | Mobile-Bracket (vertikal)             |
| **KO Zoom Controls**      | `_koZoomIn/Out/Reset()`         | Zoom-Buttons Desktop                  |

---

## TAB 7 Ã¢ÂÂ Ã°ÂÂÂÃ¯Â¸Â Gruppen (`#tab-gruppen`) Ã¢ÂÂ NEU seit v1.21.0

```
Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ
Ã¢ÂÂ  GROUP STANDINGS (ESPN)  #gruppenContent                Ã¢ÂÂ
Ã¢ÂÂ  Gruppe A Ã¢ÂÂ¦ Gruppe L                                    Ã¢ÂÂ
Ã¢ÂÂ  Je Gruppe: Tabelle mit Pos/Team/Sp/S/U/N/Tore/Punkte   Ã¢ÂÂ
Ã¢ÂÂ  Team-Name + Ã°ÂÂÂ <Klassifikationspunkte> des Users       Ã¢ÂÂ
Ã¢ÂÂ  Quali-Ampel (grÃÂ¼n/gelb/rot)                            Ã¢ÂÂ
Ã¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂÃ¢ÂÂ
```

| Kanonischer Name              | Funktion / ID                      | Beschreibung                               |
|-------------------------------|------------------------------------|--------------------------------------------|
| **Gruppen Container**         | `renderGruppen()` / `#gruppenContent` | Alle 12 Gruppen-Tabellen                |
| **Gruppen Render UI**         | `_renderGruppenUI()`               | Interne Render-Funktion fÃÂ¼r Standings-UI   |
| **Group Classification Pts**  | `calcTeamClassificationPoints()`   | Punkte pro Team fÃÂ¼r den User (ESPN-basiert)|
| **Group Class Standings Fetch** | `fetchGrupClassStandings()`      | ESPN-Standings in `_grupClassCache` laden  |

---

## TAB 8 Ã¢ÂÂ Ã¢Â­Â Campeones (`#tab-champions`)

| Kanonischer Name      | Funktion / ID                  | Beschreibung                          |
|-----------------------|--------------------------------|---------------------------------------|
| **Champion Grid**     | `renderChampions()` / `#champGrid` | LÃÂ¤nder-Kacheln mit Tipper-Anzahl  |
| **Scorer Grid**       | `#scorerGrid`                  | TorschÃÂ¼tzen-Cards mit ESPN-Tore       |

---

## TAB 9 Ã¢ÂÂ Ã°ÂÂÂ Statistiken (`#tab-stats`)

| Kanonischer Name          | ID                    | Beschreibung                                    |
|---------------------------|-----------------------|-------------------------------------------------|
| **Overall Accuracy Card** | `#accBars`            | Exact/Diff/Trend/Wrong-Verteilung aller Spieler |
| **Your Accuracy Card**    | `#yourAccBars`        | Eigene Trefferquote                             |
| **Upset Card**            | `#upsetGrid`          | Spieler die gegen Mehrheit lagen und Recht hatten |
| **Contrarian Card**       | `#contrarianContent`  | Top 15 KontrÃÂ¤r-Spieler                          |
| **Group Rank Card**       | `#groupRankChart`     | ÃÂ Score je Porra-Gruppe (Balken)                |
| **Consensus Card**        | `#consensusContent`   | Spiele mit hÃÂ¶chstem Community-Konsens           |
| **Split Card**            | `#splitContent`       | Umstrittenste Spiele (gleichmÃÂ¤ÃÂige Verteilung)  |

---

## TAB 10 Ã¢ÂÂ Ã°ÂÂÂ Suche (`#tab-search`)

| Kanonischer Name      | Funktion / ID            | Beschreibung                       |
|-----------------------|--------------------------|-------------------------------------|
| **Search Input**      | `#searchInput`           | Freitext-Eingabe Spielername        |
| **Player Detail Card**| `doSearch()` / `#searchResults` | Dynamische Detail-Card je Spieler |

---

## TAB 11 Ã¢ÂÂ Ã°ÂÂÂÃ¯Â¸Â Datenbasis (`#tab-database`)

| Kanonischer Name      | Funktion / ID            | Beschreibung                       |
|-----------------------|--------------------------|-------------------------------------|
| **Filter Bar**        | `#dbSearch`, `#dbGroupFilter`, `#dbGameFilter` | Such- und Filter-Leiste |
| **Database Table**    | `renderDatabase()` / `#databaseContent` | Alle 154 Spieler ÃÂ Tipps |

---

## TAB 12 Ã¢ÂÂ Ã°ÂÂÂ Changelog (`#tab-changelog`)

Statisches HTML. Keine Render-Funktion. Karten chronologisch (neueste oben), eine Karte (`.card`) je Version.

---

## Ã°ÂÂÂ MATCH CARD TYPEN (Shared Components)

| Kanonischer Name        | Funktion                      | Eingesetzt in                                     |
|-------------------------|-------------------------------|---------------------------------------------------|
| **Live Match Card**     | `matchCardLive(g, a)`         | Next Match Card (wenn live), Live Games Summary   |
| **FT Match Card**       | `matchCardFinished(g, a, lb)` | Last Result Card                                  |
| **Upcoming Match Card** | `matchCardUpcoming(g)`        | Next Match Card (wenn upcoming)                   |
| **Tip Block**           | `renderGameTipBlock(...)`     | Live Games Summary, Latest/Upcoming Summary, Group, Games Detail |

### Live Match Card Ã¢ÂÂ Elemente
`matchCardLive(g, a)`: Disruptor Badge ÃÂ· Team Logos ÃÂ· Live Score ÃÂ· HZ-Score ÃÂ· Rote Karten ÃÂ· Live-Status ÃÂ· Scorer Events Grid (TV-Style, 2-spaltig) ÃÂ· **My/Community Tip Row** (blau) ÃÂ· Live Punkteverteilung (4 Boxen) ÃÂ· Match Meta

### FT Match Card Ã¢ÂÂ Elemente
`matchCardFinished(g, a, lb)`: Farbgradient (Punkte) ÃÂ· Points Badge ÃÂ· Teams/Score ÃÂ· FT-Pill ÃÂ· My Tip Display + Label (Exakt/Diff/Trend/Falsch) ÃÂ· FT Punkteverteilung ÃÂ· Match Meta

### Upcoming Match Card Ã¢ÂÂ Elemente
`matchCardUpcoming(g)`: Teams ÃÂ· Countdown Pill (`.cd-pill`, Live-Update) ÃÂ· **My/Community Tip Row** (blau) ÃÂ· Match Meta

### Tip Block Ã¢ÂÂ Elemente
`renderGameTipBlock(...)`: Score Label (FT/LIVE/Ã¢ÂÂ) ÃÂ· My/Community Tip Row ÃÂ· Player Tip Cards (`.player-tip-card`, sortiert nach Rang, farbig nach Punkte)