# Anhang

## Datensätze

Hier befinden sich alle Datensätze, die im Laufe des Blocks "Netzwerkanalyse" benötigt werden:

```{list-table} Datensätze für den Block "Netzwerkanalyse"
:header-rows: 1
:name: table-datensaetze-netzwerkanalyse

* - Datensatz (inkl. Link)
  - Beschreibung
* - [Gemeinde_Waedenswil.gpkg](https://raw.githubusercontent.com/modul-agi/hs20/master/04_Netzwerkanalyse/data/Gemeinde_Waedenswil.gpkg)
  - Die Gemeindegrenze von Wädenswil. Dieser Datensatz basiert auf swissBOUNDARIES3D von Swisstopo.
* - [osm_highway.gpkg](https://raw.githubusercontent.com/modul-agi/hs20/master/04_Netzwerkanalyse/data/osm_highway.gpkg)
  - Alle "Highway" Linien aus dem OpenStreetmaps (Stand *nach* {ref}`ex-network-osmdownload`)
* - [osm_highway_prepared.gpkg](https://github.com/Modul-AGI/HS20/raw/master/04_Netzwerkanalyse/data/osm_highway_prepared.gpkg)
  - Alle "Highway" Linien transformiert und neu projiziert (Output aus {ref}`ex-clip`)
* - [shops_waedenswil.gpkg](https://github.com/Modul-AGI/HS20/raw/master/04_Netzwerkanalyse/data/shops_waedenswil.gpkg)
  - Alle Läden in Wädenswil (EPSG 2056)
* - [buildings_waedenswil_polygons.gpkg](https://github.com/Modul-AGI/HS20/raw/master/04_Netzwerkanalyse/data/buildings_waedenswil_polygons.gpkg)
  - Alle Gebäudestandorte (Polygon Daten) in Wädenswil (EPSG 2056)
```

