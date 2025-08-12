# TETRAwatch

**Autor:** FITIMDOTORG  
**Lizenz:** CC BY-NC-SA 4.0  

TETRAwatch ist ein fahrzeuginternes Detektionssystem, das dem Fahrer ermöglicht, Einsatzfahrzeuge im Nahbereich (typisch bis 50 m) zu erkennen, bevor sie optisch oder akustisch wahrnehmbar sind.  
Das System überwacht ausschließlich den BOS-Digitalfunk-Uplink (380–385 MHz) und detektiert die kurzen Funksignale mobiler BOS-Endgeräte (Fahrzeug- und Handfunkgeräte). Permanentsignale der Basisstationen werden zuverlässig ausgeblendet.

---

## Funktionen

- **Echtzeit-Erkennung** von TETRA-Uplink-Bursts im BOS-Frequenzbereich  
- **Reichweite:** optimiert für ca. 50 m Umfeld (Nahbereich)  
- **Akustische und optische Warnung** bei erkannten Signalen  
- **Filterung** permanenter Downlink-Träger der Basisstationen  
- **Keine Inhaltsauswertung** – nur Vorhandensein der Signale wird gemessen  
- **Rechtskonform**: rein energiebasierte Detektion ohne Dekodierung

---

## Hardwareanforderungen

- Raspberry Pi 4 oder 5 (2–4 GB RAM)  
- SDR-Stick (empfohlen: Airspy Mini oder RTL-SDR v3)  
- ¼-Wellen-Antenne (~19 cm) für 380–390 MHz  
- HF-Frontend-Filter (380–385 MHz, starke Sperre bei 390–395 MHz)  
- I²C-LCD (16×2, z. B. PCF8574-basiert)  
- Piezo-Buzzer (über Transistorstufe an GPIO)  
- Stromversorgung 12 V → 5 V / ≥3 A DC/DC mit EMV-Filterung

---

## Installation

```bash
git clone https://github.com/FITIMDOTORG/TETRAwatch.git
cd TETRAwatch
sudo ./install.sh
sudo systemctl start tetra-detector.service

Vor dem Start LCD-Adresse prüfen:

i2cdetect -y 1

Adresse ggf. in config.ini anpassen.

⸻

## Konfiguration

Alle Parameter befinden sich in config.ini:
	•	threshold_db: Auslöseschwelle in dB über Rauschboden
	•	window_ms: Analysefenster pro Frequenzmitte (ms)
	•	refractory_s: Sperrzeit zwischen Auslösungen
	•	centers: Liste der Mittenfrequenzen zur Uplink-Abtastung

⸻

Sicherheitshinweis

TETRAwatch wertet keine Inhalte aus, sondern misst ausschließlich das Vorhandensein von Funksignalen.
Trotzdem sind nationale Vorschriften zu Funkempfang und BOS-Frequenzen zu beachten.

⸻

Lizenz

Dieses Projekt steht unter der Creative Commons BY-NC-SA 4.0 Lizenz.
Kommerzielle Nutzung ist nicht gestattet.

