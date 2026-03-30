# Süsteemiarhitektuuri vorm

Siin kavandad kuidas HKHK broneerimiskeskus tervikuna töötaks. See on "pakkumine tellijale" — mida on vaja, et kogu kool saaks süsteemi kasutada.

---

## Tühi vorm

### 1. Süsteemi ülevaade
- Mis süsteem on ja mida teeb: *(kirjelda 2-3 lausega)*
- Kes kasutavad: *(rollid ja arv)*
- Mis on peamine eesmärk: *(1 lause)*

### 2. Komponendid

| Komponent | Mis see on | Mida teeb | Tehnoloogia |
|---|---|---|---|
| | | | |
| | | | |
| | | | |

### 3. Arhitektuuriskeem
*(Joonista diagrams.net-is — näita kuidas komponendid omavahel suhtlevad. Salvesta `docs/arhitektuur.png`)*

### 4. Andmevoog
Kirjelda kuidas andmed liiguvad läbi süsteemi:
- Kasutaja teeb broneeringu → ...
- Treener vaatab osalejaid → ...

### 5. Riskid ja nõrkused
- Mis võib katki minna?
- Mis on single point of failure?

---

## Näide — Maria lahendus

### 1. Süsteemi ülevaade
HKHK spordibaasi broneerimiskeskus on veebipõhine süsteem, kus õpilased ja töötajad saavad broneerida treeningruume ja registreeruda spordialadele. Süsteemi kasutab ~400 õpilast, 6 treenerit ja 2 admini. Peamine eesmärk: kogu spordibaasi haldus ühes kohas, ilma paberite ja e-kirjadeta.

### 2. Komponendid

| Komponent | Mis see on | Mida teeb | Tehnoloogia |
|---|---|---|---|
| Veebiserver | Teenindab kasutajate päringuid | Kuvab veebilehti, suunab päringuid andmebaasi | Apache/Nginx, Linux |
| Andmebaasiserver | Hoiab kõiki andmeid | Spordialad, treeningud, broneeringud, kasutajad | MySQL, Linux |
| Varuserver | Hoiab andmete koopiaid | Automaatne backup iga öö, taastamine vajadusel | MySQL dump, cron |
| Veebirakendus | Kasutajaliides brauseris | Broneerimisleht, ajakava, admin paneel | HTML/CSS/PHP (või muu) |
| Monitooring | Jälgib süsteemi tervist | Teavitab kui server maas, kettaruum täis jne | Uptime monitoring |

### 3. Arhitektuuriskeem

```
[Kasutaja brauser]
        |
        | HTTPS (port 443)
        v
[Tulemüür / Load balancer]
        |
        v
[Veebiserver (Apache)]  ──────  [Andmebaasiserver (MySQL)]
        |                               |
        v                               v
[Failisüsteem]                  [Varuserver (backup)]
```

*(Päris joonis diagrams.net-is, see on lihtsustatud tekst)*

### 4. Andmevoog

**Broneeringu tegemine:**
1. Õpilane avab broneerimislehe brauseris
2. Veebiserver kuvab vabad ajad (päring andmebaasist)
3. Õpilane valib aja ja spordiala → klikib "Broneeri"
4. Veebiserver saadab INSERT päringu andmebaasi
5. Andmebaas kontrollib kas koht on vaba (max osalejad)
6. Kui jah → salvestab, kuvab kinnituse
7. Kui ei → kuvab veateate "Treening on täis"

**Treener vaatab osalejaid:**
1. Treener logib sisse
2. Veebiserver kuvab tema treeningute nimekirja (SELECT + WHERE treener_id)
3. Treener valib treeningu → näeb osalejate nimekirja (JOIN)

### 5. Riskid ja nõrkused
- **Single point of failure:** kui andmebaasiserver kukub, ei tööta mitte midagi → lahendus: varuserver + automaatne backup
- **Samaaegne broneerimine:** kaks õpilast broneerivad viimast kohta samal ajal → lahendus: andmebaasi TRANSACTION
- **Turvalisus:** SQL injection kui sisendeid ei valideerita → lahendus: prepared statements

---

## Allikad

- [diagrams.net](https://app.diagrams.net/) — arhitektuuriskeemide joonistamine
- [AWS Architecture Icons](https://aws.amazon.com/architecture/icons/) — ikoonid skeemidele (inspiratsioon)
- AI prompt: "Nimeta veebipõhise broneerimissüsteemi peamised komponendid ja nende rollid"
