# Zeitmessung mit NEO6m 0001

![Plan](https://github.com/denisepostl/GPS_ESP32/blob/patch-1/plan.png)

## Hardware
Im folgenden Abschnitt wird näher auf die Hardware eingegangen.

### Lötstellen
Das nachfolgende Bild, soll die vorgenommenen Lötstellen an den Pins zum GPS-Modul erläutern.

![Lötstellen](https://github.com/denisepostl/GPS_ESP32/blob/patch-1/aufbau.png)

### Verbindung zwischen GPS-Sensor und ESP
Der GPS-Sensor ist mit dem ESP über die entsprechenden Pins für VCC, RX, TX und GND verbunden.

- **VCC**: Dieser Pin dient zur Stromversorgung.
- **RX**: Hierüber werden Daten empfangen.
- **TX**: Über diesen Pin erfolgt die Datenübertragung.
- **GND**: Zur Erdung des Sensors.

  ![Aufbau](https://github.com/denisepostl/GPS_ESP32/blob/patch-1/aufbau_esp.png)

## Daten
Im nachfolgenden Abschnitt wird näher auf die Datenerfassung eingegangen.

### Datenerfassung
Ein ESP ist am Ziel platziert und ein ESP am Start. Sobald das Go-Cart durch die Lichtschranke am Start durchfährt wird am ersten ESP ein Timestamp gespeichert. Sobald es durch das Ziel passiert ist wird am zweiten ESP ein Timestamp gespeichert. Anschließend kann die Differenz berechnet werden.

Die Daten werden als txt vom ESP überliefert. 

![Platformio](https://github.com/denisepostl/GPS_ESP32/blob/patch-1/platformio.png)

Für die Timestamps wäre folgende Information wichtig:

`$GPGGA,123241.00,4713.46600,N,01537.43809,E,1,06,1.88,506.9,M,42.3,M,,*50`

- `123241.00` - Die Uhrzeit, zu der diese Position fixiert wurde, in Stunden, Minuten und Sekunden (HHMMSS.SS), hier 12:32:41 UTC.
- `4713.46600,N` - Die geografische Breite in Dezimalgrad, hier 47 Grad 13.46600 Minuten nördlicher Breite.
- `01537.43809,E` - Die geografische Länge in Dezimalgrad, hier 15 Grad 37.43809 Minuten östlicher Länge.
- `1` - Die Fixierungsqualität. In diesem Fall handelt es sich um eine gültige GPS-Fixierung.
- `06` - Die Anzahl der Satelliten, die zum Zeitpunkt der Fixierung verfolgt wurden.
- `1.88` - Die horizontale Verminderung der Position, ein Wert, der die Genauigkeit der Position angibt.
- `506.9,M` - Die Höhe über dem Meeresspiegel in Metern, hier 506,9 Meter.
- `42.3,M` - Die Höhe des Geoids (Mittleres Meeresspiegel) über dem WGS84-Ellipsoid, hier 42,3 Meter.
- Leere Felder - Es gibt zwei leere Felder in diesem Satz. Das erste könnte normalerweise die Zeit in Sekunden seit der letzten DGPS-Aktualisierung enthalten, und das zweite könnte die DGPS-Station-ID-Nummer sein, aber diese Informationen fehlen hier.
- `*50` - Die Prüfsumme (Checksumme) am Ende des Satzes, die zur Überprüfung der Datenintegrität verwendet wird.

Anmerkung: Es werden richtige Uhrzeit Daten gesendet.

## Nächste Schritte
- Visualisieren der Daten mit Grafana (hat Arduino AddOn)
- Daten in InfluxDB speichern sollte möglich sein
- Was kann man testen?

## Quellen
### Datenblatt
- https://content.u-blox.com/sites/default/files/products/documents/NEO-6_DataSheet_%28GPS.G6-HW-09005%29.pdf

### Tutorials
- https://randomnerdtutorials.com/guide-to-neo-6m-gps-module-with-arduino/
- https://quadmeup.com/how-to-connect-gps-to-esp32/
- https://github.com/DzikuVx/esp32_gps_thingy/blob/master/types.h
- https://github.com/DzikuVx/QmuTactile


