# Klima-Heizung-Steuerung

Dieses Projekt optimiert mein Heiz- und Kühlverhalten mit Home Assistant auf einem Beelink Mini PC.

## Hardware-Kontext
* **Zentrale:** Home Assistant (Beelink Mini S13, Intel N150)
* **Heizung:** Vaillant VC 126/2-C, VRC 410, Shelly mini 1 gen3 am Thermostat
* **Klima:** Samsung Airise (Esszimmer/Wohnzimmer, Kinderzimmer, Schlafzimmer)
* **Energie:** * PV-Anlage: 7,2 kWp (Süd, 180°, 40° Dachneigung)
    * Wechselrichter: Fronius Symo GEN 6.0 Plus
    * Speicher: BYD Battery-Box Premium HV 5,4 kWh
* **Sonstiges:** MyPV AC ELWA 2 Heizstab

## Die Automatisierungen
Hier findest du meine 4 Kern-Automatisierungen:

### 1. Klima: Automatik-Wächter
Diese Automation prüft, ob genügend PV-Produktion für heute vorhanden ist, um die Klima laufen zu lassen.

### 2. Klima Master
Prüft alle 5 Minuten, ob die Werte für den Betrieb erfüllt sind:
* **Zum Einschalten:**
    * Überschuss über 600 Watt
    * Akku muss über 60 % geladen sein
    * Schalter "Klima Automation" muss auf ON stehen
    * Außentemperatur entscheidet über "Heizen" oder "Kühlen"
* **Zum Ausschalten:**
    * Wenn Schalter "Klima Automation" auf OFF geht
    * Wenn Akku unter X % fällt

### 3. Heizung – Sicherheits-Check bei Neustart
Prüft bei Neustart von HA (oder periodisch), ob die Temperatur zu niedrig oder zu hoch ist und schaltet die Heizung entsprechend ON oder OFF.

### 4. Heizung – Temperatur Steuerung
Wenn in einem Raum die Temperatur für 5 Minuten unter 20,5°C fällt, wird die Klima aktiviert. Bei einer Durchschnittstemperatur über 22,5°C wird die Heizung deaktiviert.
