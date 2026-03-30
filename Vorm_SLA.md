# SLA ja kättesaadavuse vorm

SLA (Service Level Agreement) määrab kui töökindel süsteem peab olema. Siin arvutad mis 99% kättesaadavus tähendab ja kuidas seda tagada.

---

## Tühi vorm

### 1. Kättesaadavuse eesmärk

| Parameeter | Väärtus |
|---|---|
| Kättesaadavuse % | |
| Lubatud downtime aastas | |
| Lubatud downtime kuus | |
| Lubatud downtime nädalas | |

### 2. Mis võib süsteemi maha võtta?

| Oht | Tõenäosus (madal/keskmine/kõrge) | Mõju | Kuidas vältida | Kuidas taastada |
|---|---|---|---|---|
| | | | | |

### 3. Taastamisplaan

| Parameeter | Väärtus | Selgitus |
|---|---|---|
| RTO (Recovery Time Objective) | | Kui kiiresti peab süsteem taastuma |
| RPO (Recovery Point Objective) | | Kui palju andmeid võib kaotsi minna |
| Backup sagedus | | |
| Backup asukoht | | |

### 4. Monitooring
Kuidas sa tead kas süsteem töötab?

---

## Näide — Maria lahendus

### 1. Kättesaadavuse eesmärk

| Parameeter | Väärtus |
|---|---|
| Kättesaadavuse % | 99% |
| Lubatud downtime aastas | 365 × 24 × 0.01 = **87.6 tundi** |
| Lubatud downtime kuus | ~7.3 tundi |
| Lubatud downtime nädalas | ~1.7 tundi |

99% tähendab et süsteem võib olla maas kuni 1.7 tundi nädalas. Koolisüsteemi jaoks on see piisav — kriitilised on tööpäeva tunnid (8-17), nädalavahetusel on downtime aktsepteeritav.

### 2. Mis võib süsteemi maha võtta?

| Oht | Tõenäosus | Mõju | Kuidas vältida | Kuidas taastada |
|---|---|---|---|---|
| Serveri riistvara rike | Madal | Kõrge — kõik maas | Varuserver, regulaarne riistvara kontroll | Backup → varuserverisse, RTO: 2h |
| Andmebaasi korruptsioon | Madal | Kõrge — andmed kadunud | Automaatne backup, TRANSACTION kasutamine | Viimane backup taastamine, RPO: 24h |
| Võrgukatkestus | Keskmine | Kõrge — keegi ei pääse ligi | Varuühendus (4G modem) | Oodata, kuni ISP parandab |
| Kettaruum täis | Keskmine | Keskmine — uued broneeringud ei salvesta | Monitooring, automaatne teavitus 80% juures | Vana logide kustutamine, ketta laiendamine |
| Tarkvara uuenduse viga | Madal | Keskmine — mõni funktsioon katki | Testida enne production'it | Rollback eelmisele versioonile |

### 3. Taastamisplaan

| Parameeter | Väärtus | Selgitus |
|---|---|---|
| RTO | 2 tundi | Kui server kukub, peab 2h jooksul taastuma |
| RPO | 24 tundi | Viimase 24h andmed võivad kaotsi minna (öine backup) |
| Backup sagedus | Iga öö kell 02:00 | cron + mysqldump |
| Backup asukoht | Varuserver (192.168.1.30) + pilv (valikuline) | Kohalik + kaugkoopia |

### 4. Monitooring

- **Uptime monitoring:** UptimeRobot (tasuta) — kontrollib iga 5 min kas veebileht vastab
- **Kettaruum:** cron skript, mis saadab e-maili kui kettakasutus > 80%
- **Andmebaas:** MySQL slow query log — näitab aeglaseid päringuid

---

## Arvutamise abimees

| SLA % | Downtime aastas | Downtime kuus | Downtime nädalas |
|---|---|---|---|
| 99% | 87.6h | 7.3h | 1.7h |
| 99.5% | 43.8h | 3.65h | 50 min |
| 99.9% | 8.76h | 43.8 min | 10 min |
| 99.99% | 52.6 min | 4.38 min | 1 min |

## Allikad

- [Uptime Calculator](https://uptime.is/) — SLA % → downtime arvutamine
- [UptimeRobot](https://uptimerobot.com/) — tasuta monitooring
- AI prompt: "Mis vahe on RTO ja RPO-l? Selgita koolisüsteemi näitel"
