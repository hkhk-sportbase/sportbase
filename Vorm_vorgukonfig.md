# Võrgukonfiguratsiooni vorm

Siin kavandad dokumendina kuidas broneerimiskeskuse võrk töötaks. Sa ei seadista seda päriselt — see on plaan.

---

## Tühi vorm

### 1. Võrgutopoloogia
*(Joonista diagrams.net-is võrgudiagramm. Salvesta `docs/vorgudiagramm.png`)*

### 2. IP-aadresside plaan

| Seade/teenus | IP aadress | Subnet mask | Märkused |
|---|---|---|---|
| | | | |
| | | | |

### 3. Alamvõrgud (subnets)

| Alamvõrk | Aadressivahemik | Otstarve | Seadmete arv |
|---|---|---|---|
| | | | |
| | | | |

### 4. DHCP konfiguratsioon

| Parameeter | Väärtus |
|---|---|
| DHCP server | |
| IP vahemik | |
| Lease time | |
| Default gateway | |
| DNS server | |

### 5. DNS konfiguratsioon

| Nimi | Tüüp | Väärtus | Otstarve |
|---|---|---|---|
| | | | |

### 6. Tulemüüri reeglid

| # | Suund | Port | Protokoll | Lubatud/keelatud | Põhjus |
|---|---|---|---|---|---|
| | | | | | |

### 7. Põhjendus
Miks sa valisid just selle lahenduse? Mis alternatiive kaalusid?

---

## Näide — Maria lahendus

### 1. Võrgutopoloogia

```
[Internet]
     |
[Ruuter/Tulemüür] 192.168.1.1
     |
     |── [Veebiserver] 192.168.1.10
     |── [Andmebaasiserver] 192.168.1.20
     |── [Varuserver] 192.168.1.30
     |
     |── [DHCP vahemik: .100-.200]
         ├── [Treenerite arvutid]
         └── [Admin arvutid]
```

### 2. IP-aadresside plaan

| Seade/teenus | IP aadress | Subnet mask | Märkused |
|---|---|---|---|
| Ruuter (gateway) | 192.168.1.1 | 255.255.255.0 | Default gateway kõigile |
| Veebiserver | 192.168.1.10 | 255.255.255.0 | Staatiline IP |
| Andmebaasiserver | 192.168.1.20 | 255.255.255.0 | Staatiline IP, ainult sisevõrgust ligipääs |
| Varuserver | 192.168.1.30 | 255.255.255.0 | Staatiline IP |
| DNS server | 192.168.1.1 | 255.255.255.0 | Ruuteris |

### 3. Alamvõrgud

| Alamvõrk | Aadressivahemik | Otstarve | Seadmete arv |
|---|---|---|---|
| 192.168.1.0/24 | .1 - .50 | Serverid ja infrastruktuur | 5 |
| 192.168.1.0/24 | .100 - .200 | DHCP klientidele | kuni 100 |

### 4. DHCP konfiguratsioon

| Parameeter | Väärtus |
|---|---|
| DHCP server | 192.168.1.1 (ruuter) |
| IP vahemik | 192.168.1.100 - 192.168.1.200 |
| Lease time | 8h (tööpäev) |
| Default gateway | 192.168.1.1 |
| DNS server | 192.168.1.1, 8.8.8.8 |

### 5. DNS

| Nimi | Tüüp | Väärtus | Otstarve |
|---|---|---|---|
| sportbase.hkhk.local | A | 192.168.1.10 | Broneerimiskeskuse veebileht |
| db.hkhk.local | A | 192.168.1.20 | Andmebaasiserver (ainult sisevõrk) |

### 6. Tulemüüri reeglid

| # | Suund | Port | Protokoll | Lubatud/keelatud | Põhjus |
|---|---|---|---|---|---|
| 1 | Sisse | 443 | TCP | Lubatud | HTTPS veebiliides |
| 2 | Sisse | 80 | TCP | Lubatud → redirect 443 | HTTP → HTTPS suunamine |
| 3 | Sisse | 22 | TCP | Lubatud (ainult admin IP) | SSH halduseks |
| 4 | Sisse | 3306 | TCP | Keelatud väljastpoolt | MySQL ainult sisevõrgus |
| 5 | Sisse | muu | * | Keelatud | Kõik muu blokitud |

### 7. Põhjendus

Valisin ühe /24 alamvõrgu, sest HKHK spordibaasis pole rohkem kui 100 samaaegset kasutajat. Serverid saavad staatilise IP (.10, .20, .30), et DNS ja tulemüürireeglid ei muutuks. MySQL port (3306) on väljastpoolt kinni, sest andmebaasile pääseb ligi ainult veebiserver sisevõrgust.

---

## Allikad

- [diagrams.net — Network Diagram templates](https://app.diagrams.net/) — vali "Network" template
- [Subnet Calculator](https://www.subnet-calculator.com/) — alamvõrkude arvutamiseks
- AI prompt: "Selgita mis vahe on staatilisel ja dünaamilise IP aadressil ja millal kumba kasutada"
