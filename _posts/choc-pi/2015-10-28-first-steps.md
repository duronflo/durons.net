---
title: Erste Schritte mit dem Chocolate Pi
permalink: /projects/chocolate-pi/first-steps-chocolate-pi
categories: [ChocolatePi, Do-it-your-self]
tags: [Raspberry-Pi, Audio]
project: choc-pi
---

## Einleitung


Hierbei ging es mir einen aktiven Lautsprecher für die Küche. Ich koche sehr gerne und wollte ich schon immer etwas schickes, 
was ich auch von der Ferne aus steuern kann. Daraus ist folgende Lautsprecher-Box entstanden.
 
 
 Sie kann entweder mit einem AUX-Kabel betrieben oder Remote mit Hilfe eines Smartphones. Für den Remotezugriff habe ich 
 einen Raspberry Pi verbaut, welcher die komplette Netzwerkfunktionalität bereitstellt. Die Vorderseite ist bestückt mit 
 einem Drehpoti zum Einstellen der perferkten Lautstärke einer Status-LED und einem Taster. Auf der Rückseite des Geräts 
 befinden sich ein AUX-Eingang, der Netzstecker und ein USB-Device für Software-Updates aber auch als Datenquelle für 
 Musik.
 

Hierbei ging es mir einen aktiven Lautsprecher für die Küche. Ich koche sehr gerne und wollte ich schon immer etwas schickes,
was ich auch von der Ferne aus steuern kann. Daraus ist folgende Lautsprecher-Box entstanden.

Sie kann entweder mit einem AUX-Kabel betrieben oder Remote mit Hilfe eines Smartphones. Für den Remotezugriff habe ich einen 
Raspberry Pi verbaut, welcher die komplette Netzwerkfunktionalität bereitstellt. Die Vorderseite ist bestückt mit einem Drehpoti 
zum Einstellen der perferkten Lautstärke einer Status-LED und einem Taster. Auf der Rückseite des Geräts befinden sich ein AUX-Eingang, 
der Netzstecker und ein USB-Device für Software-Updates aber auch als Datenquelle für Musik.


Hier werde ich kurz erklären wie man auf dem Raspberry Pi mit Rasbian den Logitech Media Server (LMS) installiert. Außerdem wird 
anhand von softsqueeze demonstriert wie man den Raspberry Pi auch als LMS-client verwenden kann, dazu noch ein Hifiberry Soundmodul 
mit in die Umgebung eingebunden. Die Client-Installation kann auch auf andere Raspberry Pi Clients übertragen werden.

## Vorgehensweise / Installation

Offizielles Raspbian-Image herunterladen bei www.raspberrypi.org

Einstellungen können mit rpi-config vorgenommen werden (Dateisystem muss ausgeweitet werden!)

Server-Installation von LMS

Download von LMS auf der Logitech Homepage. Ich habe den letzten nightly build  von der Version 7.8 verwendet und funktioniert 
bisher einwandfrei. Man muss hier bei den Versionen bisschen aufpassen. Logitech verfolgt folgende Philosophie. 7.7 ist stabil 
und offiziell, 7.8 stabil aber nicht offiziel, 7.9 unstabil. Danach wird das Debian-Paket ganz normal mit dem dpkg-Dienst installiert.

Der LMS Server trägt sich automatisch in das Runlevel-2 der Startroutinen ein. Er kann händisch wie folgt gestartet (start) bzw. 
gestoppt (stop) werden /etc/init.d/logitechmediaserver start Client-Intstallation squeezelite für LMS-Serveror:


Treiber-Installation für Hifiberry DAC/DIGI+