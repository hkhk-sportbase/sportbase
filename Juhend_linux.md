# Juhend: Linux serveri paigaldamine ja seadistamine

## Mis see on

Server on arvuti mis tootab 24/7 ja teenindab teisi arvuteid. Sinu andmebaas elab serveris. Sa paigaldad Ubuntu Serveri virtuaalmasinasse (VM), lood kasutajad ja seadistad pohiturvalisuse.

## Miks see oluline on

Andmebaas vajab kohta kus elada. Kui server on seadistamata voi ebaturvaline, siis:
- keegi voib sinu andmed ara kustutada
- server kukub ja keegi ei tea miks
- keegi pAaseb ligi kes ei peaks

## Pohimoisted

### Virtuaalmasin (VM)

VM on arvuti arvuti sees. Sa kasutad VirtualBoxi mis loob "virtuaalse arvuti" sinu parisarvuti sisse. Seal jookseb Ubuntu Server eraldi opwratsioonisusteem.

### SSH (Secure Shell)

SSH on viis kuidas saad serveriga uhendust voeta terminali kaudu. Sa kirjutad kasud oma arvutis aga need kaivituvad serveris.

```
ssh kasutajanimi@serveri-ip-aadress
```

### Root kasutaja

Root on serveri "jumala" kasutaja — saab koike teha. Igapaevaseks toooks EI KASUTA root kasutajat, sest uks vale kask voib kogu serveri ara rikkuda. Sellepaerast lood eraldi kasutaja.

### Tulemuur (firewall)

Tulemuur otsustab mis yhendused paasevad serverisse ja mis mitte. Sa lubad ainult need pordid mida vaja (SSH ja MySQL), koik muu on kinni.

## Sammud

### 1. VirtualBoxi paigaldamine

Kui sul pole VirtualBoxi:
- Laadi alla: https://www.virtualbox.org/wiki/Downloads
- Paigalda oma opwratsioonisuesteemile (Windows/Mac/Linux)

### 2. Ubuntu Serveri allalaadimine

Laadi alla Ubuntu Server 24.04 LTS ISO:
- https://ubuntu.com/download/server
- Vali "Manual installation" -> "Download Ubuntu Server"

### 3. VM loomine VirtualBoxis

1. Ava VirtualBox -> "New"
2. Name: sportbase-server
3. Type: Linux, Version: Ubuntu 64-bit
4. RAM: 2048 MB (2 GB)
5. Hard disk: Create a virtual hard disk -> VDI -> Dynamically allocated -> 20 GB
6. "Create"

Enne kaivitamist:
1. Settings -> Storage -> Controller: IDE -> Lisa Ubuntu ISO
2. Settings -> Network -> Adapter 1: NAT (internet jaoks)
3. Settings -> Network -> Adapter 2: Host-only Adapter (et sa saaksid SSH-ga yhenduda)

### 4. Ubuntu paigaldamine

1. Kaivita VM
2. Vali "Install Ubuntu Server"
3. Keel: English
4. Keyboard: Estonian
5. Network: vaikimisi (DHCP)
6. Storage: Use an Entire Disk
7. Your name: sportbase-admin (voi oma valik)
8. Server name: sportbase
9. Username: sportbase-admin
10. Password: kirjuta yles! Pead seda meeles pidama.
11. Install OpenSSH server: JAH (linnuke peale)
12. Oota kuni paigaldab -> Reboot

### 5. Esimene sisselogimine

Parast taaskaivitust logi sisse oma kasutajaga.

Uuenda susteem:
```
sudo apt update
sudo apt upgrade -y
```

### 6. Eraldi kasutaja loomine

```
sudo adduser sportbase
sudo usermod -aG sudo sportbase
```

Nüüd on sul kaks kasutajat:
- sportbase-admin (paigaldamise kasutaja)
- sportbase (igapAevane kasutaja, sudp oigustega)

### 7. Root SSH keelamine

```
sudo nano /etc/ssh/sshd_config
```

Leia rida mis sisaldab "PermitRootLogin" ja muuda:
```
PermitRootLogin no
```

Salvesta: Ctrl+O, Enter, Ctrl+X

Taaskaivita SSH teenus:
```
sudo systemctl restart sshd
```

### 8. Tulemiuuri seadistamine

```
sudo ufw allow 22/tcp    # SSH
sudo ufw allow 3306/tcp  # MySQL
sudo ufw enable
```

Tulemuur kysib kinnitust — kirjuta "y".

Kontrolli:
```
sudo ufw status
```

Peaks naitama:
```
22/tcp    ALLOW   Anywhere
3306/tcp  ALLOW   Anywhere
```

### 9. SSH yhenduse testimine

Ava oma parisarvutis terminal (mitte VM-is) ja proovi:

```
ssh sportbase@[serveri-ip]
```

IP aadressi saad teada VM-is:
```
ip addr show
```

Vaata "enp0s8" (Host-only adapter) aadressi.

## Levinud vead

1. SSH ei yhenda — kontrolli kas VM-i Network Adapter 2 on "Host-only"
2. "Permission denied" — kontrolli kas kasutajanimi ja parool on oiged
3. ufw lukustab sind valja — kui keelad pordi 22, ei saa enam SSH-ga ligi. Paranda VM-i konsoolis
4. ISO jaab kinni — Settings -> Storage -> eemalda ISO parast paigaldamist

## Kontroll-kusimused

- Kas sa saad SSH-ga sisse oma kasutajaga?
- Kas root SSH on keelatud? (proovi: ssh root@ip — peab keelduma)
- Kas tulemuur on aktiivne ja naitab ainult porte 22 ja 3306?

## Allikad

- Ubuntu Server docs: https://ubuntu.com/server/docs
- DigitalOcean juhend: https://www.digitalocean.com/community/tutorials/initial-server-setup-with-ubuntu
- VirtualBox docs: https://www.virtualbox.org/manual/
- AI prompt: "Kuidas seadistada Ubuntu serverit esimest korda? Mis sammud on vajalikud turvalisuse jaoks?"
