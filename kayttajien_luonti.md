# Käyttäjien luominen ja hallinnointi

Luodaan järjestelmään kaksi uutta käyttäjää. Toiselle käyttäjistä annetaan pääkäyttäjän oikeudet (sudo) ja toinen käyttäjä on tavallinen käyttäjä, jolla ei ole ylimääräisiä käyttöoikeuksia.


Käyttäjän luonti tapahtuu komennolla:
```
useradd -mc <käyttäjän_nimi> <käyttäjätunnus>
```
minkä jälkeen asetetaan salasana
```
passwd <käyttäjätunnus>
```

Tunnus pitäisi nyt näkyä tiedostossa `/etc/passwd` ja `/home´ hakemistosta pitäisi löytyä alihakemisto käyttäjätunnukselle. Lisäksi `/etc/shadow` tiedostossa käyttäjätunnuksen kohdalla pitäisi näkyä hashattu salasana. Jos siinä näkyy pelkästään `!!`. on salsana jäänyt asettamatta ja se täytyy tehdä ennen kuin siirrytään eteenpäin. 

Luodaan ensin tunnus käyttäjälle Anni Admini (aadmini), Anni toimii järjestelmän ylläpitäjänä ja tarvitsee sen mukaiset käyttöoikeudet. Anni tarvitsee siis `sudo` -oikeudet. Vilkaistaan tiedoston `/etc/sudoers` sisältöä, mistä havaitaan, että ryhmään **wheel** kuuluvilla on oikeudet ajaa mitä tahansa komentoja. Lisätään Annin käyttäjätunnus tähän ryhmään.
```
usermod -aG wheel <käyttäjätunnus> 
```
Tarkastetaan vielä, että käyttäjätunnus kuuluu ryhmään.
```
groups <käyttäjätunnus>
```

Toinen käyttäjä on Kikka Koodari (kkoodari). Kikka on ohjelmistokehittäjä, joka tarvitsee käyttöoikeuksia erinäisiin työkaluihin. Kikan käyttöoikeuksia tarkastellaan palveluiden asentamisen yhteydessä. Kikan käyttämiin työkaluihin kuuluu mm. python3, git, docker, tietokanta jne.

Sekä Anni että Kikka ottavat palvelimeen yhteydet ssh:lla. Nyt kun palvelimella on muita käyttäjiä, voidaan estää `root`ilta ssh:n käyttö. Editoidaan tiedostoa `/etc/ssh/sshd_config` etsitään rivi ´PermitRootLogin`ja vaihdetaan arvo `yes` arvoon `prohibit-password`. Tämän jälkeen palvelimeen ei voida enää ottaa ssh-yhteyttä `root`-tunnuksella. Otetaan vielä uudet asetukset käyttöön käynnistämällä ssh-daemon uudestaan
```
systemctl reload sshd
```

Tietoturvan lisäämiseksi voisi olla hyvä käyttää ssh-kirjautumisissa salasanan sijaan ssh-avaimia. Mutta palataan siihen myöhemmin, kun paneudutaan tarkemmin tietoturva-asioihin.



