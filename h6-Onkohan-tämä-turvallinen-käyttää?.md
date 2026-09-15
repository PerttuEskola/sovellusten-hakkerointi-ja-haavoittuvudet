# h6 Onkohan tämä turvallinen käyttää?


## Lähtöpiste
Miellä on käytössä tp link decrypt työkalu, jota hyödynnämme tehtävän teossa. Tehtävän materiaalista löytyy myös TapoV3 firmware binary ja Tapo C200 V3 dumb file.

Tehtävänä tutkia kameran ohjelmiston turvallisuutta ja käyttää siihen kurssilla opittuja menetelmiä.

### Tehtävät eriteltynä:

- Laiteohjelmiston salauksen purku
- Levykuvatiedoston analysointi
- Rootfs-osion purkaminen vedostiedostosta
- Rootfs-osion purkaminen levykuvatiedostosta
- Käytettävissä olevien sovellusten etsiminen
- Root-salasanan analysointi ja murtamisyritys

## Valmistelu

Kloonaamme tp link decrypt työkalun githubista suoraan omaan kansioon.

<img width="1560" height="186" alt="image" src="https://github.com/user-attachments/assets/38582646-b8c1-4796-ba32-2e5421c39042" />

Jonka jälkeen suoritamme työkalun mukana tulleet ohjeet. Ajetaan:

````bash
./preinstall.sh
````

Sen jälkeen voimme ladata materiaalesita löytyvän TapoV3 firmware binary ja dumb tiedostot.

<img width="1582" height="582" alt="image" src="https://github.com/user-attachments/assets/c5b600b8-f0c4-4d2b-950c-c1cfee85416f" />

Tämän jälkeen seuraamme ohjeita ja ajetaan:

<img width="832" height="106" alt="image" src="https://github.com/user-attachments/assets/701a0ae0-710f-4bb0-a504-564bd17033d5" />

Jonka jälkeen olemme valmiita suottamaan: 

<img width="1596" height="814" alt="image" src="https://github.com/user-attachments/assets/e312b2fc-2285-4094-9f66-f6d1ae78c68f" />

Tämä tuottaa meille ensimäisen virheen. Joten tunnila saimme virheen ohittamiseskei valmiin toimivan tiedoston.

Ladataan tiedosto ja puretaan se.

<img width="808" height="90" alt="image" src="https://github.com/user-attachments/assets/f046c107-87f6-4534-ac6e-f30169e7c7fb" />


Sisällä on jo make komennon onnistuneesti suoritettu tiedosto. Jota voimme käyttää.

<img width="1524" height="254" alt="image" src="https://github.com/user-attachments/assets/65e0fa22-dcdb-44f6-aa2c-8429640afbdc" />

Nyt voimme siirtya ensinmäiseen vaiheeseen.

### Salauksen purku

Ajetaan työkalu bin tiedostoon

<img width="1572" height="702" alt="image" src="https://github.com/user-attachments/assets/d53d7354-39c1-42a5-a99b-39021b5d56c6" />

Työkalu tekee tehtävänsä ja luo .dec tiedoston. Näemme myös Key ja IV jotka työkalu meille selvitti, ja salauksen purku onnistui. 

### Analysointi

Nyt voimme ajaa binwalk komennon äskeiseen .dec tiedostoon.

<img width="1572" height="826" alt="image" src="https://github.com/user-attachments/assets/0c64ed67-811b-4628-8da3-42dc60952bb5" />

Se luo paljon tekstiä jota tutkimalla voimme löytää asioita kuten:

- CPU: MIPS, Tämä kertoo kameran käyttämän laitteistoarkkitehtuurin.
- OS Kernel Image, Linux-3.10.14, Tämä kertoo kameran käyttämän Linux-version tarkalleen.
- Compression type: lzma, Tämä kertoo, miten kernel on pakattu
- Squashfs filesystem, little endian, version 4.0, Tämä kertoo minkä tyyppinen vain luku -tiedostojärjestelmä sisältää käyttöjärjestelmän ytimen.

### Rootfs-osio
Lisätään binwalk komentton -e joka purkaa binwalkissa saadut tiedot kansioihin.

<img width="920" height="208" alt="image" src="https://github.com/user-attachments/assets/40c33484-a056-4d39-b72d-89e989ae24ef" />

Suoritamme komennon myös dumb teidostoon.

<img width="1036" height="144" alt="image" src="https://github.com/user-attachments/assets/5112f4b7-2a8f-4a70-90d3-4ac92e55ddb9" />


Teemme tämän myös dumb tiedostolle.

Tämän jälkeen molemmat antavat varoituksia ja kertovat joidenkin kansioiden purun epäonnistuneen. Tätä yritin korjata tuloksetta.

### Sovellusten etsiminen
Kun alamme etsiä sovellussia. Löydämme:

- gdbserver, etädebuggaustyökalu, jota kehittäjät käyttävät.
- iperf, verkon suorituskyvyn mittaamiseen tarkoitettu työkalu.
- main, lähes varmasti Tapon ensisijainen sovellus.
- fatlabel, fsck.fat, mkfs.fat, käytetään kameran käyttäjän laitteeseen liittämän MicroSD-kortin alustamiseen, tarkistamiseen ja nimeämiseen paikallista tallennusta varten.
- hostapd, (Host Access Point Daemon) mahdollistaa sen, että kamera toimii Wi-Fi-reitittimenä.
- BusyBox, on yksi suoritettava tiedosto ja sisältää pienikokoiset versiot monista yleisistä UNIX-apuohjelmista tilan säästämiseksi.

Muita havaintoja: Molemmat dumb sekä laiteohjelmiston binääri tiedosto antavat täysin saman tuloksen binwalk -e komentoon. Jostain syystä se ei anna enempää kansioita, joka estää syvemmän tutkimisen.

### Root-salasana

Tässä vaiheessa olisi olut mahtavaa saada käsiin tunnilla nähdyt shadow ja pssswd tiedostot, joita nyt emme jostain syystä emme saa. 
Tunnilla nähdyn esimerkin ja jäänen käsityksen mukaan salasanat olisivat mahdollisesti löytyneet ``etc/shadow`` tiedostosta `$1$` tai `$5$` alkavilla syötteillä. 
Joihin olisi mahdolista ollut käyttä JohnTheRipper tai HashCat työkaluja salasanan selvittämiseen.

## Lähteet

- Tekoälyä käytetty tunnilla ja kotona tehtävän selvittämiseen.
- https://askubuntu.com/questions/25347/what-command-do-i-need-to-unzip-extract-a-tar-gz-file
- https://claude.ai/
- https://gemini.google.com/
