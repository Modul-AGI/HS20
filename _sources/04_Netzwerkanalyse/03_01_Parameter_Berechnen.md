# Aufgabe 5: Parameter berechnen und Kategorien bilden

Angenommen Sie sind auf Wohnungssuche in Wädenswil. Dabei gilt es nebst dem Budget viele wichtige raumgebundene Variablen zu berücksichtigen, dazu verwenden Sie natürlich QGIS. Sie wollen drei Kriterien untersuchen:

1. Laufdistanz zur nächsten Entsorgungsstelle
2. Erschliessung an die öffentlichen Verkehrsmittel unter Berücksichtigung des Fahrplans
3. Distanz zur Durchfahrtsstrasse

**Wir werden für jeden dieser drei Kriterien einen Rasterdatensatz** kreieren, den wir zum Schluss miteinander verrechnen können. So finden wir den Optimalen Standort unter der Berücksichtigung aller drei Kriterien. Starten Sie deshalb «QGIS Desktop 3.10.0 with GRASS 7.8.0» und beginnen Sie ein neues Projekt mit dem CRS CH1903+ LV95 (EPSG 2056). Laden Sie folgende Daten in das Projekt

1. Strassennetz Wädenswil («osm_highway_prepared.gpkg») aus den letzten Übungen (oder von Moodle)
2. Entsorgungsstellen Wädenswil (liegt auf Anhang bereit)
3. Gemeindegrenze Wädenswil (liegt auf Anhang bereit)
4. Optional: OSM Hintergrundkarte grau eingefärbt (siehe Übung letzter Woche)