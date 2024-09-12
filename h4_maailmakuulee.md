## x) Lue ja tiivistä. Tiivistelmäksi riittää muutama ranskalainen viiva per artikkeli. (Tässä alakohdassa ei tarvitse tehdä testejä tietokoneella)
aloitus 12.9. klo 21.40 lopetus 22.05
a) Pilvipalvelimen vuokraus ja asennus
  - palvelimen voi vuokrata esim DigitalOceanilta tai UpCloadilta - näihin voi saada alennuskoodin GitHub Educationista
  - palvelimelle kannattaa valita mahdollisimman uusi Debian versio. Asetuksiin valitaan SSD kovalevy 25GB, prosessori 1GB ja siirtodataa 1000GB. Datakeskus kannattaa valita mahdollisimman läheltä käyttäjiä.
  - Autentikointimenetelmäksi salasana, jonka täytyy olla hyvä
  - Mitään lisäpalveluita ei kannata ottaa
  - ota talteen virtuaalikoneen IP-osoite
  - Domain kannattaa vuokrata NameCheap sivulta. Tarkasta ostoskori, ettei siellä ole maksullisia tuotteita.
  - etsi vapaana oleva sopiva domainnimi
  - viimeistele tilaus ja rekisteröidy käyttäjäksi
d) Palvelin suojaan palomuurilla
  - ota yhteys virtuaalikoneeseen ssh root@ipnumero komennolla -> tee päivitykset sudo apt-get update -> asenna palomuuri sudo apt-get install ufw -> tee reikä porttia varten sudo ufw allos 22/tpc -> laita palomuuri päälle sudo ufw enable
e) Kotisivut palvelimelle
- lisää käyttäjä komennolla sudo adduser käyttäjänimi -> keksi hyvä salasana -> tee käyttäjästä pääkäyttäjä sudo adduser käyttäjänimi sudo -> testaa, että ssh yhteys toimii käyttäjällä -> lukitse juuri sudo usermod --lock root
    - ota root kirjautuminen pois päältä: sudoedit /etc/ssh/sshd_config -> PermitRootLogin no -> sudo service ssh restart
f) Palvelimen ohjelmien päivitys
- suorita päivitykset komennoilla sudo apt-get update, sudo apt-get upgrade ja sudo apt-get dist-upgrade
- tee palomuuriin reikä apachelle sudo ufw allow 80/tcp
- asenna apache: sudo apt-get install apache2 

Lähteet: Susanna Lehto 2022: Teoriasta käytäntöön pilvipalvelimen avulla (h4) (opiskelijan esimerkkiraportti) ja Karvinen 2012: First Steps on a New Virtual Private Server – an Example on DigitalOcean and Ubuntu 16.04 LTS

## a) Vuokraa oma virtuaalipalvelin haluamaltasi palveluntarjoajalta. 
## b) Tee alkutoimet omalla virtuaalipalvelimellasi: tulimuuri päälle, root-tunnus kiinni, ohjelmien päivitys.
## c) Asenna weppipalvelin omalle virtuaalipalvelimellesi. Korvaa testisivu. Kokeile, että se näkyy julkisesti. Kokeile myös eri koneelta, esim kännykältä.

  
