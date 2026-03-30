# AI kasutamise juhend

AI on tööriist, mitte lahendus. Siin on konkreetsed reeglid millal ja kuidas.

---

## Kus AI AITAB

| Olukord | Näidisprompt | Mida kontrollid |
|---|---|---|
| SQL süntaks | "Mis on MySQL süntaks CREATE TABLE käsule koos FOREIGN KEY-ga?" | Proovi käsk serveris — kas töötab? |
| Linux käsk | "Kuidas seadistada cron job mis käivitub iga päev kell 2 öösel?" | Käivita `crontab -l` — kas on sees? |
| Mõiste selgitus | "Selgita mis on SLA ja mida tähendab 99% uptime aastas" | Arvuta ise: 365 × 24 × 0.01 = ? tundi downtime |
| Dokumendi struktuur | "Mis peaks sisalduma süsteemiarhitektuuri dokumendis?" | Võrdle wiki vormiga — kas kattub? |

## Kus AI EI AITA

| Olukord | Miks | Mida teed selle asemel |
|---|---|---|
| "Seleta ära" küsimused | Need on SINU projekti kohta — AI ei tea miks SA valisid just need tabelid | Kirjuta ise, oma sõnadega |
| HKHK spordibaasi andmed | AI ei tea HKHK tegelikke spordialasid ja ruume | Küsi Kasparilt või vaata kooli kodulehte |
| Riistvara hinnad | AI andmed on aegunud | Vaata hind.ee, amazon.de, Dell/HP konfigurator |
| Sinu serveri seisund | AI ei näe sinu serverit | Käivita käsk ise ja loe tulemust |

---

## Kuidas AI-d kasutada — samm-sammult

1. **Proovi ise kõigepealt** — isegi kui ei tea, proovi. Vigadest õpid.
2. **Küsi konkreetselt** — mitte "tee mulle andmebaas" vaid "mis andmetüüp sobib telefoninumbri hoidmiseks MySQL-is?"
3. **Kontrolli ALATI tulemust** — käivita serveris, vaata kas töötab
4. **Kirjuta ümber oma sõnadega** — kopeerimine ≠ õppimine

---

## Prompti näited tasemel

### Algaja tase — küsi selgitust
```
Mis vahe on CHAR ja VARCHAR andmetüüpidel MySQL-is? 
Millal kasutada kumba?
```

### Keskmine tase — küsi abi konkreetse probleemiga
```
Mul on tabel "treeningud" ja tabel "osalejad". 
Tahan teha päringut mis näitab iga treeningu kohta 
osalejate arvu. Kuidas JOIN ja GROUP BY kasutada?
```

### Kõrgem tase — küsi disainiabi
```
Kavanadan broneerimiskeskuse süsteemiarhitektuuri. 
Mis komponendid peavad olema et tagada 99% kättesaadavus? 
Nimeta komponendid, ära kirjuta mulle dokumenti valmis.
```

---

## ⚠️ Reegel

Kui õpetaja küsib "miks sa selle valisid?" ja sa ei oska vastata — siis sa ei ole seda õppinud, olenemata sellest kas AI kirjutas koodi sinu eest.

"Seleta ära" sektsioonid taskides on just selleks — sa pead oma valikuid põhjendama.
