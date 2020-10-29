(chap-netzwerk-einleitung)=
# Einleitung

Wir werden in den kommenden drei Lektionseinheiten mit QGIS verschiedene Aspekte der Netzwerkanalyse
untersuchen. Dafür lohnt es sich vorgängig eine sinnvolle Ordnerstruktur anzulegen. Wir empfehlen, in
einem geeigneten Folder _(z.B. C:/Users/benutzername/Studium/5_Semester)_ einen Ordner mit dem
Modulnamen anlegen (z.B. "Modul_AGI") und darin nachstehende Struktur zu pflegen. Vermeiden Sie bei der
Namensgebung auf jeden Fall Umlaute, Leerschläge und Sonderzeichen.

```
|-- Modul_AGI
    |── 01_Datenqualitaet_Unsicherheit
    |── 02_Coding_in_GIS                                           _
    |── 09_Netzwerkanalyse1                                         \            
    |   |── Geodaten                                                |
    |   |   |── Waedenswil.gpkg                                     |
    |   |   |── osm_highway.gpkg                                    |
    |   |── QGIS_Projectfiles                                       |
    |   |   |── Netzwerkanalyse_I_vorbereitung.qgs                  \ Netzwerk-
    |   |   |── Netzwerkanalyse_I.qgz                               / analyse I  
    |   |── Output                                                  |
    |   |   |── Uebersichtskarte.pdf                                |
    |   |── Unterlagen                                              |
    |   |   |── AGI_HS19_9_Netzwerkanalyse_I_vorbereitung.pdf       |
    |   |   |── AGI_HS19_9_Netzwerkanalyse_I.pdf                   _/
    |── 10_Netzwerkanalyse2 
    |   |── Geodaten
    |   |── QGIS_Projectfiles
    |   |── Karten
    |   |── Unterlagen
    ...                                                            _   

```


*Datensätze:* 

```{list-table}
:header-rows: 1
:name: table-datensaetze-netzwerkanalyse

* - Datensatz (inkl. Link)
  - Beschreibung
* - [Gemeinde_Waedenswil.gpkg](https://raw.githubusercontent.com/modul-agi/hs20/master/04_Netzwerkanalyse/data/Gemeinde_Waedenswil.gpkg)
  - Die Gemeindegrenze von Wädenswil. Dieser Datensatz basiert auf swissBOUNDARIES3D von Swisstopo.
* - [osm_highway.gpkg](https://raw.githubusercontent.com/modul-agi/hs20/master/04_Netzwerkanalyse/data/osm_highway.gpkg)
  - Alle "Highway" Linien aus dem OpenStreetmaps (Stand *nach* Vorbereitungsübung)

```
