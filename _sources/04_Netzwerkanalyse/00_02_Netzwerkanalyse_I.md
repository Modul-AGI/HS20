# Zentralitätsmasse

KW 45

```{admonition} Übungsziele
:class: attention
- Einfache GIS-Operationen mit QGIS durchführen können (Clip, Reproject, Abfrage der Attributtabelle,
    Symbolisierung, Export als jpg)
- Schnittstelle zwischen QGIS und anderer GIS-Software am Beispiel GRASS kennenlernen
- Erste Netzwerkoperationen mit QGIS/GRASS GIS durchführen
- Netzwerk-Zentralitätsmasse verstehen und für einfache Netzwerkdaten berechnen
```

## 1. Einfache GIS Operationen mit QGIS

Starten Sie «QGIS 3. 10 .0 with GRASS GIS 7. 8 .1», beginnen Sie ein neues QGIS Projekt und speichern dies an
einem geeigneten Ort (siehe Vorbereitungsübungen) ab. Weisen Sie dem Projekt das Koordinatensystem
EPSG 2056 zu und importieren die Gemeindegrenze sowie die OSM Strassendaten aus der
Vorbereitungsübung.

### Übung 1: Daten Transformieren

Die OSM Daten sind aktuell noch im Koordinatensystem WGS84 (EPSG 4326). Die Gemeindegrenze hingegen
ist mit den neuen Schweizer Landeskoordinaten CH1903+ LV95 (EPSG 2056) abgespeichert. Wir wollen in
unserer Analyse mit CH1903+ LV95 (EPSG 2056) arbeiten. Transformieren Sie dazu den Strassendatensatz in
das Koordinatensystem CH1903+ LV95 (EPSG 2056). Nutzen Sie dazu das Tool «Reproject Layer».

Viele wichtige Tools lassen sich über den Menü Bar aufrufen (v.a. «Vector» und «Raster»). Die Tools lassen
sich auch relativ rasch mit der Suchfunktion der «Processing Toolbox» finden.

```{figure} figures/ueb1_fig1.jpg
:name: figure 1
```

### Übung 2: Daten Clippen

Zoomen sie auf die Gemeindegrenze (Layers Panel -> Rechtsklick auf Datensatz -> Zoom to layer»). Es ist
ersichtlich, dass die Strassendaten über die Gemeindegrenze hinaus verlaufen. Wir möchten für die
kommenden Übungen nur die Strassen, die _innerhalb_ der Gemeinde Wädenswil liegen. Dazu müssen wir das
Strassennetz mit der Gemeindegrenze verschneiden («clip»). Führen Sie das gleichnamige Werkzeug mit
dem Input Layer «OSM_highway» und dem Clip Layer «Stadt_ Waedenswil.gpkg» aus.

Es gibt eine ganze Reihe Werkzeuge zum Begriff «clip». Entscheiden Sie selbst, welches für diese
Fragestellung geeignet ist.

## 2. Arbeiten mit GRASS GIS Plugin

Die mächtigsten (aber nicht die einzigen*) Netzwerkanalyse Werkzeuge in QGIS stammen aus dem
eigenständigen GIS «GRASS GIS», welches bei der Installation von QGIS mitinstalliert wird. Diese können
innerhalb von QGIS verwendet werden.

* Da QGIS wie bereits erwähnt von verschiedenen Personen und Gruppen entwickelt wird, gibt es auch
Doppelspurigkeiten, die man so in einer kommerziellen Software wie ArcGIS weniger vorfindet. In dieser
Hinsicht ist QGIS sehr ähnlich wie die Programmiersprache R.

### Übung 3: Topologie bereinigen

Das OSM Strassennetz «osm_highway» ist topologisch nicht perfekt für unsere Zwecke vorbereitet. An
Kreuzungen fehlen teilweise Knoten, welche ein «abbiegen» auf der Kreuzung ermöglich. Um diesen
Umstand zu beheben, nutzen wir das Tool «v.clean» und führen damit die Operation «break» durch.
Dadurch werden Linien an Kreuzungen unterbrochen. Diese Operation löst einige topologische Fehler, führt
z.B. bei Brücken und Tunnels aber euch neue Unstimmigkeiten ein, die Sie an dieser Stelle aber getrost
ignorieren können.

1. Werkzeug “v.clean” auswählen
2. Parameter:
    a. _Layer to clean_ : Transformierter und geclippter OSM Strassendatensatz
    b. _Cleaning tool_ : break
    c. _v.out.ogr output type:_ auto
3. Mit “Run” ausführen


### Übung 4: Losgelöste (getrennte) Elemente entfernen

Aufmerksamen Anwendern könnte nun auffallen, dass gewisse Bestandteile des Netzwerks nicht mit dem
Hauptnetz verbunden sind. Diese getrennten Elemente können mit dem Werkzeug v.net.components
identifiziert werden. Das Werkzeug prüft, welche Bestandteile des Netzwerkes miteinander verbunden sind
und gruppiert diese mit Nummern. Im Idealfall sollte unser Netzwerk aus einer Gruppe bestehen; so wäre
jeder Knotenpunkt mit jedem andern Knotenpunkt verbunden: Bei uns ist dies jedoch nicht der Fall. Damit
wir in den nachstehenden Übungen mit einem sauberen Datensatz arbeiten können, bereinigen wir dieses
Problem an dieser Stelle:

1. Führen Sie das Werkzeug aus
    a. _Type of components_ : «strong»
    b. _V.out.ogr output type:_ auto
2. Symbolisieren den entstandenen Liniendatensatz nach den vergebenen Kategorien («comp»)
3. Ermitteln Sie die Nummer der Hauptkategorie (z.B. mit dem Werkzeug «Identify Features»
4. Öffnen Sie die Attributtabelle und machen eine «Selektion anhand einer Abfrage» («Select Features
    using an expression» [1])
5. Selektieren Sie die Hauptkategorie mittels einer korrekten Abfrage (z.B. comp = 99). QGIS bietet
    ihnen hierfür leider wenig Hilfestellung (im Gegensatz zum Query Builder von ArcGIS)
6. Um sich von den anderen Kategorien zu trennen, haben Sie nun zwei Möglichkeiten:
    a. Eine Editiersession starten [2], die Selektion invertieren [3] und die selektierten Daten
       löschen [4]. Speichern Sie den Layer anschliessend mit folgendem Namen ab:
       «osm_highway_prepared.gpkg»
       ODER
    b. Selektierte Daten (ohne Invertierung) in ein neues File exportieren mittels Rechtsklick auf
       den Layer -> «Save as» -> Häkchen bei «Save only selected features» -> Speichern als
       «osm_highway_prepared.gpkg»
       
```{figure} figures/ueb1_fig2.jpg
:name: figure 2
```

### Übung 5: Zentralitätsmasse berechnen

Nun kann mit der eigentlichen Netzwerkanalyse begonnen werden. Wir rechnen für unser bereinigtes
Strassennetz verschiedene Zentralitätsmasse.

1. v.net.centrality starten
2. Parameter
    - _Input vector line layer_ : Bereinigter Output aus letzter Übung
    - _Centers point layer (nodes):_ Punkt-Output aus letzter Übung
    - _Name of betweenness centrality column_ : “betwCt”. Wichtig: dieser Variablenname darf nicht
       „between“ oder „betweenness“ lauten, sonst gibt es einen Ausführungsfehler.
    - _v.out.ogr output type_ : auto
3. Mit “run” ausführen
4. Speichern Sie die Resultierende Datei in ihrem Ordner ab («waedenswil_centrality.gpkg»)

### Übung 6: Zentralitätsmasse Visualisieren

Visualisieren Sie die Ausprägung «Closeness» der berechneten Zentralitätswerte über die Symbologie (Layer
Properties -> Style -> Graduated). Wählen Sie eine geeignete Methode und passen Sie den Stil an, bis er
Ihnen gefällt. Spielen Sie dabei mit der Klassifikationsmethode (Mode: Equal interval, Quantile, Natural
Breaks..) sowie der Color ramp rum. Achten Sie darauf, dass Sie immer auf «Classify» klicken müssen, um
Änderungen anzuwenden.


### Übung 7: Zentralitätsmasse vergleichen

Installieren Sie das Plugin «QuickMapServices» um eine OSM Hintergrundkarte einzubinden. Um direkt in
QGIS die Zentralitätsmasse zu vergleichen, duplizieren sie den entsprechenden Layer noch zweimal
(rechtsklick -> Duplicate) – so können Sie jede der Zentralitäten separat symbolisieren und vergleichen. Sie
können auch für jedes der Zentralitätsmasse eine Karte exportieren via Project -> Save as Image.

Vergleichen Sie die drei Zentralitätsmasse und setzen Sie sie in den Kontext der Theorie.

