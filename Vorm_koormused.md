# Koormuse arvutuste vorm

Siin arvutad kui palju süsteem peab kandma — kasutajad, päringud, andmemaht.

---

## Tühi vorm

### 1. Kasutajate arv

| Parameeter | Väärtus | Kuidas arvutasid |
|---|---|---|
| Registreeritud kasutajaid kokku | | |
| Maksimaalselt samaaegseid kasutajaid | | |
| Tüüpiline samaaegne kasutajate arv | | |
| Tipptund | | |

### 2. Andmemaht

| Tabel | Ridade arv (aasta) | Ühe rea suurus (hinnang) | Tabel kokku |
|---|---|---|---|
| | | | |
| **Kokku** | | | |

### 3. Päringute koormus

| Tegevus | Päringuid sekundis (tipptunnil) | Päringu keerukus |
|---|---|---|
| | | |

### 4. Serveri nõuded

| Parameeter | Minimaalne | Soovituslik | Põhjendus |
|---|---|---|---|
| CPU | | | |
| RAM | | | |
| Kettaruum | | | |

---

## Näide — Maria lahendus

### 1. Kasutajate arv

| Parameeter | Väärtus | Kuidas arvutasin |
|---|---|---|
| Registreeritud kasutajaid kokku | ~410 | 400 õpilast + 6 treenerit + 2 admini + 2 varu |
| Maksimaalselt samaaegseid kasutajaid | ~80 | 20% kasutajatest broneerimisel korraga (vahetunni ajal) |
| Tüüpiline samaaegne kasutajate arv | ~15 | Väljaspool tipptundi |
| Tipptund | E kell 10:00-10:15 | Vahetund, nädala algus — broneeritakse nädala treeninguid |

### 2. Andmemaht

| Tabel | Ridade arv (aasta) | Ühe rea suurus | Tabel kokku |
|---|---|---|---|
| spordialad | 10 | ~500 B | 5 KB |
| ruumid | 5 | ~300 B | 1.5 KB |
| treeningud | 10 × 3 × 52 = 1560 | ~200 B | 312 KB |
| kasutajad | 410 | ~500 B | 205 KB |
| broneeringud | 1560 × 12 = 18720 | ~100 B | 1.87 MB |
| **Kokku** | | | **~2.5 MB** |

Andmemaht on väike — isegi 10 aastat andmeid mahub <50 MB.

### 3. Päringute koormus

| Tegevus | Päringuid sekundis (tipptunnil) | Päringu keerukus |
|---|---|---|
| Ajakava vaatamine | ~5/s | SELECT + JOIN (lihtne) |
| Broneerimine | ~2/s | INSERT + SELECT (kontrolli vaba koht) |
| Statistika | ~0.5/s | GROUP BY + JOIN (raskem) |
| Admin haldus | ~0.1/s | CRUD operatsioonid |

Kokku tipptunnil: ~8 päringut sekundis. MySQL saab sellega hõlpsalt hakkama.

### 4. Serveri nõuded

| Parameeter | Minimaalne | Soovituslik | Põhjendus |
|---|---|---|---|
| CPU | 1 tuum | 2 tuuma | MySQL + veebiserver koos |
| RAM | 1 GB | 2 GB | MySQL puhvrid + OS |
| Kettaruum | 10 GB | 20 GB | OS + andmebaas + logid + backupid |

Kooli broneerimiskeskus on väikese koormusega süsteem. Isegi odav VPS (5€/kuu) saab hakkama.

---

## Allikad

- [MySQL Performance Tuning](https://dev.mysql.com/doc/refman/8.0/en/optimization.html) — kui tahad süveneda
- Kalkulaator: rea suurus = veergude andmetüüpide summa (INT = 4 B, VARCHAR(100) = kuni 100 B, DATE = 3 B)
- AI prompt: "Kui palju MySQL päringuid sekundis suudab keskmine server teenindada?"
