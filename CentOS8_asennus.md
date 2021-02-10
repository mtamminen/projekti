# CentOS8 virtuaalikoneen asennus

1. Haetaan asennusmedia:
* [https://www.centos.org/download/](https://www.centos.org/download/)
* valitaan ISO: x86_64
* valitaan joku ehdotetuista mirroreista
* ladataan tiedosto: *-x86_64-dvd1.iso

2. Käynnistetään VMWare Pro
* Valitaan File-valikosta: New Virtual Machine
* Valitaan avautuvasta ikkunasta jompikumpi vaihtoehto (oletus:typical)
* Aktivoidaan Installer disk image file (iso)
* Painetaan Browse ja etsitään edellä ladattu iso-tiedosto järjestelmästä
* Jatketaan eteenpäin VMWaren ehdottamilla arvoilla
* Finish

3. Käynnistetään kone klikkaamalla Power On this Virtual Machine

4. Valitaan Install CentOS Linux 8 

5. Hetken kuluttua avatuu näkymä, jossa valitaan asennusprosessin kieli (oletus: English (US)). Valitaan haluttu kieli ja jatketaan.

6. Seuraavassa näkymässä päästään tekemään asetuksia.
* Keyboard: lisätään suominäppäimistö ja nostetaan se ylimmäksi vaihtoehdoksi (valintaikkunan alalaidassa olevilla nappuloilla voidaan lisätä ja poistaa vaihtoehtoja ja järjestää niitä).
* Language support: oletus English
* Time & Date: valitaan aikavyöhyke (Europe/Helsinki)
* Root password: Asetetaan rootille salasana
* Installation source: Auto-detect installation media pitäisi olla valittuna.
* Software selection: valitaan vasemmalta Minimal install ja oikealta System tools
* Installation destination: valitaan VMware Virtual S..., Storage configuration Automatic
* KDUMP: oletuksena käytössä, annetaan olla
* Network & hostname: laitetaan verkko päälle. ei muita muutoksia.
* Security Policy: annetaan olla kuten on

7. Begin Installation -> asennus alkaa 
