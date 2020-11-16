# Aufgabe 9: Flächen verrechnen

In dieser Übung verschneiden wir die Informationen aus Entsorgungsstellen (abfall_raster.tif), ÖV-Güteklassen (oev_raster.tif), und Zentralitätsmass (centrality_raster.tif), die wir in den vorherigen Übungen berechnet und in Raster überführt haben. Durch die Verschneidung können wir den Optimalen Wohnort eruieren. Diese Methode ist auch als Multikriterienevaluation bekannt und kennt ihr bereits vom GIS «Basic» Modul.
In einem ersten Schritt müssen wir alle drei Rasterdatensätze auf eine einheitliche Skala (z.B. 0 – 100) bringen um sie anschliessend miteinander verrechnen zu können. Dafür brauchen wir die Minimum- und Maximumwerte der drei Raster Datensätzen Güteklassen oev_raster.tif, centrality_raster.tif, abfall_raster.tif. Gehen Sie dafür in die Properties -> Information von jedem Layer und notieren Sie sich die minimalen und maximalen Zellenwerte.

## Übung 1: Rasterdatensätze skalieren
Öffnen Sie anschliessend den Raster Calculator (Raster -> Raster Calculator) und Skalieren sie jeden der drei Rasterdatensätze einzeln mit folgender Formel:

$X_{new}$ = $\frac{x_{i} - x_{min}}{x_{max} - x_{min}} * 100$

Der Output dieser Übung sind drei Rasterdatensätze mit einer Skala von 0 bis 100

```{figure} figures/rastCalc.jpg
:name: 
```
In Worten: Ziehen Sie vom Rasterwert (xi) den Minimumwert (xmin) ab und dividieren sie diesen durch die Spannweite der Zahlen (**$x_{max}$-$x_{min}$**)
- $x_{i}$ ist der jeweilige Rasterdatensatz, xmin und xmax sind jeweils die Zahlenwerte, die sich eben notiert hatten.
- Achten sie darauf, dass Sie die richtigen Klammen setzen.
- Speichern Sie diese unter folgenden Namen ab: oev_scaled.tif, abfall_scaled.tif, centrality_scaled.tif.

## Übung 2: Zusammenführen mit Raster Calculator

Nutzen Sie erneut den Raster Calculator um die drei Rasterdatensätze miteinander zu verrechnen. Die einfachste Variante ist den Mittelwert der drei Rasterdatensätze zu berechnen. Dafür muss man alle drei summieren und mit drei dividieren:

$raster_{neu}$ = $\frac{oevScaled+abfallScaled+centralityScaled}{3}$

Optional kann man auch die drei Rasterdatensätze unterschiedlich gewichten, wie beispielweise nachstehend. Beachten Sie, dass in diesem Fall nicht mehr durch 3, sondern durch die Summe der Gewichte dividiert wird. Visualisieren und interpretieren Sie anschliessend das Resultat.

$raster_{neu}$ = $\frac{oev*1+abfall*10+centrality*5}{16}$
