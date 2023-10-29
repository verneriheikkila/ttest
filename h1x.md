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
