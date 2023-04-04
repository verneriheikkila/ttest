# Oma Labra
## x.)
- Darknet Diaries Jakso 27: "Chartbreakers"
- Podcastissa keskustellaan podcast-rankingin manipuloinnista.
- Keskitytään kahteen podcasteriin (Jack ja Lila), jotka paljastavat järjestelmän.
- Taulukoiden manipuloijat käyttävät botteja, väärennettyjä arvosteluja ja latauksia.
- Tekniikoihin kuuluvat podcast-listojen parantaminen ja väärät positiiviset arvostelut.
- Podcasterit kärsivät epäreilusta kilpailusta ja uskottavuuden vähenemisestä.
- Ala tarvitsee parempia havaitsemis- ja torjuntamekanismeja

## a.) Kalin Asennus M1 rautaan

- Avasin UTM ja loin uuden virtuaalikoneen
- Valitsin käyttöjärjestelmäksi "other" ja Kali ISO-tiedoston
- Asetin muistin määräksi 4096 MB ja kiintolevyn kooksi 40 GB
- Asensin Kali Linuxin "console only" -moodissa UTM-bugin vuoksi
- Lisäsin Serial-laitteen asetuksiin ja poistin sen Kali-asennuksen jälkeen
- Käynnistin virtuaalikoneen ja asensin Kali Linuxin oletusasetuksilla
- Poistin USB-driven asetuksista asennuksen jälkeen
- Lisäsin kaksi verkkokorttia: "Shared" ja "Host-only"

## b.) Metasploitable2 asennus M1 rautaan

### Asennus
- Asenna Qemu Homebrew'n avulla:
```bash
brew install qemu
```
- Lataa Metasploitable 2 image:
https://sourceforge.net/projects/metasploitable/
- Pura ladattu zip-paketti ja muunna Metasploitable.vmdk UTM:n tukemaan qcow2-muotoon:
```bash
unzip metasploitable-linux-2.0.0.zip
cd Metasploitable2-Linux
qemu-img convert -O qcow2 -c Metasploitable.vmdk MetasploitableUTM.qcow2
```

### UTM-virtuaalikoneen asetukset
- Avaa UTM ja luo uusi virtuaalikone.
- Valitse käyttöjärjestelmäksi "Other" ja ohita ISO-boot.
- Aseta haluttu muisti ja levytila (kannattaa arvioida mielummin yläkanttiin, koska tämä on emulaatio, ei virtualisaatio).
- Nimeä virtuaalikone ja tallenna asetukset.
- Poista UEFI Boot -asetus QEMU-kohdasta.
- Aseta verkkotila "Host Only" -tilaan.
- Poista IDE Drive ja lisää uusi IDE-levy MetasploitableUTM.qcow2-levykuvalla.
- Tallenna asetukset ja käynnistä virtuaalikone UTM:n konsolista.

## c.)
- Kali-koneella on kaksi verkkosovitinta: "Shared", joka tarjoaa internetyhteyden, ja "Host-only", joka on virtuaalikoneiden välinen sisäinen verkko.
- Metasploitable-koneella on vain "Host-only" sisäinen verkko.

## d.)
- Testaa yhteys
```bash
ping (metasploitip)
```
- Start Metasploit 
```bash
sudo msfdb run
```
- Luo Worspace harjoitusta varten
```bash
workspace -a metasploitable-h1
```
- Porttiskannaa kohde
```bash
db_nmap -sn (metasploit ip)
```
