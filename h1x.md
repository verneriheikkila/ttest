# Hacker Warmup

## x.)

### Santos et al: The Art of Hacking

https://learning.oreilly.com/videos/the-art-of/9780135767849/9780135767849-SPTT_04_03/

- Aktiivinen tiedustelu on hyökkääjän toimintaa, jolla kerätään tietoja kohteesta.
- Porttiskannaus on yksi yleisimmistä aktiivisen tiedustelun tekniikoista.
- Sen avulla voidaan selvittää, mitkä portit ovat auki kohdejärjestelmässä.
- Jos avoimia portteja löytyy voi hyökkääjä niiden avulla yrittää päästä sisään järjestelmään.
- Aktiivinen tiedustelu jättää jälkiä logeihin toisin kuin passiivinen.

### Hutchins et al 2011: Intelligence-Driven Computer Network Defense

https://lockheedmartin.com/content/dam/lockheed-martin/rms/documents/cyber/LM-White-Paper-Intel-Driven-Defense.pdf

- Hyökkäysketjussa hyökkääjä pyrkii saamaan pääsyn kohteeseen ja toteuttaa tarkoituksensa toteuttamalla sarjan vaiheita.
- Sen vaiheita ovat:
  - Tutkiminen: Kohteesta kerätään tietoja.
  - Tarkkailu: Kohteen toimintaa seurataan.
  - Injektio: Kohteeseen asennetaan haittaohjelma.
  - Eskalaatio: Kohteeseen saadaan pääsy.
  - Tarkoitus: Hyökkääjä toteuttaa tarkoituksensa, kuten tiedon varastamisen tai palvelun häiritsemisen.

## a.)

Olen pelannut Bandittia muutamaan otteeseen aikaisemmin, joten ensimmäiset tasot olivat jo ennaltaan tuttuja.

![1](/kuvat/h1/a/1.png)

Otetan SSH yhteyden bandit.labs.overthewire.org koneelle/palvelimelle tunnuksella bandit0 käyttäen porttia 2220 tehtävänannon ohjeiden mukaisesti.

![2](/kuvat/h1/a/2.png)

Tutkin hakemiston ls komennolla ja löydän tiedoston "readme" jonka luen cat komennolla. Se paljastaa seuraavan tason salasanan.
Lopeta SSH yhteyden.

![3](/kuvat/h1/a/3.png)

Avaan uuden yhteyden, mutta käytän tälläkertaa käyttäjää bandit1 kirjautumiseen ja käytän salasanana edellisestä tasosta löytämääni salasanaa. Salasana on oikea ja pääsen kirjautumaan sisään.

![4](/kuvat/h1/a/4.png)

Tutkin taas hakemiston käyttämällä ls komentoa ja löydän tiedoston, joka on nimetty "-". Linux tulkistee tämän vaihtoehdoksi ja lipuksi eikä sen lukeminen suoraltaan onnistu vaan se täytyy lukea muulla tavalla, esimerkiksi lisäämällä eteen tiedostopolku "./cat". Lukeminen onnistuu tällä tavalla ja salasana seuraavaan tasoon paljastuu.

![5](/kuvat/h1/a/5.png)

Kirjaudun sisään tunnuksella bandit2 ja saamallani salasanalla ja pääsen kirjautumaan sisään ilman ongelmia.

![6](/kuvat/h1/a/6.png)

Tutkin hakemiston taas ls komennolla ja löydän tiedoston jonka nimi koostuu useasta sanasta.
Koska välilyönnit toimivat usein komentorivillä argumenttien erotinmerkkeinä ei cat komennolla pysty suoraan lukemaan tiedostoa. Tiedostonimen voi esimerkiksi kääriä lainausmerkkeihin, jolloin cat tunnistaa sen yhtenäiseksi tiedostonimeksi. Salasana paljastuu.

## b.)

![b1](/kuvat/h1/d/a.png)
![b2](/kuvat/h1/d/b.png)
![b3](/kuvat/h1/d/c.png)
![b4](/kuvat/h1/d/d.png)

## c.)

Ennen laboratorion avaamista on tehtävänanto, jossa periaatteessa kerrotaan miten tehtävä tulee tehdä.
Avaan laboratorion ja tutkin sivuja. Huomaan,että tuotekategoriat näkyvät mudossa:

```
/filter?category=Gifts
```

voimme siis injektoida SQL injektion:

```
'+OR+1=1--
```

Eli

```
/filter?category=Gifts+'+OR+1=1--
```

En ole aivan varma miksi injektio aloitetaan merkillä ', mutta loppuosa on melko itsestäänselvä. Annetaan arvo joka on aina tosi, eli 1=1 ja sen jälkeen käytetään SQL kommenttia "--" kommentoimaan loput lauseesta pois.

## d.)

![d1](/kuvat/h1/d/1.png)

Latasin ditribuutiot kunkin omalta nettisivulta.
Mounttasin levykuvan VirtualBoxiin ja käynnistin koneen, joka boottasi levykuvasta ja kävin läpi asennuksen ilman ongelmia.

## e.)

Latasin nmapin

```
sudo apt-get nmap
```

Scannasin 1000 yleisintä porttia

```
sudo nmap
```

![e1](/kuvat/h1/e/1.png)

Ilman lisämääreitä nmap skannaa vain 1000 yleisintä porttia joista kaikki 1000 olivat huomioiimattomassa tilassa.

## f.)

Tulos ei juurikaan muuttunut. Kone sanoo edelleen, että kaikki portit ovat suljettuja. Edelleen ihmettelen miltä portilta yhteys internettiin tulee ja kohtaa "1 IP Adress 1 Host up".

![f1](/kuvat/h1/f/1.png)

## g.)

![g1](/kuvat/h1/g/1.png)

Komento ei Kalilla tunnistanut järjestelmää, joten siirryin kokeilemaan Debianilla jolla sai komennolla hieman enemmän asiaa irti. -A lippu tekee paljon. Se aktivoi neljä muuta lippua -sV -T4, -O ja -script=default.

- -Sv Pyrkii tunnistamaan käynnissä olevia palveluita ja niiden versioita.
- -T4 Lippu yrittää ajaa haun agressiivisemmin, eli nopeammin.
- -O Pyrkii keräämään tietoa kohteen käyttöjärjestelmästä ja sen käynnissä olevista palveluista.
- -script=default Ajaa nmpain skriptitiedostota oletus asetuksilla ja keräämään tietoa kohteen palveluista.

Minun tapauksessani se sai selville portin 631 jokaa onauki internet yhteyden muodostamista varten.Se sai myös selville, että järjestelmäni pyöroo linux kernelillä, ditribuutioota tai sen versiota se ei saanut selville.

## h.)

![h1](/kuvat/h1/h/1.png)

Scannaus tunnisti asennetun palvelimen ja sen avulla myös linux ditribuution jolla sitä ajetaan(aiemmin ei tunnistanut). Eli pystyi palvelimen perusteella päättelemään muutakin tietoa koneestani.

## i.)

En täysin ymmärtänyt tehtävää.
https://www.bellingcat.com/category/resources/
sisälsi nopealla katsauksella lähinnä artikkeleita eikä työkaluja.
https://inteltechniques.com/tools/index.html
sen sijaan sisälsi työkaluja joista monet oli tehty täysin jenkkilää varten - osoitetiedot, puhelinnumerot, yms... olivat jenkkilä mallia. koitin ajaa omaa sähköpostiani ja käskin työkalua ajamaan kaikilla hakukoneilla, mutta eteeni ilmestyi vaim google haku omalla söhköpostilla. Ei tuntunut varsinaisesti kovin hyödylliseltä. Toki tuo populate all toiminto nopeuttaa, jos niitä siitä listasta alkaa yksitellen painelemaan.

## Lähteet

- https://chat.openai.com/
- https://bard.google.com/chat/
- https://learning.oreilly.com/videos/the-art-of/9780135767849/9780135767849-SPTT_04_03/
- https://lockheedmartin.com/content/dam/lockheed-martin/rms/documents/cyber/LM-White-Paper-Intel-Driven-Defense.pdf
- https://portswigger.net/web-security/sql-injection
- https://portswigger.net/web-security/sql-injection/lab-retrieve-hidden-data
- https://inteltechniques.com/tools/index.html
- https://www.kali.org/docs/installation/hard-disk-install
- https://terokarvinen.com/2021/install-debian-on-virtualbox/
- nmap man sivu
