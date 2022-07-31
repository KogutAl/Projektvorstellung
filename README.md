# Klangfarben
#### (*Ein Projekt von Lisa Umlauft,Alexander Konrad und Janina D. Lettow*)
 &nbsp;

![Bild zeigt Hand die Apparatur nutzen](https://mir-s3-cdn-cf.behance.net/project_modules/disp/44c08617327583.562b89aa4da9f.jpg)

---
### **Konzept**
---
Kreiere eine Playlist, weise Farben hinzu und kombiniere bis zu 8 von diesen auf einer kleinen Disc mit RFID tags.


- Technologie für Sender-Empfänger-Systeme
- kontaktlose Lokaliserung und Übermittlung von Daten
- Senden durch Antenne oder Mikrochip
- Senden durch integrierte Schaltung (IC) möglich
- Mikrochip wird mit den gewünschten Daten beschrieben
 &nbsp;
---
### **2) Wie funktioniert Klangfarben?**
---

Man erstellt Playlist-Themes und ordnet diesen bestimmte Farben zu. Z.B. nostalgische Songs werden *blau*, Entspannung wird durch die Farbe *grün* repräsentiert.
Durch drehen des "Records" werden Songs abgespielt. "Zufälliges Replay" verhindert hier das ständige Wiederholen der selben Songs.
Ziel ist das Zufällige Abspielen von Liedern und eine Untermalung der Atmosphäre durch die Farblichter.

 &nbsp;
[Hier mehr über das Projekt erfahren](https://www.behance.net/gallery/17327583/Klangfarben?tracking_source=search_projects_recommended%7Cphysical%20computing)

 &nbsp;
---
# Emotion Sensing
#### (*Ein Projekt von Abijeet Pol und Midhu S. Valsan*)
 &nbsp;
 
 
![Das Konzept des Gerätes in Form eines Gramophons](https://mir-s3-cdn-cf.behance.net/project_modules/1400_opt_1/0fba0733332439.56a8df1ca9c53.jpg)
 
---
### **Konzept**
---
Ein Apparat, welches Emotionen erkennt und dazu passende Musik abspielt. Aussehen soll dieses wie ein Gramophon, in dessen Box sich der Motor befindet und Sensoren innerhalb des Zylinderschafts, welches zum Ausgabekörper führt.
Der User muss seine Hand in die Apparatur stecken, wobei es für jeden Finger ein seperater Slot vorgesehen ist. In jedem dieser Slots befindet sich ein Sensor.
Ein LCD- Bildschirm zeigt die Ermessene Emotion an.
 &nbsp;
 
---
### **2) Komponenten?**
---

 **Galvantic Skin Response**
 - misst die elektrodermale Aktivität = kurzzeitiges Absinken des elektrischen Leitungswiderstandes der Haut
 - d.h. erhöhter Scheißausstoß der Haut durch bpsw. Stressempfinden
 - die Leitfähigkeit der Haut wird erhöht

 **Heartbeat Sensor**
 - misst die Herzfrequenz

 **Heat Sensor**
 - misst die Körpertemperatur


 **Bluetooth Modul**
 - zur Übermittlung der Daten an einen Computer

 &nbsp;
[Hier mehr über das Projekt erfahren](https://www.behance.net/gallery/33332439/Physical-Computing?tracking_source=search_projects_recommended%7Cphysical%20computing)

 &nbsp;
---
# Neopixel LED Mirror
#### (*Ein Projekt von User "Super Make Something"*)
 &nbsp;

![Personenabbild wird mit LEDs wiedergegeben](https://user-images.githubusercontent.com/105751118/181501305-6d31a85a-d7c0-442f-84c8-39da03c55ec0.png)

---
### **Konzept**
---

Mit Hilfe von 3D Druck, Laser Cutting, einem Raspberry Pi, computerbasiertes Sehen (computer vision) und circa 600 Neopixel LEDs wurde ein low resolution LED Spiegel gebaut, welches das Abbild des Betrachters auf einem 9mx9m großem Grid mit 24x24 RGB LEDs, dargestellt wird.
Dieses Projekt hat bis zur Fertigstellung 2 Jahre in Anspruch genommen un wurde auf der "Cleveland Maker Faire" 2019 in Ohio ausgestellt.
 &nbsp;
 
---
### **Komponenten**
---

- 1x Raspberry Pi 3 B
- SD Karte
- 1x Raspberry Pi Hülle
- 1x Raspberry Pi Kamera
- 1x Kameraflachbandkabel
- 1X PCB Prototyp Brett
- 36x36 cm Holzhintergrund
- 24x NeoPixel LED Streifen mit jeweils 24 LEDs
- 576x durchsichtige LED-Überdeckungen aus 3D Druck
- 16x Monategitter (laser cut)
- 1x 5V 30A Energiequelle
- 1x PC Netzkabel


 &nbsp;
 
---
### **Der Code - ** [Seperater Git-Link](https://github.com/SuperMakeSomething/neopixel-led-mirror)
---

#!/usr/bin/env python3
**coding: utf-8**
"""
Neopixel LED Mirror Image Display Code (Neopixel LED Mirror - Super Make Something Episode 20) - https://youtu.be/Ew0HmLy_Td8
by: Alex - Super Make Something
by: Alex - Super Make Something
date: November 18, 2019
license: Creative Commons - Attribution - Non Commercial.  More information at: http://creativecommons.org/licenses/by-nc/3.0/
description: This script loads a desired image and displays it on the Neopixel Mirror
"""

**Import required libraries**
from PIL import Image
import numpy as np
import board
import neopixel

def extractROI(image,windowSize):
    
    imWidth, imHeight = image.size
    roiImage = image.resize((windowSize[0],windowSize[1]))

    return roiImage

def discretizeImage(roiImage,noLevels):

    image=np.array(roiImage)#Image.fromarray(roiImage,'RGB')
    normalizedImage=image/255
    discretizedImage=np.floor(normalizedImage*noLevels).astype(int)
    multiplier=255/noLevels
    discretizedImage=np.floor(discretizedImage*multiplier).astype(np.uint8) #Rescale to range 0-255
    return discretizedImage

def imageToLED(discreteImageRaw,pixels):
    
    discreteImageR=discreteImageRaw[:,:,0]
    discreteImageG=discreteImageRaw[:,:,1]
    discreteImageB=discreteImageRaw[:,:,2]
    discreteImageR=discreteImageR.flatten()
    discreteImageG=discreteImageG.flatten()
    discreteImageB=discreteImageB.flatten()
    pixelArray=np.zeros((len(discreteImageR),3))
    pixelArray[:,0]=discreteImageR
    pixelArray[:,1]=discreteImageG
    pixelArray[:,2]=discreteImageB
    pixelArray=(pixelArray).astype(int)# Convert to int
    pixelTuple=[tuple(x) for x in pixelArray] #Convert to correctly dimensioned tuple array
    pixels[:]=pixelTuple
        
    return pixels
    
#Parameters
noLevels=255 #No of LED brightness discretization levels
numNeopixels_x = 24 #Declare number of Neopixels in grid
numNeopixels_y = 24
windowSize=(numNeopixels_x,numNeopixels_y) #Define extracted ROI size


pixelPin=board.D18
numPixels=numNeopixels_x*numNeopixels_y
colorOrder = neopixel.GRB
pixels = neopixel.NeoPixel(pixelPin, numPixels, auto_write=False, pixel_order=colorOrder)

while 1:
    newImage = Image.open('yoshi.png')
    newImageROI = extractROI(newImage,windowSize) #Extract base image ROI
    discretizedImage=discretizeImage(newImageROI,noLevels) #Discretize image and scale values   
    pixels=imageToLED(discretizedImage,pixels) #Convert the image to an LED value array and assign them to the string of Neopixels
    pixels.show() #Light up the LEDs


[Hier mehr über das Projekt erfahren](https://blog.adafruit.com/2019/12/27/neopixel-led-mirror-python-raspberry-pi-arduino-3d-printing-laser-cutting-diy-how-to-raspberry_pi-piday-raspberrypi/)
 &nbsp;
 
[Hier der Projektverlauf auf Youtube](https://www.youtube.com/watch?v=Ew0HmLy_Td8)


 &nbsp;
---
# RGB Sensor Project
#### (*Ein Projekt von User "thinklearndo"*)
 &nbsp;

![Sensor und RGB Stern](https://cdn-blog.adafruit.com/uploads/2022/07/Untitledx-58.png)

---
### **Konzept**
---

Ein auf Distanz basierendes Farbwechsel-Projekt. Drei Sonar Sensoren messen den Abstand von Objekten zum jeweiligen Sensor, bei dem der gemessene Abstand jedes einzelnen Sensors, auf einem anderen Farbkanal korrespondieren.

 &nbsp;
 
---
### **Komponenten**
---

- 3x Sonar Sensoren
- 1x Arduino uno
- 1x ws2812b rbg led
- Anschlussdrähte
- 3d gedruckte Hülle und Stern
- Heißklebepistole

 &nbsp;

 
---
### **Schaltplan und Verbindung**
---
 &nbsp;

![Schaltplan](https://raw.githubusercontent.com/thinklearndo/rgb_distance/main/images/circuit_layout.png)

 &nbsp;
 
"Splice hook up wires for voltage and ground for all the components. Or use a Breadboard to hook up voltage and ground power rails.

Hook up the 3x sensors according to the diagram.

Hook up the ws2812b rgb led according to diagram.

Flash Aruino with code.

Insert sonar sensors into case and use glue gun to affix them.

Insert ws2812b rgb through top square hole in case and use glue gun to glue it to case."

 &nbsp;

[Eine ausführliche Git-Doku](https://github.com/thinklearndo/rgb_distance)

 &nbsp;
---
# Mini GIF Player
#### (*Ein Projekt von User "Ruiz Brothers"*)
 &nbsp;

![Kleine Bildschirme auf dem GIFs abgespielt werden](https://i.ytimg.com/vi/G8YGo2eVU8M/maxresdefault.jpg)

---
### **Konzept**
---

Mit Hilfe von CircuitPython und Ardunio entstanden diese kleinen GIF Player. 
Diese 3D gedruckten Gehäuse wurden optisch dem dem Vorbil eines Retro Fernsehers und eines tragbaren Gaming Konsole entworfen, welche GIFs abspielen können.
Dieses Projekt nutzt CircuitPythons USB Massenspeicher Kapazität um eine Flas Drive zu imitieren, damit GIFs einfach per Drag & Drop übernommen werden können.

 &nbsp;
 
---
### **Komponenten**
---

- Adafruit Feather RP2040
- Adafruit 1.47" 320x172 Round Rectangle Color IPS TFT Display
- Lithium Ion Polymer Battery with Short Cable - 3.7V 420mAh
- Breadboard-friendly SPDT Slide Switch
- Adafruit 1.9" 320x170 Color IPS TFT Display
- 1 x USB Cable A to C
- 8 x M2.5x6mm Schrauben
 &nbsp;
 
---
### **Schaltplan und Verbindung**
---
 &nbsp;

![Schaltplan für 1.47 Display](https://cdn-learn.adafruit.com/assets/assets/000/112/142/large1024/projects_1.4_CircuitPython-feather2040-fritz.jpg?1653935309)

Die Kreatoren weisen darauf hin, dass Drähte abgemessen und so abgeschnitten werden sollten, dass noch genügend Material übrig ist, um die einzelnen Komonenten zu verbinden.

Sie nutzen Silikonbanddraht, da dieser einfach zu biegen und drehen ist, was in solch einem kleinen Raum sehr wichtig ist für eine möglichst angenehme Handhabung ist.


 &nbsp;

[Das Projekt](https://learn.adafruit.com/mini-gif-players/)
 &nbsp;
 
[Das Zusammenbauen](https://learn.adafruit.com/mini-gif-players/assemble)
 &nbsp;

[Das Programmieren](https://learn.adafruit.com/mini-gif-players/coding-the-mini-gif-players)
 &nbsp;
