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
Lähtötilanne: Virtuaalikone VirtualBoxin kautta
RAM muisti 2GiB
Virtuaalikoneella käytettävissä 64GB levy
käyttöjärjestelmänä Debian Linux
Host kone Windows 11 Home, jonka levy 474Gt
prosessori AMD Ryzen 5 5500U with Radeon Graphics

aloitus 15.9. klo 14.20 lopetus 14.59 
Käytin ohjeena Susannan Lehdon tarkkaa raporttia Teoriasta käytäntöön pilvipalvelimen avulla https://susannalehto.fi/2022/teoriasta-kaytantoon-pilvipalvelimen-avulla-h4/ 

Aloitin tutustumalla GitHub Educationin tarjontaan. Löysin valikoimasta DigitalOceanin tarjouksen ja valitsin sen, koska se oli tuttu tunnilta ja Susannan raportista. Klikkasin linkkiä "Get access.."
![image](https://github.com/user-attachments/assets/8c6c70c9-23bf-43bd-a7f4-a03aef9671d9)
Seuraavasta näkymästä valitsin "Sign In with GitHub" ja seuraavasta näkymästä valitsin "Authorize digitalocean"
![image](https://github.com/user-attachments/assets/1b1ef4b2-9b49-422b-85ba-53c416d705de)

Sain virheviestin ja tulkitsin tästä, että minun täytyy ensin rekisteröityä, koska tunnusta ei löydy:
![image](https://github.com/user-attachments/assets/94f0e0b1-477e-4ae5-b30a-07f1d9dde066)
Valitsin oikeasta yläkulmasta signup ja github. 

Täytin pyydetyt tiedot: 
![image](https://github.com/user-attachments/assets/9be08d89-42ad-460a-a10e-689c1aa0306f)

Seuraavaksi pyydettiin maksutiedot indentiteetin varmistusta varten. Täytin tiedot. 
![image](https://github.com/user-attachments/assets/5aa7a64f-cd82-42b3-a362-54b402a371d0)

1 dollarin maksu vahvistettiin pankkitunuksilla. Tämän jälkeen klikkasin "Authenticate with GitHub"
![image](https://github.com/user-attachments/assets/76f6f1e4-111e-437f-b767-1cdbfd58ac47)

Ja valitsin Authorize digitalocean:

![image](https://github.com/user-attachments/assets/470771fa-b9b9-462e-af19-387760cfa157)

Sain vahvistuksen, että 200$ student pack on käytettävissä.
![image](https://github.com/user-attachments/assets/b8edae9c-e541-4b28-a498-dc6e9871bd80)

Palvelun etusivu aukesi ja valitsin vasemmalta Droplets ja sieltä Create Droplet:
![image](https://github.com/user-attachments/assets/b201b6c3-e63d-454f-b50a-25935934243b)

Valitsin alueeksi Amsterdamin, sillä se oli lähimpänä. Jätin Datacenterin oletusasetuksen Amsterdam Datacenter3 aMS3. Käyttöjärjestelmäksi otin Debian 12x64

![image](https://github.com/user-attachments/assets/2fd86a50-0f38-45f1-b527-2d10db2520b5)

Droplet Type: valitsin Basic, CPU options: valitin Regular SSD levyn, tilaukseksi edullisin 1GB/ 1CPU vaihtoehto 6$/kk:
![image](https://github.com/user-attachments/assets/23fadabc-5183-4359-af12-19a3b2bb041c)

En ottanut lisäpalveluita.
Authentication Method -> valitsin hyvän salasanan

![image](https://github.com/user-attachments/assets/27205bee-e40b-4088-8ae3-5b097ebf5fe1)

En ottanut muitakaan lisäpalveluita. 1 Droplet riittää, jätin sen valinnan ja muutin hostname kohtaan "Webbi"

![image](https://github.com/user-attachments/assets/77248b0c-3940-4980-bf42-501dc034414a)

Seuraavaksi klikkasin Create Droplet -nappia.

Virtuaalikoneen luominen oli valmis ja tallensin itselleni IP-osoitteen:
![image](https://github.com/user-attachments/assets/198de61a-f881-4759-96fc-da3e8b3b608e)


## b) Tee alkutoimet omalla virtuaalipalvelimellasi: tulimuuri päälle, root-tunnus kiinni, ohjelmien päivitys.


## c) Asenna weppipalvelin omalle virtuaalipalvelimellesi. Korvaa testisivu. Kokeile, että se näkyy julkisesti. Kokeile myös eri koneelta, esim kännykältä.

  
