# Attack-Defense Matrix (MITRE ATT&CK)

Ovaj repozitorij koristi **MITRE ATT&CK** okvir za mapiranje provedenih napada (Red Team) i metoda detekcije (Blue Team). Tablica prikazuje koje su tehnike korištene u kojem scenariju, je li napad uspio te kako je detektiran.

### Legenda statusa
* **Blocked:** Windows Defender ili druga kontrola je zaustavila napad.
* **Success:** Napad je uspješno izvršen na žrtvi.
* **Logged:** Aktivnost je zabilježena u Sysmon ili Event Viewer logovima (uspješna detekcija).
* **Missed:** Aktivnost nije generirala jasan alert ili log.

---

## Matrix Tablica

| ID Tehnike | Taktika (Tactic) | Naziv Tehnike (Technique) | Korišteno u Profilu (Adversary) | Status Napada | Detekcija (Blue Team) | Bilješka o Detekciji |
| :--- | :--- | :--- | :--- | :---: | :---: | :--- |
| **T1082** | Discovery | System Information Discovery | `01_Discovery` | Success | Logged | Sysmon Event ID 1: Detektirano pokretanje `systeminfo` i `ipconfig`. |
| **T1033** | Discovery | System Owner/User Discovery | `01_Discovery` | Success | Logged | Sysmon Event ID 1: Detektirano pokretanje naredbe `whoami`. |
| **T1057** | Discovery | Process Discovery | `01_Discovery` | Success | Logged | Sysmon: Zabilježen pregled procesa (`tasklist`). |
| **T1016** | Discovery | System Network Configuration Discovery | `01_Discovery` | Success | Logged | Sysmon: Mrežne naredbe korelirane s IP adresom Linux servera. |
| **T1548.002** | Privilege Escalation | Bypass User Account Control (UAC) | `02_You_Shall_Not_Bypass` | Success | Logged | Sysmon Event ID 12/13: Sumnjive modifikacije Registry ključeva za *Silent Elevation*. |
| **T1574** | Privilege Escalation | Hijack Execution Flow | `02_You_Shall_Not_Bypass` | Success | Logged | Detektirano učitavanje DLL-a iz neuobičajene putanje. |
| **T1083** | Discovery | File and Directory Discovery | `03_Ransack` | Success | Logged | Sysmon: Masivno izlistavanje direktorija (Documents/Desktop). |
| **T1005** | Collection | Data from Local System | `03_Ransack` | Success | Logged | Sysmon Event ID 11: Kreiranje kopija `.pdf` i `.docx` datoteka. |
| **T1074** | Collection | Data Staged | `03_Ransack` | Success | Logged | Sysmon: Premještanje datoteka u skriveni *staging* folder prije eksfiltracije. |
| **T1113** | Collection | Screen Capture | `04_SuperSpy` | Success | Logged | Sysmon: Proces (agent) kreira slikovne datoteke (screenshotove) na disku. |
| **T1115** | Collection | Clipboard Data | `04_SuperSpy` | Success | Missed | Teško detektirati bez specifičnog monitoringa clipboard API-ja, ali vidljivo u Caldera reportu. |
| **T1041** | Exfiltration | Exfiltration Over C2 Channel | *Svi profili* | Success | Logged | Sysmon Event ID 3: Mrežna konekcija prema C2 serveru (port 8888). |

---

## Zaključak analize

1.  **Efikasnost Defendera:** Blue Team nije detektirao većinu *fileless* aktivnosti ili legitimnih administrativnih alata (PowerShell, CMD) koje Caldera koristi.
2.  **Sysmon Vidljivost:** Iako napadi nisu automatski blokirani, **Sysmon** je uspješno zabilježio telemetriju za 90% aktivnosti.
3.  **Korelacija:** Ključ obrane bio je ručna korelacija vremena (Timestamp) iz Caldere s vremenom zapisa u Sysmonu, čime je potvrđen incident.
