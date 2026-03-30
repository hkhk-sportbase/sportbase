# Riistvara kavandi vorm

Kaks osa: (A) dokumenteeri oma praeguse serveri/VM specs, (B) kavanda mis riistvara päris broneerimiskeskus vajaks.

---

## A. Oma serveri/VM specs — tühi vorm

| Parameeter | Väärtus |
|---|---|
| Masina tüüp (füüsiline / VM / konteiner) | |
| OS | |
| CPU | |
| RAM | |
| Kettaruum (kokku / vaba) | |
| Võrguliides | |
| IP aadress | |

Käsud mille abil leiad:
- `uname -a` — OS info
- `lscpu` — CPU
- `free -h` — RAM
- `df -h` — kettaruum
- `ip addr` — võrguliides ja IP

---

## B. Päris süsteemi riistvara kavand — tühi vorm

### Serverid

| Server | Otstarve | CPU | RAM | Ketas | Hind (hinnang) |
|---|---|---|---|---|---|
| | | | | | |

### Võrguseadmed

| Seade | Otstarve | Specs | Hind |
|---|---|---|---|
| | | | |

### Kogu maksumus

| Komponent | Hind |
|---|---|
| | |
| **Kokku** | |

### Alternatiiv: pilv vs oma riistvara

| | Oma server | Pilvetenus (VPS) |
|---|---|---|
| Algkulu | | |
| Kuukulu | | |
| Haldustöö | | |
| Plussid | | |
| Miinused | | |

---

## Näide — Maria lahendus

### A. Oma VM specs

| Parameeter | Väärtus |
|---|---|
| Masina tüüp | VirtualBox VM |
| OS | Ubuntu Server 24.04 LTS |
| CPU | 2 tuuma (host: Intel i5-12400) |
| RAM | 2 GB |
| Kettaruum | 20 GB (vaba: 14 GB) |
| Võrguliides | enp0s3 (NAT) + enp0s8 (Host-only) |
| IP aadress | 192.168.56.101 |

### B. Päris süsteemi riistvara kavand

**Variant 1: Oma server**

| Server | Otstarve | CPU | RAM | Ketas | Hind |
|---|---|---|---|---|---|
| Dell PowerEdge T150 | Veebi + andmebaasiserver | Xeon E-2314 (4C) | 16 GB | 2× 1TB SSD (RAID 1) | ~1200€ |
| Vana desktop | Varuserver + backup | i5 (olemasolev) | 8 GB | 500 GB HDD | 0€ (olemasolev) |

| Seade | Otstarve | Specs | Hind |
|---|---|---|---|
| TP-Link managed switch | Sisevõrk | 8-port Gigabit | ~50€ |
| UPS | Toitekatkestuse kaitse | 600VA | ~80€ |

| Komponent | Hind |
|---|---|
| Põhiserver | 1200€ |
| Varuserver | 0€ |
| Switch | 50€ |
| UPS | 80€ |
| **Kokku** | **~1330€** |

**Variant 2: Pilvetenus**

| | Oma server | Pilvetenus (Hetzner VPS) |
|---|---|---|
| Algkulu | ~1330€ | 0€ |
| Kuukulu | ~20€ (elekter) | ~10€ (CX21: 2 CPU, 4 GB RAM, 40 GB) |
| Haldustöö | Kõik ise (riistvara + tarkvara) | Ainult tarkvara |
| Plussid | Täielik kontroll, andmed majas | Odav alustada, hooldus minimaalne |
| Miinused | Algus kallis, riistvara vananeb | Andmed pilves, kuumaksumus |

Kooli jaoks soovitaksin **oma serverit** — andmed jäävad majja, algkulu tasub ennast 10+ aastaga ära, ja IT-õpilased saavad serverit hooldada praktika raames.

---

## Allikad

- [Hetzner Cloud](https://www.hetzner.com/cloud) — VPS hinnad
- [Dell PowerEdge](https://www.dell.com/et-ee/) — serverite hinnad
- [hind.ee](https://hind.ee/) — Eesti hinnavõrdlus
- AI prompt: "Mis riistvara on vaja veebipõhise broneerimissüsteemi jaoks mis teenindab 400 kasutajat?"
