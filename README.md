# M117_Netzwerk
---
# Ethernetverkabelung – Tag 1 (13. Mai)

## 🎯 Lernziele
- Unterschied zwischen Bit/Byte, SI- und IEC-Präfixen (k, M, G, T vs. Ki, Mi, Gi, Ti)
- Netzwerktopologien: Bus, Baum (Stern), Mesh
- Alte vs. neue Netzwerktechnologien: Yellow-Coaxial vs. Twisted-Pair-Kabel
- Materialvergleich: Kupferlitze, Kupferdraht, Glasfaser
- Störungsabwehr: Schirmung, Twisted-Pair, S/FTP
- Kabelkategorien: z. B. CAT5e, CAT6, CAT7
- Ethernet-Medientypen: z. B. 1000Base-T, 1000Base-SX
- Unterschied: logisches Layout vs. Verkabelungsplan
- Netzwerkgeräte: Switch, Router, Bridge, Medienkonverter

## 📐 Theorie

### SI- und IEC-Präfixe
- **SI (Dezimal)**: k = 10³, M = 10⁶, G = 10⁹, T = 10¹²
- **IEC (Binär)**: Ki = 2¹⁰, Mi = 2²⁰, Gi = 2³⁰, Ti = 2⁴⁰

### Historie & Medientypen
- Früher: Yellow Cable (Koaxial, Bus)
- Heute: Twisted-Pair, Stern-/Baumtopologie
- Medientypen: z. B. **1000Base-T (Kupfer)**, **1000Base-SX (Glas)**

### Materialwahl
- **Litze (flexibel)**: für Patchkabel
- **Draht (starr)**: für permanente Gebäudeverkabelung (UGV)
- **Glasfaser**: hohe Datenraten, störungsresistent, aber empfindlich

### Kabelschirmung
- S/FTP = Geflechtschirm + Paarweise Folienschirmung
- STP, UTP, S/UTP etc. je nach Schirmungstyp

### Kabelkategorien
- **CAT5e**: min. für 1000Base-T
- **CAT6/CAT7**: höhere Frequenzen & Zukunftssicherheit

## 💡 Praxis: WG „La familia“

### Szenario
- Mehrere WG-Zimmer mit je einem PC pro Person
- Gemeinsame PCs in Gemeinschaftsraum, Bastelraum, Mansardenzimmer
- Verkabelung über Switches
- Verbindung ins Internet via Swisscom-ADSL

### Aufgaben
1:
[Aufgabe 1](./Aufgaben/Tag1/Aufgabe1.md)
<br>
2:
[Aufgabe 2](./Aufgaben/Tag1/Aufgabe2.md)
<br>
3:
[Aufgabe 3](./Aufgaben/Tag1/Aufgabe3.md)
<br>

## 🔌 Geräte zur Verbindung
- **Switch (L2)**: Verbindet Hosts im selben Netz
- **Router**: Verbindet Netzwerke, auch ins Internet
- **Bridge / Repeater / Medienkonverter**: Spezialfälle

> Merksatz: „UGV = Draht, Patch = Litze“


[Theorie Tag1](./Pdfs/Tag1.pdf)

---

# Netzwerkadressierung – Tag 2 (20. Mai)

## 🎯 Lernziele
- CSMA/CD – Zugriffsverfahren in Ethernet-Netzen
- Netzwerkparameter: Hostname, MAC-Adresse, IPv4-Adresse, Subnetzmaske
- Subnetting: Netz-ID, Host-ID, Netzwerkadresse, Broadcastadresse, Loopbackadresse
- Dynamische IP-Vergabe: DHCP, APIPA
- Öffentliche vs. private IPv4-Adressen
- Windows-Kommandos: `arp`, `ping`, `ipconfig`, `ncpa.cpl`, `sysdm.cpl`


## 🔁 CSMA/CD (Carrier Sense Multiple Access / Collision Detection)
- Zugriffsmethode in Ethernet (IEEE 802.3)
- Geräte „hören“, ob Leitung frei ist
- Bei Kollision: Senden abbrechen, Zufallszeit warten, erneut senden


## 🧾 Netzwerkparameter

| Parameter       | Beschreibung |
|----------------|--------------|
| **Hostname**   | Menschlich lesbarer Name, z. B. `Eiger`, `CAU-IT-511-01` |
| **MAC-Adresse**| Eindeutige, unveränderbare physische Adresse (48 Bit) |
| **IPv4-Adresse** | Logisch, änderbar, 32 Bit, z. B. `10.0.0.83` |
| **Subnetzmaske**| Teilt IP in Netz-ID und Host-ID, z. B. `/24` = `255.255.255.0` |


## 🧮 Subnetting & Adressen

### Wichtige Begriffe:
- **Netz-ID**: Teil der IP, der das Netzwerk beschreibt
- **Host-ID**: Teil der IP, der das Gerät beschreibt
- **Netzwerkadresse**: alle Host-Bits = 0
- **Broadcastadresse**: alle Host-Bits = 1
- **Loopback**: `127.0.0.1` = eigener Rechner
- **APIPA (Zeroconf)**: `169.254.x.x`, wenn kein DHCP verfügbar

### Gängige Subnetzmasken (CIDR):
- `/8` → 255.0.0.0 → 16'777'214 Hosts
- `/16` → 255.255.0.0 → 65'534 Hosts
- `/24` → 255.255.255.0 → 254 Hosts


## 🔐 Private vs. öffentliche IP-Adressen

### Private IPv4-Adressen:
- `10.0.0.0 – 10.255.255.255`
- `172.16.0.0 – 172.31.255.255`
- `192.168.0.0 – 192.168.255.255`

### Spezialadressen:
- **Loopback**: `127.0.0.1`
- **APIPA (DHCP-Fallback)**: `169.254.0.0 – 169.254.255.255`

> 🔑 Tipp: Diese fünf Adressbereiche sollte man auswendig können!


## 💻 Windows-Kommandos

| Kommando       | Zweck                                |
|----------------|--------------------------------------|
| `ipconfig /all`| Netzwerkkonfiguration anzeigen       |
| `ping <ip>`    | Erreichbarkeit testen                |
| `arp -a`       | ARP-Cache anzeigen (MAC/IP-Zuordnung)|
| `ncpa.cpl`     | Netzwerkverbindungen öffnen          |
| `sysdm.cpl`    | Hostname/Arbeitsgruppe einstellen    |


## ❓ Können die PCs kommunizieren?

Kommunikation hängt davon ab:
- Gleiche **Netz-ID** durch passende Subnetzmaske?
- Gültige IP-Adressen?
- Unterschiedliche IPs (nicht doppelt)?
- Öffentliche vs. private Bereiche → NAT nötig?

Beispiele wurden mit `/8`, `/16` und `/24` durchgerechnet (siehe Musterlösungen im PDF).


## 🧠 Merksätze
- Subnetzmaske **trennt** Netz-ID und Host-ID
- `ipconfig` zeigt dir, **was dein Rechner denkt, wer er ist**
- Private IPs sind **nur intern gültig**, für extern braucht es NAT

### Aufgaben
1:
[Aufgabe 1](./Aufgaben/Tag2/Aufgabe1.md)
<br>
2:
[Aufgabe 2](./Aufgaben/Tag2/Aufgabe2.md)
<br>
3:
[Aufgabe 3](./Aufgaben/Tag2/Aufgabe3.md)
<br>
4:
[Aufgabe 4](./Aufgaben/Tag2/Aufgabe4.md)
<br>
5:
[Aufgabe 5](./Aufgaben/Tag2/Aufgabe5.md)
<br>

[Theorie Tag2](./Pdfs/Tag2.pdf)
