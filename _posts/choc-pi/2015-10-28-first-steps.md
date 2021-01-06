---
title: Installation Spotify
permalink: /projects/chocolate-pi/spotify-chocolate-pi
categories: [ChocolatePi, Do-it-your-self]
tags: [Raspberry-Pi, Audio]
project: choc-pi
---

## Vorgehensweise / Installation Spotify

Offizielles Raspbian-Image herunterladen bei www.raspberrypi.org

Einstellungen können mit rpi-config vorgenommen werden (Dateisystem muss ausgeweitet werden!)

Server-Installation von LMS

Download von LMS auf der Logitech Homepage. Ich habe den letzten nightly build  von der Version 7.8 verwendet und funktioniert 
bisher einwandfrei. Man muss hier bei den Versionen bisschen aufpassen. Logitech verfolgt folgende Philosophie. 7.7 ist stabil 
und offiziell, 7.8 stabil aber nicht offiziel, 7.9 unstabil. Danach wird das Debian-Paket ganz normal mit dem dpkg-Dienst installiert.

Der LMS Server trägt sich automatisch in das Runlevel-2 der Startroutinen ein. Er kann händisch wie folgt gestartet (start) bzw. 
gestoppt (stop) werden /etc/init.d/logitechmediaserver start Client-Intstallation squeezelite für LMS-Serveror:


Treiber-Installation für Hifiberry DAC/DIGI+