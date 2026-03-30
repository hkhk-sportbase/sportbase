# Dokumentatsiooni vormid

## Eesti keel — kasutajajuhend

### Tühi vorm

```markdown
# [Süsteemi nimi] — Kasutajajuhend

## 1. Mis see süsteem on
*(1-2 lauset)*

## 2. Kuidas sisse logida
*(sammhaaval, ekraanipiltidega)*

## 3. Kasutamine

### Ajakava vaatamine
*(kuidas leida treeninguid)*

### Broneerimise tegemine
*(samm-sammult)*

### Broneeringu tühistamine
*(kuidas ja millal saab)*

## 4. Korduma kippuvad küsimused
*(3-5 küsimust vastustega)*

## 5. Abi saamine
*(kuhu pöörduda probleemide korral)*
```

### Näide — Maria kasutajajuhend (lühendatud)

# HKHK SportBase — Kasutajajuhend

## 1. Mis see süsteem on
HKHK SportBase on broneerimiskeskus, kus saad registreeruda sporditreeningutele ja vaadata ajakava.

## 2. Kuidas sisse logida
1. Ava brauser → mine aadressile `sportbase.hkhk.local`
2. Sisesta oma HKHK e-maili aadress
3. Sisesta parool (esimesel korral: õpilasnumber)
4. Vajuta "Logi sisse"

## 3. Broneerimise tegemine
1. Kliki menüüs "Ajakava"
2. Vali spordiala (nt "Korvpall")
3. Vali sobiv aeg → kliki "Broneeri"
4. Ekraanile ilmub kinnitus: "Broneering tehtud!"

Kui treening on täis, näed teadet "Kohad on täis" ja saad valida teise aja.

---

## Eesti keel — tehniline kirjeldus

### Tühi vorm

```markdown
# [Süsteemi nimi] — Tehniline kirjeldus

## 1. Süsteemi ülevaade
*(mis süsteem, kellele, mis eesmärk)*

## 2. Arhitektuur
*(komponendid, kuidas suhtlevad — viita arhitektuuriskeemile)*

## 3. Andmebaas
*(tabelid, seosed — viita ERD-le)*

## 4. Server
*(OS, konfiguratsioon, turvalisus)*

## 5. Võrk
*(IP, DNS, tulemüür — viita võrgudiagrammile)*

## 6. Backup
*(strateegia, sagedus, taastamine)*

## 7. Teadaolevad piirangud
*(mis ei tööta, mis vajab edasiarendust)*
```

---

## Inglise keel — README

### Tühi vorm

```markdown
# [System Name]

## Overview
*(What the system does, who it's for)*

## Architecture
*(Components, how they interact — link to diagram)*

## Database
*(Tables, relationships — link to ERD)*

## Installation
*(How to set up the system from scratch)*

## Configuration
*(Server, network, database settings)*

## Backup & Recovery
*(Strategy, schedule, how to restore)*

## Known Limitations
*(What doesn't work yet)*
```

### Näide — Maria README (lühendatud)

# HKHK SportBase — Booking System

## Overview
SportBase is a booking system for HKHK sports facility. Students and staff can book training sessions, view schedules, and manage reservations. The system serves approximately 400 users.

## Architecture
The system consists of a web server (Apache), database server (MySQL), and backup server. See `docs/architecture.png` for the full diagram.

## Database
6 tables: sports, rooms, trainers, sessions, users, bookings. See `docs/erd.png` for the entity-relationship diagram.

---

## Allikad
- [Technical Writing Guide](https://developers.google.com/tech-writing) — Google'i tehniline kirjutamise juhend
- AI prompt EE: "Kontrolli minu teksti grammatikat ja stiili. Ära muuda sisu, ainult keelt."
- AI prompt EN: "Check my English text for grammar. Keep the technical terms. Don't change the content."
