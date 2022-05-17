# Klangfarben
(*Ein Projekt von Lisa Umlauft,Alexander Konrad und Janina D. Lettow*)
 &nbsp;
---
### **Konzept**
---
Kreiere eine Playlist, ordne Farben hinzu und kombiniere bis zu 8 von diesen auf einer kleinen Disc mit RFID tags.

RFID-Tag =

- Technologie für Sender-Empfänger-Systeme
- kontaktlose Lokaliserung und Übermittlung von Daten
- Senden durch Antenne oder Mikrochip
- Senden durch integrierte Schaltung (IC) möglich
- Mikrochip wird mit den gewünschten Daten beschrieben

---
### **2) Wie benutze ich LEDs?**
---
 &nbsp;
Your guests interact with Klangfarben through turning the record - randomised replay prevents the same songs playing over and over again. Different playlists are only distinguishable through colours, which could represent moods, genres, artists, or even memories you share with your friends. Let them play, guess the theme, and be surprised by that song they haven't heard in ages.


- Die LED wird an eine Energiequelle (z.B. Batterie) angeschlossen/gelötet

- LEDs benötigen eine bestimmte Durchlassungsspannung (*FV*) um zu leuchten
- Moderne LEDs sind unabhängig von ihrer Farbe alle mit einer *Durchlassspannung* von ca. *3,3 V* ausgestattet.
- Besitzt die Energiequelle eine höhere *Versorgungsspannung* als die LEDs benötigen (*Volt (V)*) :
-- schmort LED durch
- daher : Einbau von Widerstand (*Resistor*)
-- dieser lässt nur eine gewisse Zufuhr an Energie an die LED
-- z.B. von *12V* erreichen letztendlich *2V* die LED
- anhand der LED lässt sich erkennen was du verbinden musst, damit die Verbindung funktioniert:
-- Das Gehäuse ist auf einer Seite flach = *negative Seite*
-- Der Draht ist auf einer Seite länger = *positive Seite*
-- nun kann man die Drahtenden mit der richtigen Polarität an den Energieträger oder den *Strombegrenzungswiderstand* anschließen
- möglich : mehrere LEDs miteinander verknüpfen (*LED Strip*)
-- max. werden 3 LEDs aneinandergereiht
-- danach folgt das Widerstandselement
-- in dieser Abfolge lässt sich eine Kette bilden mit immer *3 LEDs und dem jeweiligen Strombegrenzungswiderstand* folgend

### So findet man den richtigen *Resistor* für die LEDs :
 &nbsp;
Wie bereits erwähnt, wird ein Strombegrenzungswiderstand benötigt, damit eine höhere Energiequelle nicht die LEDs durchschmort. Da es unterschiedliche Typen von LEDs auf dem Markt gibt, ist es essenziell herauszufinden, welchen Resistor für welche Art von LED verwendet werden muss, um eine erfolgreiche Energieweiterlung zu ermöglichen.
 &nbsp;

### Dazu kann man 2 Methoden verwenden :
##### - Die theoretische Methode mit Hilfe einer Berechnung
 &nbsp;
**R** = (Versorgungsspannung **VS** - LED-Durchlassspannung **VF**) / LED-Strom **I**
 &nbsp;
 - Hier ist R der fragliche Widerstand in Ohm

- Vs ist der Versorgungsspannungs-Eingang der LED
- VF ist die LED vorwärts, die tatsächlich die minimale Versorgungsspannung ist, die eine LED benötigt, um mit optimaler Helligkeit zu leuchten.
- LED-Strom oder I bezieht sich auf die Nennstromstärke der LED und kann je nach Spezifikation der ausgewählten LED zwischen 20 mA und 350 mA liegen. Dies muss in der Formel in Ampere umgerechnet werden, damit 20 mA zu 0,02 A, 350 mA zu 0,35 A usw. werden.

Hier wird dir die Berechnung abgenommen:
<https://leds-and-more.de/Widerstandsrechner>
 &nbsp;
##### - Die praktische Methode durch Erprobung
 &nbsp;
 Man braucht eine verstellbare/variable Energiequelle, verstellbarer/variabler Strombegrenzungswiderstand und natürlich LEDs :
 - zuerst stellt man das Energiegerät auf die Spannungszufuhr um, die man für seine Endenergiequelle nutzen möchte
 
- man schließt den *Resistor* an
- LED wird angeschlossen
- am Resitstor stellt oder erhöht man die Zufuhr, um zu erfahren, wann es ausschlägt und somit nicht tauglich für die LED ist 
 &nbsp;
---
### **3) Was ist mir unklar?**
---
 &nbsp;
- Die Methode zur Erprobung
- somit die Rollen/Unterschiede der verschiedenen Werte (Ampere, Ohm etc.)
 &nbsp;
