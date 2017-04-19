---
layout: post
title: Creació LiveUSB de WifiSlax - Guia Bàsica
---

En primer lloc, caldrà descarregar l'última versió de la imatge .iso de la distribució. Ho podeu fer des dels següents enllaços: [64 bit](http://www.wifislax.com/category/wifislax-64bits/download-wifislax-x64/) / [32bit](http://www.wifislax.com/category/download/versiones-anteriores/)

Necessitarem un pendrive USB de 4GB com a mínim.

A continuació veiem com podem crear el LiveUSB des de diferents sistemes operatius.

## Windows
Des de sistemes Windows, podem crear el LiveUSB amb l'eina de software lliure Rufus, que es pot descarregar des del següent enllaç: <https://rufus.akeo.ie/downloads/rufus.exe>

A l'apartat *Device* cal seleccionar la unitat on es troba el pendrive USB. A la casella *Create a bootable disk using* trieu ISO Image, i seleccioneu el fitxer .iso que heu descarregat. La resta de paràmetres haurien de funcionar sense problema tal com estan per defecte. Doneu a *Start* i ja només cal esperar que acabe.

## GNU/Linux
Usarem la utilitat *dd* característica dels sistemes UNIX.

Per descobrir en quina unitat tenim el nostre pendrive USB usarem la comanda

*lsblk*

que retornarà una llista jeràrquica de possibles unitats (en general, de la forma sdX, amb X minúscula). Per assegurar-nos quin és el nostre USB, podem executar la comanda just abans i just després de connectar-lo.

Quan el tinguem localitzat, si aquest té alguna partició creada (sdX1, per exemple) caldrà assegurar-nos que estiga desmuntada. Per fer-ho, executem

*umount /dev/sdXn*

Ara ja podem usar *dd* per a copiar els arxius de la .iso l'USB amb

*sudo dd if=/path/to/file/filename.iso of=/dev/sdX bs=4M*

I un cop haja acabat, ens assegurem que haja carregat tots els buffers pendents amb

*sync*

### Boot

Un cop fet això, només caldrà modificar la BIOS de l'ordinador indicant-li que arranque des del pendrive USB que acabem de crear.
