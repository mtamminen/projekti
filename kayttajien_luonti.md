# Käyttäjien luominen ja hallinnointi

Luodaan järjestelmään kaksi uutta käyttäjää. Toiselle käyttäjistä annetaan pääkäyttäjän oikeudet (sudo) ja toinen käyttäjä on tavallinen käyttäjä, joka saattaa tarvita oikeuksia tiettyjen palveluiden käyttöön työssään.

Aloitetaan käyttäjän luominen luomalla ensin käyttäjälle salasana. Salasanan pituus on 16 merkkiä ja se tallennetaan tiedostoon.
```
pwmake 16 > <tiedoston_nimi>
```

Luodaan käyttäjätunnus
```
useradd -mc "Etunimi Sukunimi" <käyttäjätunnus>
```
Optio `-m` luo käyttäjälle kotihakemiston, `-c` lisää kommenttikentän, jossa yleensä on käyttäjän nimi.

minkä jälkeen asetetaan salasana
```
cat <salasanatiedosto> | passwd --stdin <käyttäjätunnus>
```
ja lopuksi vielä pakotetaan käyttäjä vaihtamaan salasana ensimmäisellä kirjautimisella.
```
passwd -e <käyttäjätunnus>
```
Tunnus pitäisi nyt näkyä tiedostossa `/etc/passwd` ja `/home` hakemistosta pitäisi löytyä alihakemisto käyttäjätunnukselle. Lisäksi `/etc/shadow` tiedostossa käyttäjätunnuksen kohdalla pitäisi näkyä hashattu salasana. Jos siinä näkyy pelkästään `!!`, on salasana jäänyt asettamatta ja se täytyy tehdä ennen kuin siirrytään eteenpäin. 

Luodaan ensin tunnus käyttäjälle Anni Admini (aadmini), Anni toimii järjestelmän ylläpitäjänä ja tarvitsee sen mukaiset käyttöoikeudet. Anni tarvitsee siis `sudo` -oikeudet. Vilkaistaan tiedoston `/etc/sudoers` sisältöä, mistä havaitaan, että ryhmään **wheel** kuuluvilla on oikeudet ajaa mitä tahansa komentoja. Lisätään Annin käyttäjätunnus tähän ryhmään.
```
usermod -aG wheel <käyttäjätunnus> 
```
Tarkastetaan vielä, että käyttäjätunnus kuuluu ryhmään.
```
groups <käyttäjätunnus>
```

Toinen käyttäjä on Kikka Koodari (kkoodari). Kikka on ohjelmistokehittäjä, joka tarvitsee käyttöoikeuksia erinäisiin työkaluihin. Kikan käyttöoikeuksia tarkastellaan palveluiden asentamisen yhteydessä. Kikan käyttämiin työkaluihin kuuluu mm. python3, git, docker, tietokanta jne.

Sekä Anni että Kikka ottavat palvelimeen yhteydet ssh:lla. Nyt kun palvelimella on muita käyttäjiä, voidaan estää `root`ilta ssh:n käyttö. Editoidaan tiedostoa `/etc/ssh/sshd_config` etsitään rivi `PermitRootLogin`ja lisätään rivin eteen `#` (ottaa käyttöön oletusasetuksen). Tämän jälkeen palvelimeen ei voida enää ottaa ssh-yhteyttä `root`-tunnuksella. Otetaan vielä uudet asetukset käyttöön käynnistämällä ssh-daemon uudestaan
```
systemctl reload sshd
```

Tietoturvan lisäämiseksi voisi olla hyvä käyttää ssh-kirjautumisissa salasanan sijaan ssh-avaimia. Mutta palataan siihen myöhemmin, kun paneudutaan tarkemmin tietoturva-asioihin.

Jatkokehitys: käyttäjien luonnin automatisointi (käyttäjätunnuksen generointi nimitiedoista yms.), mietittävä myös miten tunnukset ja salasanat toimitetaan käyttäjille tietoturvallisesti.
