# Aufgabe 1: Kürzeste Pfade auf Netzwerk berechnen

**Hinweis (Wiederholung)**: Standartmässig werden Dateien als Temporäre Files abgespeichert, die nach dem Schliessen von QGIS gelöscht werden. Um einen Output an einem festgelegten Ort abzuspeichern muss der Output definieret werden. Dazu klickt man neben [Save to temporary file] auf die drei Punkte und wählt «Save to File» aus.

```{figure} figures/saveToTemp.jpg
:name: saveToTempFile
```

## Übung 1: Projekt vorbereiten

Starten Sie «QGIS Desktop 3.10.0 with GRASS 7.8.0» und beginnen Sie ein neues Projekt mit dem CRS CH1903+ LV95 (EPSG 2056). Laden Sie den Datensatz «osm_highway_prepared.gpkg» von letzter Woche. Wer den Datensatz von letzter Woche nicht auffinden kann, findet die Datei auf Sektion "Anhang". Prüfen Sie, ob das CRS richtig erkannt wurde (Rechtsklick -> Properties -> Reiter Source -> Set source coordinate reference system -> Hier sollte EPSG 2056 stehen).

Wir brauchen zudem eine Hintergrundkarte zur Orientierung. Blenden Sie diese mit dem Plugin
«QuickMapServices» die Openstreetmap Hintergrundkarte ein (Web -> QuickMapServices -> OSM -> OSM
Standard) ein. Falls Sie diese Option nicht finden, müssen Sie das enstprechede Plugin «QuickMapServices»
installieren (siehe dazu Netzwerkanalyse I).

Die Hintergrundkarte dient lediglich zur Orientierung, die Farbe lenkt uns jedoch vom Netzwerk ab. Wechseln
Sie deshalb den Darstellungsmodus auf Graustufen mittels Rechtklick auf den Layer «OSM Standard» -> Properties -> Symbology -> 
Grayscale Auswahl: «By lightness».

## Übung 2: Kürzester Pfad berechnen

Nun können wir mittels «Shortest path» (aus dem Toolset «Network analyses» den kürzesten Pfad zwischen
zwei Knotenpunkten auf dem Netzwerk berechnen. Starten sie das Tool und wählen sie als Input Datensatz
(«Vector Layer representing network») _osm_highway_prepared_ aus.

Die Start- und Endpunkte können Sie interaktiv in der Karte setzen. Klicken Sie dazu auf das Symbol neben den
entsprechenden Feldern («Start point» bzw. «End point») und klicken Sie in der Karte an den gewünschten
Stellen. Führen Sie das Tool mit «Run» aus.

Visualisieren Sie nun den neuen Layer «Shortest Path» so, dass er gut ersichtlich ist.

**Hinweis:** Auch GRASS GIS bietet einen Shortest Path Algorithmus an (v.net.path). Dieser ist darauf ausgelegt,
viele Kürzeste Pfade für viele Punkte zu berechnen, und nimmt als Input deshalb ein Textfile.

## Übung 3: Mit ORS Routing vergleichen

Nun wollen wir diese Route mit derjenigen eines professionellen Routing Services vergleichen.
https://maps.openrouteservice.org/ bietet ihre Dienste bis zu einem bestimmten Kontingent kostenlos an.
Installieren Sie das Plug-In «ORS Tools» um diesen Service zu nutzen.

Führen Sie das Tool nach der Installation via Web -> ORS Tools -> ORS Tools aus. Fügen Sie bei Settings ( ) -> 
«API Key» folgenden Schlüssel ein: 5b3ce3597851110001cf624843314e7742a7494fb0f7bc672cb9d6a

Über diesen Schlüssel wird sichergestellt, dass die Anzahl Abfragen pro Minute und Tag ein gewisses
Maximum nicht überschreiten.

Geben Sie Start und Endpunkt mit der Maus ein (klick auf das +) und orientieren sich dabei an dem Layer
«Shortest_Path» (aus der vorherigen Übung). Allenfalls verschwindet das «ORS Tools» Fenster, sie können es
aber über die Toolbar wieder aufrufen.

```{figure} figures/osm.jpg
:name: ORSrouting
```

Führen Sie die Berechnung mit «OK» aus und vergleichen den resultierenden Pfad mit «Shortest Path». Führen
Sie die gleiche Berechnung mit verschiedenen Einstellungen durch (kürzeste Route, schnellste Route, Fahrrad,
zu Fuss). Vergleichen Sie die unterschiedlichen Routen mit unserer eigenen Berechnung und visualisieren Sie
diese in einer Karte.

Berechnen Sie nun mit OSM Routing den kürzesten Pfad zwischen Campus Grüental und Campus Reidbach,
auch wieder je einmal mit der Verkehrsmodalität Auto, Fahrrad und Fussweg. Vergleichen Sie die drei
Resultate.

## Übung 4: Traveling Salesman für Campus Standorte

Angenommen Sie sind ein Kurrierdienst und müssen ausgehend von der Halbinsel Au aus alle Campus
Standorte der ZHAW Wädenswil besuchen. Sie wollen die Route so optimieren, dass Sie die kürzeste Route
Sie das gleichnamige Tool (v.net.salesmen) um genau dieses Problem zu lösen.

1. Erstellen Sie dazu als erstes eine neue Geopackage Datei (Layer -> Create Layer -> New Geopackage Layer) um die Campus Standorte zu erfassen
    - Mit dem Feld «Database» ist der Pfad inkl. Dateiname der zu erstellenden Datei gemeint. Wählen Sie hier an einem geeigneten Speicherort den Dateiname «campus_waedenswil.gpkg»
    - «Table name» ist der Name des Layers innerhalb der Geopackage Datei (im Gegensatz zu einem Shapefile können innerhalb eines Geopackage mehrere Layers von unterschiedlichen Datentypen Coexistieren)  
    - Wählen Sie bei «Geometry Type» «Point» aus und bei CRS EPSG 2056
    - Fügen Sie eine Spalte in der Attributtabelle hinzu indem Sie unter «New field» -> «Name» den Wert «Standort_name» eingeben (Hier wollen wir «Grüental», «Reidbach».. erfassen) Wählen Sie einen geeigneten Datentyp sowie eine geeignete Maximallänge
    - Bestätigen Sie mittels «Add field to list»
    - Erstellen Sie das Geopackage mit «OK»  
2. Starten Sie mit einem Klick auf **den Stift** die Editiersession und fügen Sie Features hinzu mit dem «Add Feature» Werkzeug. Digitalisieren Sie so die Campus Standorte (Grüental, Reidbach, Seifenstreuli, Schloss) sowie den Ausgangspunkt (Halbinsel Au). Wählen Sie pro Standort einen für Sie geeigneten Punkt, möglichst auf dem OSM Strassennetz.
3. Speichern Sie die erfassten Punkte mit einem Klick auf «Save Edits».
4. Starten Sie nun das Tool v.net.salesman (über die Processing Toolbox) und wählen als Input Layer den OSM Strassendatensatz und als «Center Point Layer» die eben digitalisierten Standorte.
5. v.out.ogr output type: auto.
6. Betrachen Sie die Output daten.

## Übung 5: Traveling Salesman für mehr Standorte

Der Traveling-Salesman-Pfad für fünf Punkte zu berechnen ist relativ trivial und könnte «von Hand» gerechnet werden. Anspruchsvoller wird es jedoch, wenn sich die Anzahl der Standorte erhöht. Nehmen wir an, Sie wollen eine Einkaufstour durch alle Läden in Wädenswil machen: Nutzen Sie die OSM Daten und v.net.salesman und eine sinnvolle Route zu berechnen.  

1. OSM Daten der Läden laden: Vector -> QuickOSM -> QuickOSM
2. key «shop» -> Run query sowie Gebiet wählen (siehe dazu Netzwerkanalyse I)
3. Punkt-Daten der Shops in CRS 2056 konvertieren (reproject). Clippen ist fakultativ (nicht erreichbare Knotenpunkte werden schlicht ignoriert)
4. v.net.salesman mit diesen Standorten durchführen


## Übung 6 (fakultativ, Guezli-Challenge): Traveling Salesman für noch mehr Standorte

Um unsere Rechenmaschine richtig herauszufordern, können wir den Traveling Salesmen Pfad für alle Gebäudestandorte in Wädenswil berechnen. Nutzen Sie hierzu QuickOSM um «building» herrunterzuladen. Reprojizieren Sie die Polygon-Daten in CRS 2056 und konvertieren Sie diese in Punkte, indem Sie das Centroid pro Polygon berechnen (Tool «Polygon Centroids»). Berechnen Sie anschliessend den Traveling Salesman. Ermitteln Sie die Gesamtdistanz dieses Pfades, indem Sie mit dem Field Calculator die Länge pro Segment rechnen (length) und anschliessend die Summe aller Längen ermitteln (View -> Panels -> Statistic). **Wer zuerst die korrekte Distanz ausruft, wird mit Ruhm, Ehre und einem Guezli belohnt!**

```{warning}
**Merken Sie sich:** 
 - Für viele klassische Fragestellungen (z.B. shortest path, traveling salesmen) bietet QGIS / GRASS 
 einen passenden Algorithmus
 - Die Tools werden teilweise sehr unterschiedlich angesprochen (shortest path braucht Textfiles,
 Traveling salesmen braucht Punkt-Features) und liefern unterschiedliche Outputs
```
