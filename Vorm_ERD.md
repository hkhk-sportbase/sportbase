# ERD juhend

## Mis see on
ERD (Entity-Relationship Diagram) on sinu andmebaasi arhitektuurijoonis. Näitab tabelid, väljad ja seosed.

## Kuidas teha
1. Ava [diagrams.net](https://app.diagrams.net/) → New → vali "Entity Relationship" template
2. Joonista oma Task 02 analüüsi põhjal
3. Salvesta `docs/erd.png`

## Minimaalsed tabelid
- **spordialad** (id, nimi, kirjeldus)
- **ruumid** (id, nimi, mahutavus, varustus)
- **treenerid** (id, nimi, telefon, email)
- **treeningud** (id, spordiala_id, ruum_id, treener_id, algus, lõpp, max_osalejad)
- **kasutajad** (id, nimi, roll, email)
- **broneeringud** (id, treening_id, kasutaja_id, broneeringu_aeg, staatus)

## Seosed
- spordiala 1:N treeningud (üks spordiala, mitu treeningut)
- ruum 1:N treeningud (üks ruum, mitu treeningut)
- treener 1:N treeningud
- treening M:N kasutaja (läbi broneeringud tabeli)

## Näide

```
┌──────────────┐     ┌──────────────┐     ┌──────────────┐
│ spordialad   │     │ treeningud   │     │ ruumid       │
├──────────────┤     ├──────────────┤     ├──────────────┤
│ PK id        │──┐  │ PK id        │  ┌──│ PK id        │
│ nimi         │  └─>│ FK spordiala_id│  │  │ nimi         │
│ kirjeldus    │     │ FK ruum_id   │<─┘  │ mahutavus    │
└──────────────┘     │ FK treener_id│     │ varustus     │
                     │ algus        │     └──────────────┘
┌──────────────┐     │ lõpp         │
│ treenerid    │     │ max_osalejad │     ┌──────────────┐
├──────────────┤     └──────────────┘     │ broneeringud │
│ PK id        │──┐       │              ├──────────────┤
│ nimi         │  └──────>│              │ PK id        │
│ telefon      │          │              │ FK treening_id│
│ email        │          └─────────────>│ FK kasutaja_id│
└──────────────┘                         │ aeg          │
                     ┌──────────────┐    │ staatus      │
                     │ kasutajad    │    └──────────────┘
                     ├──────────────┤         │
                     │ PK id        │<────────┘
                     │ nimi         │
                     │ roll         │
                     │ email        │
                     └──────────────┘
```

*(Päris ERD joonista diagrams.net-is, see on lihtsustatud tekst)*

## Allikad
- [diagrams.net](https://app.diagrams.net/)
- [ERD tutorial](https://www.lucidchart.com/pages/er-diagrams)
- AI prompt: "Selgita mis vahe on 1:N ja M:N seosel andmebaasis, too näide broneerimissüsteemist"
