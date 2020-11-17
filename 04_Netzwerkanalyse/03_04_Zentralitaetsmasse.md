# Aufgabe 7: Zentralitätsmasse

## Übung 7.1: Zentralitätsmasse betrachten und auswählen

Da Sie aber auf keinen Fall an einer Durchfahrtsstrasse wohnen möchten, müssen Sie dies in der Wohnungssuche ebenfalls berücksichtigen. Laden Sie deshalb den Datensatz "waedenswil_centrality.gpkg" aus der ersten Woche. Falls Sie diesen nicht mehr haben, können Sie die Zentralitätsmasse neu berechnen (v.net sowie v.net.centrality) oder Sie verwenden den Datensatz auf Moodle. Prüfen Sie anhand der Symbolisierung, welches Mass "Durchfahrtsstrassen" am besten abbildet.

## Übung 7.2: Zentralitätsmasse in Fläche überführen

Das gewählte Zentralitätsmass können wir nun ebenfalls mit dem Tool "Inverse distance weighted interpolation" (SAGA) in eine Oberfläche überführen. Führen sie das Tool analog Übung 6.3, mit dem gewählten Zenralitätsmass aus. Sie können die Parameter des Tools nach eigenem Gutdünken auch anpassen.
Clippen sie anschliessend den Output anschliessen mit dem Werkezeug "Clip raster by Mask Layer" (GDAL). Speichern Sie den Output unter centrality_raster.tif in ihrem Projektordner und gruppieren Sie alle Layers im Zusammenhang mit den Zentralitätsmassen.

