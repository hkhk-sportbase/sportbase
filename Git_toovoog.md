# Git töövoog — SportBase projekt

## Päeva alustamine

Iga päev alustad uue branchi. Branch nimi = päeva number.

```bash
# Tõmba viimased muudatused
git checkout main
git pull

# Loo uus branch
git checkout -b paev1
```

Järgmistel päevadel: `paev2`, `paev3`, `paev4`, `paev5`.

---

## Commitimine töö käigus

Sa commitid IGA SAMMU JÄRGI, mitte päeva lõpus korraga. See tähendab vähemalt 3-5 committi päeva jooksul.

### Commit sõnumi formaat

```
paevX-taskY: mida tegid
```

### Näide — esmaspäeva commitid

```bash
# Task 1
git add paev1/task1_spordibaasi_analyys.md
git commit -m "paev1-task1: spordibaasi analüüs"
git push origin paev1

# Task 2
git add docs/erd.md paev1/task2_andmemudel.md
git commit -m "paev1-task2: ERD andmemudel"
git push origin paev1

git add docs/erd.md paev1/task2_andmemudel.md
git commit -m "paev1-task2: parandused pärast AI kontrolli"
git push origin paev1

# Task 3
git add paev1/task3_kasutajalood_wireframe.md docs/wireframe*
git commit -m "paev1-task3: kasutajalood ja wireframe"
git push origin paev1

git add paev1/task3_kasutajalood_wireframe.md
git commit -m "paev1-task3: mõtlemise osa"
git push origin paev1
```

### Hea commit sõnum

Hea commit sõnum vastab küsimustele: MIS sa tegid ja KUI PALJU.

```
HEA:
paev1-task1: spordibaasi analüüs, 6 spordiala kirjeldatud
paev1-task2: ERD diagramm, 6 tabelit, kõik seosed määratud
paev2-task1: linux server seadistatud, tulemüür aktiivne
paev2-task2: mysql andmebaas loodud, 25 kirjet sisestatud

HALB:
update
fix
task 1
valmis
asdf
```

Halb commit sõnum = Maria küsib "mida sa tegid?" ja sa ei oska vastata.

---

## Päeva lõpetamine — Pull Request

Päeva lõpus teed Pull Requesti oma branchi pealt main'i.

```bash
# Kontrolli et kõik on push'itud
git status
git push origin paev1
```

Siis GitHubis:
1. Mine oma repo lehele
2. Nuppu "Compare & pull request" (ilmub automaatselt pärast push'i)
3. Pealkiri: `Päev 1 — Analüüs ja planeerimine`
4. Kirjeldus: kopeeri oma refleksiooni kokkuvõte siia
5. "Create pull request"

Maria vaatab PR üle ja:
- Kui kõik OK: merge'ib main'i, saad järgmise päevaga jätkata
- Kui vaja täiendada: kirjutab kommentaari MIS on puudu, sa parandad samas branchis ja push'id uuesti

---

## Järgmise päeva alustamine

```bash
git checkout main
git pull
git checkout -b paev2
```

NB: Sa saad paev2 branchi luua AINULT kui paev1 PR on merge'itud. Kui pole — paranda enne paev1.

---

## Kokkuvõte

| Millal | Mida teed | Käsk |
|---|---|---|
| Hommikul | Loo päeva branch | `git checkout -b paevX` |
| Iga sammu järgi | Commiti ja push'i | `git add` + `git commit -m "..."` + `git push origin paevX` |
| Päeva lõpus | Tee PR | GitHubis "Compare & pull request" |
| Järgmine hommik | Oota kuni PR merge'itud, siis uus branch | `git checkout main` + `git pull` + `git checkout -b paevX` |

Miinimum commitid päeva kohta: 5 (3 taski + vaheetapid + refleksioon).

---

## Kui lähed sassi

```bash
# Vaata mis seis on
git status
git log --oneline -5

# Kui unustasid push'ida
git push origin paevX

# Kui oled vales branchis
git stash
git checkout oige-branch
git stash pop

# Kui midagi läks totaalselt katki
# ÄRA KUSTUTA MIDAGI — küsi Marialt abi
```

---

## Mida Maria näeb

Maria vaatab Classroom dashboardist:
- Mitu committi päeva kohta (miinimum 5)
- Commit ajatemplid (kas tööd kogu päeva või ainult õhtul)
- Commit sõnumid (kas on informatiivsed)
- PR kommentaarid (kas reageerisid tagasisidele)

Kui kõik commitid on ühel päeval (nt reede õhtul): maksimaalne tulemus on "Täienda", olenemata kvaliteedist.
