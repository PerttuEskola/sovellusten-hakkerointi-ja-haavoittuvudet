# h2 Break & Unbreak

## x)

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


Lähteet:

Hack'n Fix: https://terokarvinen.com/hack-n-fix/

Find Hidden Web Directories - Fuzz URLs with ffuf: https://terokarvinen.com/2023/fuzz-urls-find-hidden-directories/



