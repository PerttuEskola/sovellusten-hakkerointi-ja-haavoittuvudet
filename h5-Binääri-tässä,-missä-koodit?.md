# h5 Binääri tässä, missä koodit?

## 1. main.cpp
Käytiin tunnilla yhdessä läpi miten saadaan main.cpp käännettyä
````bash
g++ main.cpp -g -Wall -Werror -o main.dbg
````
ja miten käynnistetään debugger luotuun tiedostoon main.dbg
````bash
gdb ./main-dbg
````
sekä lista debugger komentoja. 
````
list
run
step
next
continue
quit
````
## 2.Lab0.zip
Huomaamme että ohjelmassa on virhe

<img width="640" height="216" alt="image" src="https://github.com/user-attachments/assets/64ab8da0-da83-4914-acfc-63aab0a357e8" />

Etsitään virhe koodista

<img width="1130" height="452" alt="image" src="https://github.com/user-attachments/assets/8849f421-342c-4bbe-961d-1c56f6569fc8" />

Löydämme virheen koodista ja teemme tarvittavat korjaukset

<img width="1024" height="418" alt="image" src="https://github.com/user-attachments/assets/73bb33a9-23b5-4e65-9e3c-f097b9e9dec5" />

Nyt ohjelma toimii

<img width="638" height="262" alt="image" src="https://github.com/user-attachments/assets/6dede555-0e15-40d9-825c-06424c4284e4" />

## 3. lab1.zip

Ohjelmassa on jotain pielessä. 

<img width="692" height="94" alt="image" src="https://github.com/user-attachments/assets/2d494488-0f98-4598-a76b-63dcd22a83c8" />

Kun yrittää kääntää ohjelmaa se luo seuraavan virhe ilmoituksen.

<img width="1544" height="348" alt="image" src="https://github.com/user-attachments/assets/8f9e7c95-b9ec-46c8-a9ef-e35d3384d385" />

Ohjelma kaatuu koska bad_message on NULL ja se annetaan funkiolle print_scrabled joka ei voi käyttää sitä.

<img width="658" height="672" alt="image" src="https://github.com/user-attachments/assets/f0756665-bccc-472a-92a0-4439ce410aae" />

Ohjelma on siis mahdollista korjata lisäämällä jokin ohitus jos message on NULL


## 4. lab2.zip
Kansiossa on kaksi ohjelmaa sekä toisen läähdekoodi.

<img width="742" height="70" alt="image" src="https://github.com/user-attachments/assets/0e3c0b92-619d-4a67-936d-162df007feb7" />

Saamme kansion README.md ohjeet etsiä teron ja larin liput. Lippujen saamiseen tarvitaan kumpaankin salasana.
Ensimäinen salasana ja lippu löytyy helposti psstr.c lähdekooida tarkastelemalla.

<img width="1416" height="624" alt="image" src="https://github.com/user-attachments/assets/0371fd18-ce36-4be5-9bc2-a7f2b47bb336" />

Testaamme salasanan toimivuutta ohjelmassa pssrtr, ja saamme ohjelman tulostamaan lipun.

<img width="978" height="136" alt="image" src="https://github.com/user-attachments/assets/96c05c5c-c008-4537-bbd4-839d3f999fc9" />

Seuraavaksi on lähdettävä debuggaamaan ohjelmaa passtr2o, ajetaan passtr2o debuggeriin ja ajetaan komento disassemble main

<img width="1058" height="1054" alt="image" src="https://github.com/user-attachments/assets/10fd538f-9cce-46a3-8ff0-3f5a28028d48" />

Listalla meitä kiinnostaa eniten call 0x125a mAsdf3a, joten teemme disassemble mAsdf3a.

<img width="922" height="1158" alt="image" src="https://github.com/user-attachments/assets/8b349643-1bf2-45c9-ab56-73ffa8892fbc" />

Löydämme kaksi annettavaa merkkijono RDI ja RSI

Löydämme myös kaavat test 1 sub 7 ja add 3.


Haluamme lukea RDI:n ja RSI:n.

Sieltä löydämme antamamme salasanan ja toisen merkkijonon joka voi olla oikea salasana.
<img width="1058" height="428" alt="image" src="https://github.com/user-attachments/assets/50f091b5-5127-4613-9d6b-ccdfc24911da" />

Salasana anLTj4u8 ei kuitenkaan ole oikea koska aijemmin mainitut kaavat muokkaavat sitä.

Parilliseen merkkiin tulee +3 ja parittomaan -7. 

Voimme sen perusteella alkaa muokkaa maan salasanaa ASCII taulukon perusteella.

a +3 = d

n -7 = g

L +3 = O

T -7 = M

j +3 = m

4 -7 = -

u +3 = x

8 -7 = 1

Uusi salasana on dgOMm-x1 

Voimme testata uutta salasanaa.

<img width="1000" height="176" alt="image" src="https://github.com/user-attachments/assets/1358b0e2-c4e0-4338-ad73-6c51f1c7dc21" />

Se toimii ja meillä on nyt hallussa 2 salasanaa ja 2 lippua.


## 5. Lab3.zip
Tein tehtävän crackme01

Kun teemme crackme01.64 komennon cat tai strings, molemmista voimme huomata salasanan jota voimme yrittää.

<img width="677" height="568" alt="image" src="https://github.com/user-attachments/assets/81fd894a-a6dd-4fd6-8372-b241211d198a" />

password1 toimi ja tehtävä onnistui. Pitää huomioida että salasana ei välttämättä olisi näin helposti löynyty jos sen nimi olisi ollut jokin muu kuin password1.

<img width="958" height="158" alt="image" src="https://github.com/user-attachments/assets/2a9a3bd9-5153-4f6d-b215-c8b473282f73" />

## Lähteet

- Moodle opinto materiaalit.
- everybodylovesgdb https://everybodylovesgdb.org/2020/03/21/cracking-a-crackme/


