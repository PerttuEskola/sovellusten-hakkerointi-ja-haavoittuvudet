# h2 Break & Unbreak

## x)

OWASP: OWASP Top 10:
- Pääsynhallinta pettää, jos järjestelmä ei kunnolla varmenna, onko käyttäjällä todellisuudessa oikeus pyytämäänsä tietoon tai toimintoon.
- Puutteellinen pääsynhallinta on edelleen kyberturvallisuuden yleisin ja vakavin web-haavoittuvuus OWASP Top 10 -listauksessa vuonna 2025.

Karvinen 2023:
- ffuf-työkalua käyetetään verkkosivujen piilotettujen hakemistojen ja tiedostojen etsimiseen.
- Piilosivujen etsimisessä käytetään valmiita sanakirjoja, joita työkalu käy automaattisesti läpi testaten mahdollisia osoitteita.
  
PortSwigger:
- Access control määrittää, mitä resursseja ja toimintoja vahvistetut käyttäjät saa käyttää.
- Suojaukset voivat pettää esimerkiksi silloin, kun oikeuksia hallitaan manipuloitavissa olevilla parametreilla, tai kun piilotettujen sivujen oletetaan olevan turvassa vain siksi, ettei niihin ole suoria linkkejä.

Karvinen 2006:
- Raportin tulee olla niin tarkka, että kuka tahansa voi toistaa kokeen samassa ympäristössä ja saada saman tuloksen.
- Kerro tarkalleen, mitä komentoja annoit, mitä tapahtui ja millä testillä totesit onnistumisen.
## a)

Ladataan zip ja puretaan se.

<img width="1094" height="146" alt="image" src="https://github.com/user-attachments/assets/c53a00f3-faeb-4ac0-955a-a4b3d1dbd45c" />

Avataan sovellus ``python3 staff-only.py`` komennolla`.
<img width="1570" height="314" alt="image" src="https://github.com/user-attachments/assets/cf2e15a6-9475-46d9-a4dc-380274c041d9" />

Ja sieltä löytyvä osoite selaimeen.

<img width="952" height="386" alt="image" src="https://github.com/user-attachments/assets/3a7fb0e5-90c2-4dfd-9240-a77c8f7416ef" />

Laitetaan selaimeen ohjeista löytynyt salasana 123, joka antaa meille viestin ``Your password is Somedude``, ja huomataan että kenttä ei hyväksy tekstiä.

<img width="442" height="286" alt="image" src="https://github.com/user-attachments/assets/ef21ebd4-ef64-44c5-be1d-396262d0e39f" />

Löydämme tämän kun tutkimme sivua selaimen F12 kehittäjän työkalujen kautta.

<img width="488" height="200" alt="image" src="https://github.com/user-attachments/assets/341f4018-3a45-494c-9bef-364a1e969738" />

Ja voimme vaihtaa sen tekstiksi.

<img width="490" height="224" alt="image" src="https://github.com/user-attachments/assets/9cf88a0c-5a20-49ac-b2a6-6eef02128a42" />

Nyt voimme koittaa antaa salasanaa uudestaan.

<img width="708" height="368" alt="image" src="https://github.com/user-attachments/assets/9e11ad10-7b62-4355-b313-b1dbd172b9cb" />

Ja sivu antaa (not found).

Seuraavaksi kokeilin laittaa pelkän ``'``. Se antoi Internal Server Error joka on vihje sivun tietoturvahaavoittuvuudesta.

<img width="1284" height="274" alt="image" src="https://github.com/user-attachments/assets/0c8a8c45-30bb-4ccf-8e2e-3b7174273913" />

Kokeilin salasana kenttään ``foo' OR 1=1--``. Joka antoi vastaukseksi ``foo``.

<img width="892" height="364" alt="image" src="https://github.com/user-attachments/assets/00428833-ee3c-4620-9c0b-37544270cb57" />

Kun lisäsimme syötteeseen ``LIMIT 2,1--``.

<img width="954" height="378" alt="image" src="https://github.com/user-attachments/assets/5e61e2f8-79ec-48ce-b49a-5b99678af111" />

Antaa sivu vastaukseksi admin salasanan: ``SUPERADMIN%%rootALL-FLAG{Tero-e45f8764675e4463db969473b6d0fcdd}``

<img width="954" height="378" alt="image" src="https://github.com/user-attachments/assets/7f26f5b1-b1c7-49b5-91e7-9fada618559e" />


## b)
Korjaamista varten voimme avata koodin ``nano staff-only.py``.

Löydämme koodista virheen seuraavasta kohdasta. 

<img width="868" height="180" alt="image" src="https://github.com/user-attachments/assets/6b5179ea-fb71-4554-95a0-3c18faf93808" />

Ja voimme korjata sen muokkaamalla seuraavat kohdat.

<img width="765" height="156" alt="image" src="https://github.com/user-attachments/assets/a9d7cbf4-5e25-443c-aed4-37990581ba83" />

Kun sivia testataan uudelleen samalla tavalla se ei anna enää admin salasanaa.

<img width="680" height="382" alt="image" src="https://github.com/user-attachments/assets/fe2c6dca-56da-4d63-b310-7cc18137e0f5" />


## c) 
Ladataan ensiksi ffuf työkalu ja common.txt joka sisältää sanalistan työkalua varten.

ffuf

<img width="946" height="316" alt="image" src="https://github.com/user-attachments/assets/7c95d58e-db8d-48c3-bab5-ccadb830c6dc" />

Ja common.txt

<img width="2228" height="608" alt="image" src="https://github.com/user-attachments/assets/d32df50d-2e92-4564-ad19-180d0e8e1950" />

Sitten aloitettiin muuttamalla tehtävä tiedostoon oikeudet ja ajettiin se.

<img width="268" height="158" alt="image" src="https://github.com/user-attachments/assets/d054393c-bc68-42ea-b537-78ab76ea5c01" />

Selain antaa seuraavanlaisen sivun

<img width="676" height="200" alt="image" src="https://github.com/user-attachments/assets/3f75b597-1202-4325-854e-382f2f6cde8a" />

Käytetään ffuf työkalua ohjeen mukaisesti ja se antaa ensinmäiseen komentoon ``ffuf -w common.txt -u http://127.0.0.2:8000/FUZZ`` seuraavanlaista listaa.

<img width="1638" height="1440" alt="image" src="https://github.com/user-attachments/assets/fc1141ef-11bf-4d98-94b1-e9a3b246704e" />

Lista on aivan liian pitkä joten voimme antaa erilaisia komentoja syötteen hallinoimiseen.

Lisäämme perään ohjeista löydetyn ``-fs 132`` mutta lista on edelleen liian pitkä joten yritämme jotain muuta.

``-fs 154`` Lisääminen antaa meille halutun tuloksen ja voimme suoraan löytää sieltä Admin sivun ja versionhallintaan liittyvän sivun. ``wp-admin`` ja ``.git``

<img width="1744" height="1282" alt="image" src="https://github.com/user-attachments/assets/7f74bca9-0dee-4fba-9a28-f2751e749b56" />

Molemmat sivut antavat meille vastauksen.

<img width="754" height="320" alt="image" src="https://github.com/user-attachments/assets/c8cfd984-f940-43f5-b9b1-c46efa19c2c2" />

<img width="644" height="332" alt="image" src="https://github.com/user-attachments/assets/e128b9a3-6ad5-4ffe-81de-a84b8951cc2e" />

## d) 

Aloitamme luomalla meille virtuaalinen tehtävä ympäristö.

Siirrytään tehtävä hakemistoon ja asennetaan virtualenv.

<img width="1184" height="268" alt="image" src="https://github.com/user-attachments/assets/98c43e48-a9d8-4471-9816-5748c476b7ff" />

Tehdään seuraavat komennot. ``virtualenv virtualenv/ -p python3 --system-site-packages``, ``source virtualenv/bin/activate``

<img width="2658" height="386" alt="image" src="https://github.com/user-attachments/assets/2781f030-2561-47c8-b4bb-239a0ea9e8b0" />

<img width="1128" height="106" alt="image" src="https://github.com/user-attachments/assets/c777e6bc-386c-40c9-8513-714dae627c1a" />

Seuraavaksi asennetaan django 

<img width="1366" height="728" alt="image" src="https://github.com/user-attachments/assets/197f8974-6a77-4040-8456-43c0a83d01a4" />

ja seuraavat komennot  ``./manage.py makemigrations; ./manage.py migrate``
<img width="1514" height="306" alt="image" src="https://github.com/user-attachments/assets/a33c106f-fdc8-4b2b-a792-2bb3db0886b2" />

ja nyt voimme käynnistää verkkosivun ``./manage.py runserver``

<img width="1508" height="442" alt="image" src="https://github.com/user-attachments/assets/4f93c3ce-ed18-483a-8a9e-5bbb06e6debb" />

Sivu näyttää tältä

<img width="1264" height="696" alt="image" src="https://github.com/user-attachments/assets/6c30edfe-5ddd-4f30-b989-df53e11212cf" />

Voimme aloittaa tutkimalla sitä ja huomaamme käyttäjän luomisen ja kirjautumisen jälkeen että pääsemme My data sivulle mutta Admin dashboard antaa virheen.

<img width="992" height="352" alt="image" src="https://github.com/user-attachments/assets/c4f82d39-6144-4046-b5a6-8d71c306d980" />

<img width="648" height="246" alt="image" src="https://github.com/user-attachments/assets/fa1efa68-51a0-45f5-a379-ac40f8f96a74" />

Seuraavaksi voimme aloitaa ffuf työkalun käytön, hetken selailun jälkeen huomaamme että komento ``ffuf -w common.txt -u http://127.0.0.1:8000/FUZZ -t 10`` antaa meille vastauksen.

<img width="1878" height="1032" alt="image" src="https://github.com/user-attachments/assets/e9287b5d-fd40-4059-ace9-61c3a72e39c8" />

admin-console sivu oli oikea ratkaisu

<img width="726" height="300" alt="image" src="https://github.com/user-attachments/assets/06b1b1b4-55ce-4481-8059-9ef0e5b51884" />

## e)
Seuraavaksi lähdimme korjaamaan sivua. Lähdin etsimään tehtävä kansiosta.

views.py löydämme seuraavaa.

<img width="1910" height="864" alt="image" src="https://github.com/user-attachments/assets/044a7064-9030-4b88-bf9d-dd1e83c212e9" />

ja voimme helposti korjata koodin lisäämällä luokan ``AdminDashboardView`` loppu koodin ``AdminShowAllView`` perään, koska sieltä se puutui.

<img width="1826" height="518" alt="image" src="https://github.com/user-attachments/assets/faebfb8b-4b88-470a-a04b-f4369e124377" />

Nyt verkkosivu ei anna pääsyä admin-console sivulle.

<img width="604" height="224" alt="image" src="https://github.com/user-attachments/assets/0a5424dd-46bc-490b-b9a5-af2a73662c58" />


## Lähteet:

OWASP: OWASP Top 10: https://top10.owasp.org/2025/A01_2025-Broken_Access_Control/

Hack'n Fix: https://terokarvinen.com/hack-n-fix/

PortSwigger: https://portswigger.net/web-security/access-control

Raportin kirjoittaminen: https://terokarvinen.com/2006/raportin-kirjoittaminen-4/

Find Hidden Web Directories - Fuzz URLs with ffuf: https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/



