# Õpilase juhend — SportBase

## Mis see projekt on?

HKHK tahab ehitada spordibaasi broneerimiskeskuse. Sina:
1. **Ehitad päriselt:** Linux server + MySQL andmebaas + backup süsteem
2. **Kavandad dokumendina:** kogu süsteemidisain — arhitektuur, võrk, riistvara, UI, SLA — nagu päris pakkumine tellijale

---

## Kuidas töö käib

### 5 päeva, 3 taski päeva kohta

Iga hommik ilmuvad uue päeva failid (Maria release'b). Sul on 3 taski mis tuleb sel päeval ära teha ja commitida.

Iga taski struktuur:

| Osa | Mida teed | Aeg |
|---|---|---|
| Loe | Materjal, juhend, wiki vorm | ~10 min |
| Tee | Praktiline ülesanne või dokumendi täitmine | ~20 min |
| Mõtle | Vasta küsimustele OMA projekti kohta | ~10 min |

### Päeva lõpus

- Push oma branch ja tee PR (paevX -> main)
- Kirjuta refleksioon Discussions'isse (mis sai selgeks, mis jäi segaseks, mida õppisin)

### Vormid wikis

Iga dokumendi jaoks on wikis **tühi vorm** (mida täita) ja **näide** (Maria lahendus). Sa ei pea ise välja mõtlema mis dokument peaks sisaldama — vorm ütleb ette.

---

## Git töövoog

Iga päev:
1. Loo branch: `git checkout -b paev1` (või paev2, paev3 jne)
2. Tee 3 taski, commiti iga taski järel
3. Push ja tee PR

Commit sõnumid:
```
paev1-task1: spordibaasi analüüs
paev1-task2: ERD andmemudel
paev1-task3: kasutajalood ja wireframe
```

Loe rohkem: [Git töövoog](Git_toovoog)

---

## Hindamine

Iga aine: **A** (arvestatud) / **Täienda** / **MA** (mittearvestatud)

- **A** = checklist täidetud, "Mõtle" vastatud, tulemus sisukas
- **Täienda** = põhiasi olemas aga midagi puudu. Õpetaja ütleb mis parandada
- **MA** = tulemus puudub või vale

### Parandamine

Kui said "Täienda":
- Parandad järgmine päev = 80% väärtusest
- Parandad ülejärgmine päev = 50%
- 3+ päeva hiljem = võid esitada, 0%

### Mis loeb

- Commit ajalugu — kas tegid iga päev või kõik reedel
- Checklist iga taskis — kas kõik on täidetud
- "Mõtle" vastused — kas mõtlesid ise, mitte kopeerisid
- Discussions refleksioonid — kas kirjutasid iga päev
- AI kasutamine — kas tegid AI kontrolli ja parandasid vead

Detailsed kriteeriumid: [Rubriigid](Rubriigid)

---

## Kaustastruktuur

```
├── README.md
├── paev1/
│   ├── task1_spordibaasi_analyys.md
│   ├── task2_andmemudel.md
│   └── task3_kasutajalood_wireframe.md
├── paev2/
│   ├── task1_linux_server.md
│   ├── task2_mysql_andmebaas.md
│   └── task3_riistvara.md
├── paev3/
│   ├── task1_arhitektuur_vork.md
│   ├── task2_sla_koormused.md
│   └── task3_backup_plaan.md
├── paev4/
│   ├── task1_backup_praktiline.md
│   ├── task2_dok_eesti.md
│   └── task3_disaini_kokkuvote.md
├── paev5/
│   ├── task1_dok_inglise.md
│   ├── task2_testimine.md
│   └── task3_esitlus.md
├── docs/
│   ├── erd.md
│   ├── wireframe.png
│   ├── arhitektuur.png
│   ├── vorgudiagramm.png
│   ├── kasutajajuhend_est.md
│   ├── tehniline_kirjeldus_est.md
│   ├── readme_eng.md
│   └── technical_doc_eng.md
└── sql/
    ├── create.sql
    ├── insert.sql
    ├── queries.sql
    └── backup.sh
```

---

## AI kasutamine

Loe [AI kasutamise juhend](AI_juhend). Lühidalt:
- AI aitab: SQL süntaks, Linux käsud, mõistete selgitus
- AI EI AITA: "Mõtle" küsimused (sinu projekti kohta), HKHK andmed, riistvara hinnad
- Alati kontrolli tulemust ise
- Kopeeri prompt ja AI vastus taski faili (AI kontrolli sektsioonides)

---

## Kui jääd kinni

1. Samm-sammult juhend taskis (ava details)
2. Wiki vormid ja näited
3. [Allikad](Allikad) — konkreetsed lingid
4. Discussions — kirjuta mida proovisid
5. Küsi Marialt
