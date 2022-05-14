# Beleuchtungsstärken und Fremdlichtfestigkeit bei Sensoren

## Wieso sind optische Sensoren empfindlich gegenüber Umgebungslicht?
Alle optischen Sensoren können durch Umgebungslicht - der Fachbegriff dafür ist "Fremdlicht" - gestört werden. Je nach Sensorauslegung können schon wenige Hundert Lux zum Ausfall eines Sensors führen. Sensoren für den Außenbereich müssen Fremdlichtfestigkeiten von >100 klx aufweisen. Die meisten optischen Sensoren senden eigenes Licht ("Nutzlicht") aus, das auf das anzutastende Objekt fällt. Das Objekt reflektiert einen Teil des Nutzlichts zurück zum Sensor. Je nach Sensorverfahren d.h. je nachdem welche Objekteigenschaft gemessen werden soll, wie etwa der Objektabstand, die Objektfarbe oder die Objektpräsenz, wird die Lichtlaufzeit, das Lichtspektrum, die Lichtintensität/-verteilung oder ein anderer Lichtparameter vom Sensor ausgewertet.

Auf die Empfängeroptik des Sensors und auf das vom Sensor angetastete Objekt fällt jedoch nicht nur dieses Nutzlicht sondern zusätzlich auch Fremdlicht. Die Quelle des Fremdlichts ist meistens das Sonnenlicht oder in geschlossenen Räumen die Allgemeinbeleuchtung wie Halogen- oder LED-Leuchten.

Man unterscheidet zwischen indirektem und direktem Fremdlicht:
Indirektes Fremdlicht, ist Fremdlicht das auf das Objekt fällt und zusammen mit dem Nutzlicht zurück zum Sensor reflektiert wird. Indirektes Fremdlicht addiert sich auf das Nutzlicht auf.
Direktes Fremdlicht fällt direkt auf den Empfänger des Sensors und gelangt dadurch auf dessen Photodiode. Dirketes Fremdlicht kann man somit auch als ein Blenden des Sensors bezeichnen.

![Fremdlicht](/skizzeNutzFremdLicht.png) 

Nahezu alle optische Sensoren verwenden intensitätsmoduliertes Nutzlicht. Eine Infrarot-Fernbedienung pulst beispielsweise das Nutzlicht mit einer Frequenz von 38 kHz. Da das Fremdlicht meistens Gleichlicht ist, kann so im Empfänger des Sensors der Fremdlichtanteil nach der Photodiode per Hochpassfilter elektronisch unterdrückt werden. Dies funktioniert aber nur solange wie das Fremdlicht die Photodiode nicht übersteuert. Außerdem nimmt in jedem Fall das Rauschen des Nutzsignals durch das Fremdlicht zu und damit die Messgenauigkeit des Sensors ab.
Hinzu kommt, dass die Allgemeinbeleuchtung ebenfalls oft intensitätsmoduliert ist: LEDs werden oft über Pulsweitenmodulation gedimmt, Leuchtstoffröhren werden mit Wechselspannung betrieben.

Wenn es die Applikation und die Sensorkosten zulassen, wird möglichst Nutzlicht in dem Bereich verwendet, in dem das Spektrum des Fremdlichts eine geringe spektrale Leistungsdichte hat: Daher versucht man möglichst Infrarotlicht zu verwenden - je langwelliger destso besser, jedoch auch desto teurer.

Weiter verwenden alle optischen Sensoren empfangsseitig optische Bandpassfilter, deren Durchlassbereich möglichst nur dem Nutzlichtspektrum entspricht. Das Fremdlicht wird hier spektral weitgehend ausgeblendet. Jedoch kommt innerhalb des Durchlassbereichs immer noch Fremdlicht zum Empfänger des Sensors.
Daher verwendet man gerne schmalbandiges Laserlicht und passt den Durchlassbereich des optischen Bandpassfilters so eng wie möglich daran an. Dies ist aber bei kostensensitiven Sensoren wie einfachen Lichttastern oder Lichtgittern nicht wirtschaftlich, weshalb hier meistens nur monochromatische LEDs als Nutzlichtquellen und nur eingefärbte Kunststoffscheiben als "Bandpassfilter" Verwendung finden.

Bis auf wenige Ausnahmen im Militär- oder Weltraumbereich sind optische Sensoren trotz dieser Gegenmaßnahmen in der Praxis fremdlichtempfindlich. Denn Präzisionsoptiken wie genau gefertigte Linsen und Filter sind sehr kostspielig.

## Wieso wird die Fremdlichtfestigkeit in Lux (lx) angegeben?
Damit ein Anwender abschätzen kann, ob die Verfügbarkeit eines optischen Sensors trotz Fremdlicht gegeben ist, muss die Fremdlichtfestigkeit des Sensors in irgend einer Weise spezifiziert sein.
Idealerweise würde der Sensorhersteller hierfür die Nutzlichtwellenlänge und den Durchlassbereich des Sensorempfängers sowie die Modulation des Nutzlichts angeben. Dann könnte die Fremdlichtfestigkeit als maximale Bestrahlungsstärke für Gleichlicht bzw. moduliertes Licht spezifiziert werden.

Eine solche Sensor-Spezifikation ist jedoch aus mehreren Gründen nicht praktikabel:

Der Sensorhersteller möchte aus Gründen des IP-Schutzes nicht diese optischen Eigenschaften des Sensors veröffentlichen.
Der Anwender hat selten die Möglichkeit den Fremdlichtpegel spektral- und zeitaufgelöst zu bestimmen. Er besitzt höchstens ein Luxmeter um damit die Beleuchtungsstärke des Fremdlichts abzuschätzen.
Deshalb wird die Fremdlichtfestigkeit von Sensoren allgemein als maximale Beleuchtungsstärke in Lux auf dem angetasteten Objekt oder auf dem Sensorempfänger spezifiziert.
Zugegebenermaßen ist eine solche Spezifikation nicht sonderlich wasserdicht, denn sie berücksichtigt weder das Fremdlichtspektrum, bei der direkten Blendung eine Richtung des einfallenden Fremdlichts, noch eine mögliche Modulation des Fremdlichts.

In Normen zu bestimmten Sensoren ist jedoch zur Bestimmung der Fremdlichtfestigkeit der Messaufbau für die zulässige Beleuchtungsstärke näher spezifiziert. Beispielsweise wird ein Halogenscheinwerfer mit einer bestimmten elektrischen Leistung und Reflektorgröße vorgeschrieben, der entlang der Sichtlinie des Sensors in den Sensor hinein strahlt.

## Fremdlicht-Bestrahlungsstärke aus der Beleuchtungsstärke abschätzen
Im Jupyter Notebook wird exemplarisch gezeigt, wie bei Kenntnis des Fremdlichtspektrums und der Beleuchtungsstärke des Fremdlichts die Bestrahlungsstärke auf der Photodiode des Sensor-Empfängers abgeschätzt werden kann.  
Dabei wird der Wert der Bestrahlungsstärke des Fremdlichts so lange variiert, bis dessen gewünschte Beleuchtungsstärke eingestellt ist. Die Berechnung ergibt die dazu gehörige Bestrahlungsstärke des Fremdlichst auf dem Objekt bzw. dem Empfänger.

> Hinweis: Wenn Sie oben im File Explorer auf eine der beiden Jupyter Notebooks (Endung ".ipnyb") klicken, dann wird lediglich ein Viewer geöffnet, in dem Sie das Notebook nur anschauen können. *Dieser einfache Viewer funktioniert jedoch nicht wirklich zuverlässig.*  
**Zum Anschauen verwenden Sie daher bitte den speziellen Viewer für Jupyter-Notebooks "nbviewer" [über diesen Link](https://nbviewer.jupyter.org/github/StefanMack/LumenSpectra/blob/main/lumenUndSpektren.ipynb).**

Möchten Sie die Codebeispiele darin einzeln ausführen und ändern, dann klicken Sie bitte auf das Icon "launch|binder". **Das Starten des Webservice binder kann bis zu einer Minute dauern.**


Prof. Dr. S. Mack, 14. Mai 2022.

License
-----
<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img alt="Creative Commons Lizenzvertrag" style="border-width:0" src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" /></a><br />Dieses Werk ist lizenziert unter einer <a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative Commons Namensnennung - Weitergabe unter gleichen Bedingungen 4.0 International Lizenz</a>.
