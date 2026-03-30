# Wireframe juhend

## Mis see on
Wireframe on broneerimiskeskuse kasutajaliidese plaan — kus on navigatsioon, nupud, tabelid, vormid. Mitte ilus disain, vaid struktuur.

Sa ei ehita veebilehte — aga kavandad milline see välja näeks.

## Kuidas teha
- **Figma** (tasuta) — kui tahad detailsemat
- **diagrams.net** — kiire ja lihtne
- **Paber + foto** — samuti OK, pildista ja lisa reposse

## Minimaalsed vaated

| Vaade | Mida kuvab | Kes kasutab |
|---|---|---|
| Avaleht | Spordibaasi ülevaade, kiirlingid | Kõik |
| Ajakava | Treeningute kalender/tabel, filtreerimine spordiala/ruumi järgi | Kõik |
| Broneerimine | Spordiala valik → vaba aja valik → kinnitus | Õpilane |
| Minu broneeringud | Kasutaja broneeringute nimekiri, tühistamine | Õpilane |
| Treenerite vaade | Minu treeningud, osalejate nimekiri, kohaloleku märkimine | Treener |
| Admin paneel | Spordialade/ruumide haldus, statistika | Admin |

## Näide — Maria wireframe (tekst)

```
┌─────────────────────────────────────────┐
│  HKHK SportBase    [Ajakava] [Broneeri] │
│                    [Minu] [Logi välja]  │
├─────────────────────────────────────────┤
│                                         │
│  Tere, [Kasutajanimi]!                  │
│                                         │
│  ┌─────────────┐  ┌─────────────┐      │
│  │ Järgmine     │  │ Minu        │      │
│  │ treening:    │  │ broneeringud│      │
│  │ Korvpall     │  │ 3 aktiivset │      │
│  │ T 16:00      │  │ [Vaata →]   │      │
│  └─────────────┘  └─────────────┘      │
│                                         │
│  Populaarsed spordialad:               │
│  [Korvpall] [Ujumine] [Jõusaal]       │
│                                         │
└─────────────────────────────────────────┘
```

Salvesta `docs/wireframe.png` (või mitu pilti eri vaadete jaoks).

## Allikad
- [Figma](https://www.figma.com/) — tasuta konto
- [diagrams.net — Mockup shapes](https://app.diagrams.net/)
- AI prompt: "Mis elemendid peaks olema spordi broneerimissüsteemi avalehel? Nimeta, ära joonista"
