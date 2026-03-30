# Backup plaani vorm

Kaks osa: (A) praktiline backup skript mille sa päriselt teed, (B) backup strateegia dokumendina süsteemidisaini jaoks.

---

## A. Praktiline — mysqldump + cron

### Backup skript

```bash
#!/bin/bash
# backup.sh — SportBase andmebaasi backup
DATUM=$(date +%Y%m%d_%H%M%S)
mysqldump -u [kasutaja] -p[parool] sportbase > /home/backup/sportbase_$DATUM.sql
# Kustuta vanemad kui 7 päeva
find /home/backup -name "*.sql" -mtime +7 -delete
```

### Cron seadistus
```
# crontab -e
0 2 * * * /home/backup/backup.sh
```
See käivitab backup skripti iga öö kell 02:00.

### Taastamise test
```bash
# Loo test-andmebaas
mysql -u root -p -e "CREATE DATABASE sportbase_test;"
# Taasta backup
mysql -u root -p sportbase_test < /home/backup/sportbase_[kuupäev].sql
# Kontrolli
mysql -u root -p sportbase_test -e "SELECT COUNT(*) FROM treeningud;"
# Kustuta test-andmebaas
mysql -u root -p -e "DROP DATABASE sportbase_test;"
```

---

## B. Backup strateegia dokumendina — tühi vorm

| Parameeter | Väärtus | Põhjendus |
|---|---|---|
| Backup tüüp | | (full / incremental / differential) |
| Sagedus | | |
| Kellaaeg | | |
| Hoiukoht | | |
| Säilitusaeg | | |
| Taastamise aeg (RTO) | | |
| Andmekao piir (RPO) | | |
| Kes vastutab | | |
| Kuidas testitakse | | |

---

## Näide — Maria lahendus

| Parameeter | Väärtus | Põhjendus |
|---|---|---|
| Backup tüüp | Full (mysqldump) | Andmemaht väike (<50 MB), full on lihtsaim |
| Sagedus | Iga öö | Tööpäeva andmed salvestatakse öösiti |
| Kellaaeg | 02:00 | Kasutajaid pole, server vaba |
| Hoiukoht | Varuserver (192.168.1.30) + USB ketas (nädalane) | Kohalik kiire taastamine + füüsiline koopia |
| Säilitusaeg | 7 päeva serveris, 30 päeva USB-l | Piisav vigade avastamiseks |
| RTO | 2 tundi | Varuserverisse ümberlülitus |
| RPO | 24 tundi | Viimase öö backup |
| Kes vastutab | IT-admin (+ IT-õpilane praktikandina) | |
| Kuidas testitakse | Kord kuus: taasta backup → kontrolli andmed → kustuta test-db | |

---

## Allikad
- [mysqldump dokumentatsioon](https://dev.mysql.com/doc/refman/8.0/en/mysqldump.html)
- [crontab.guru](https://crontab.guru/) — cron süntaksi kontrollija
- AI prompt: "Selgita mis vahe on full, incremental ja differential backupil"
