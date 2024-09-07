# X) Tiivistelmät
## Name-based Virtual Host Support 
- nimiperusteinen vs ip-perusteinen: ip-perusteisessa tarvitaan erillinen Ip-osoite jokaiselle hostille. Nimiperusteisessa nimi ilmoitetaan HTTP otsikossa ja usemmalla hostilla voi olla sama ip-osoite.
- nimiperusteisen osoitteen valinta: palvelin etsii mahdollisimman tarkan vastaavuuden Ip-osoitteen ja portin avulla. Jos vaihtoehtoja on useampi, verrataan myös ServerName ja ServerAlias.
- VirtualHostia varten täytyy luoda VirtuaHost block ja antaa sille ServerName ja DocumentRoot
- VirtualHostille voi antaa ServerAlias määreen, joka kertoo muut nimet, jotka johtavat samaan IP-osoitteeseen. Esim www.example.com ja example.com
- Lähde The Apache Software Foundation 2023: Apache HTTP Server Version 2.4 Documentation https://httpd.apache.org/docs/2.4/vhosts/name-based.html

## Asennus
- ensin asennetaan apache2 ja korvataan oletussivu index.html tiedostolla
- seuraavaksi luodaan nimiperusteinen Virtual host
- sitten tehdään kansio kotisivulle ja sinne index.html sivu
- testataan toimivuutta komentorivin curl käskyillä ja selaimessa valitulla ServerNamella. Testaan, että sisältö on eri localhost ja virtualhost osoitteilla.
- Lähde Tero Karvinen 2018: Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/


# Lähtötilanne: 
Virtuaalikone VirtualBoxin kautta

RAM muisti 2GiB 

Virtuaalikoneella käytettävissä 64GB levy

käyttöjärjestelmänä Debian Linux

Host kone Windows 11 Home, jonka levy 474Gt 

prosessori AMD Ryzen 5 5500U with Radeon Graphics

Apache on jo asennettu 

# a) testaa localhost-osoite 
Testasin localhostin selaimella kirjoittamalla osoiteriville "localhost" ja sain seuraavan näkymän, joka kertoi, että sivu toimii:
![image](https://github.com/user-attachments/assets/c965f1a0-b0d5-43be-a6dc-ef65468acd04)


Testasin toiminnan myös komentorivillä "curl localhost" komennolla ja html koodi vastasi selaimella näkymyttä sivua, joten sivu toimii:
![image](https://github.com/user-attachments/assets/43362c0b-fc03-4aea-805f-9ee054bc9007)


# b) Loki
Aloitin selvittämällä millä komennolla loki löytyy. Olin kirjoittanut tunnilta muistiin komennon sudo tail /var/log/apache2/access.log|nl 

Tutkin vielä Apachen dokumenttia ja totesin, että tämän komennon pitäisi sopia tarkoitukseen: https://httpd.apache.org/docs/current/logs.html 

Komennon tuloksena tulei: 
![image](https://github.com/user-attachments/assets/ea883b4e-da08-4f77-853e-43217d981af4)

Käytin Apachen dokumentointia apuna analysointiin https://httpd.apache.org/docs/current/logs.html

127.0.0.1 IP-osoite 

-- tässä kohdassa olisi pyynnön tehneen käyttäjän id, mutta - kertoo, että se tieto puuttuu

[] sisällä on pyynnön ajankohta muodossa [day/month/year:hour:minute:second zone]

"GET / HTTP/1.1" käytetty metodi on GET ja pyydetty resurssi HTTP/1.1

200 statuskoodi. 2-alkuinen koodi kertoo, että pyyntö onnnistui. 4-alkuinen koodi kertoo virheestä

3380 palautuneen objektin koko

"-" sivusto, joka sisältää tai on linkitetty pyynnön kohteeseen

"Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0" asiakasselaimen raportoimat tiedot 

Lokissa oli merkintöjä 4.9. ja 5.9. (tehtävän tekopäivä)

5.9. päivältä näkyi äskeisen kohdan testaukset ensin selaimella ja sitten komentorivin curl komennolla riveillä 7-10.

7, 8 ja 10 rivit antoivat 200 koodin, eli pyynnöt olivat onnistuneet. 9 rivin 404-koodi kertoi virheestä favicon.ico pyynnön osalta. 7-9 rivien loppuosat kertoivat, että käytössä on ollut Firefox-selain ja Linux järjestelmä.



# c) Etusivu uusiksi. 
Seurasin Tero Karvisen ohjetta: https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/ 
Ensin poistin esimerkkisivun komennolla echo "Default"|sudo tee /var/www/html/index.html
Kävin katsomassa, että html-tiedosto on oikeassa paikassa ja avasin sen:

![image](https://github.com/user-attachments/assets/27e8f3c9-7119-4e42-b796-389ecaf7dea7)

![image](https://github.com/user-attachments/assets/05ead494-06bc-4ca8-88ac-ee332cdb6d32)

Seuraavaksi tein uuden name based virtual hostin komennolla sudoedit /etc/apache2/sites-available/hattu.example.com.conf ->
jotain meni pieleen ja sain virheviestin "No such file or diretory"

![image](https://github.com/user-attachments/assets/00a209ae-8d5d-4f62-9a70-d4c77488e36c)

Mietin johtuiko tämä sen hetken hakemistosta ja siirryin juurihakemistoon, mutta komennon jälkeen avautui tällainen ikkuna: 
![image](https://github.com/user-attachments/assets/54456eb7-5579-4d2f-aace-7e0053cc0644)

Tämä ei auttanut, joten kysyin chatgptltä apua, kuvasin ongelman ja virheviestin ja chat gptn ohjeella tajusin täyttää tyhjään näkymään tiedot:

![image](https://github.com/user-attachments/assets/45c3163c-69a5-4eca-8a40-ce92916ada74)

Tämän jälkeen tiedot näyttivät oikeilta: 
![image](https://github.com/user-attachments/assets/ba91e692-47d6-44af-8ff7-6eea1b7bf304)

Aktivoin virtualhostin ja käynnistin apachen uudelleen:

![image](https://github.com/user-attachments/assets/81828faf-a9f4-4e52-9a57-53135a581946)

Testasin välissä mitä curl komento kertoo = host puuttuu:

![image](https://github.com/user-attachments/assets/79f85ccd-3be4-446a-b982-053d5a15f9ee)


seuraavaksi koitin luoda webbisivut, mutta huomasin, että jotain on mennyt pieleen. En saa luotua www-hakemiston alle kansiota, mutta var-hakemistoon on tullut www.hattu.example.com hakemisto 
![image](https://github.com/user-attachments/assets/bbd1cf8d-4818-4e75-a868-e75c05a0abfb)

Olin tehtävän kanssa jumissa ja päätin aloittaa alusta. Pysäytin apachen komennolla sudo systemctl stop apache2

Tutkin ohjetta tarkemmin ja päätin kokeilla eri hakemistoa. Katsoin mitä roosa-hakemiston alta löytyy ja tarkemmin Public-hakemistoa. Aloitin uuden yrityksen tehdä uusi virtual host ja webbisivu polkuun /home/roosa/Public/lakki.example.com/

![image](https://github.com/user-attachments/assets/69a52e2c-617b-43e9-897f-4ed06d0e706f)

Aloitin alusta komennolla sudoedit /etc/apache2/sites-available/lakki.example.com.conf
Täytin tiedot, jotka näkyivät cat /etc/apache2/sites-available/lakki.example.com.conf komennolla:

![image](https://github.com/user-attachments/assets/6fcc22e7-bb0c-4e18-8aac-e788724e0567)

Käynnistin apachen uudestaan:

![image](https://github.com/user-attachments/assets/a65f69b0-3d00-4e9f-937b-db2b25f2f162)


Loin hakemiston lakki.example.com/ polkuun /home/roosa/Public/ Ja tarkastin, että se löytyy oikeasta paikasta.
![image](https://github.com/user-attachments/assets/7d5db42d-fe98-4ce6-971c-d3e70885e2aa)

Loin html-tiedoston kansioon ja tarkastin, että se on siellä:
![image](https://github.com/user-attachments/assets/08113a2b-08cb-49ce-8ad9-54537c45a78d)

Ja tarkastin selaimesta, että "lakki" näkyy:
![image](https://github.com/user-attachments/assets/b79e418a-92bc-415b-8c40-d413d2b9dafb)

Testausta: 
curl -H 'Host: lakki.example.com' localhost antaoi forbidden virheviestin, jota käytiin myös oppitunnilla.

curl localhost toimii. Koitan korjata 403 virheviestin komennolla 'chmod ugo+x $HOME $HOME/Public/', 'ls -ld $HOME $HOME/Public/' -> sain virheviestin No such file or direcotry:
 
![image](https://github.com/user-attachments/assets/8f1c3f02-b81c-484d-a15c-e22eb4ab8952)

Tarkastin käyttöoikeudet ls -ld komennolla.
Uusi yritys toisella polulla, joka vastaa tiedostoa chmod ugo+x /home/roosa/Public/lakki.example.com/
chmod komennon kohdalla ei tullut virheviestiä, mutta komento curl -H 'Host: lakki.example.com' localhost antaoi silti virheviestin. Koitin sammuttaa ja käynnistää uudelleen Apachen.

![image](https://github.com/user-attachments/assets/09c447b7-03b7-4c9b-80dd-31bc601184fe)

Vieläkään ei toiminut:
![image](https://github.com/user-attachments/assets/2ce8e4b4-392b-44e0-983d-08f47a4eaa1a)

Kysyin chat gptltä neuvoa ja sain ohjeen koittaa apachen uudelleen latausta: sudo systemctl reload apache2
Tämäkään ei auttanut ja seuraava neuvo oli tarkastaa error-loki: sudo tail /var/log/apache2/error.log
Loki ei tehnyt minua paljon viisaammaksi ja kysyin taas chatgptltä apua tulkitsemiseen: ei löytynyt mitään uutta, luvissa on vikaa. Katsoin uudelleen virtual hostin konfiguraatiota ja löysin kirjoitusvirheen. ChatGpt neuvoi mistä pääsen muokkaamaan tietoja: sudo nano /etc/apache2/sites-available/lakki.example.com.conf

![image](https://github.com/user-attachments/assets/c110078d-4b81-4387-ae6d-81376534975e)

Muutin pisteen kauttaviivaksi, mutta saan silti saman virheviestin. Tarkastin vielä cat-komennolla, että kaikki tiedot ovat nyt oikein:

![image](https://github.com/user-attachments/assets/6293419e-c9f4-4098-8c7e-4d9fb1fe764e)

Koitin uudelleen enabloida virtualhostin ja käynnistää uudelleen apachen siltä varalta, että niissä oli jotain vikaa ja nyt curl -H komento antoi jo lupaavan tuloksen:

![image](https://github.com/user-attachments/assets/6bde30b0-d323-463a-8c99-37850420dc61)

Testasin ratkaisua vielä selaimella- localhost toimii
![image](https://github.com/user-attachments/assets/c85b5839-beab-42fa-9d06-7f02ca7357cc)

lakki.example.com ei toiminut

![image](https://github.com/user-attachments/assets/c8dcd4f6-d8ed-4e14-8ffc-99d5abd792b2)

Huomasin, että ohjeessa on vielä yksi kohta, jossa määritellään lakki.example.com host-nimeksi: sudoedit /etc/hosts. Lisäsin tänne 127.0.1.1. lakki.example.com ja tarkastin cat /etc/hosts -komennolla:

![image](https://github.com/user-attachments/assets/764f340c-62f2-4701-9f62-42760e67cb3f)

Vihdoin sivu toimi sekä lakki.example.com osoitteella, että localhost osoitteella, kummallakin oma teksti:

![image](https://github.com/user-attachments/assets/56785bac-3719-4882-8c00-4b6a16d6615c)

![image](https://github.com/user-attachments/assets/2b1ba0b5-7cd5-4715-9dd0-699400747e67)

![image](https://github.com/user-attachments/assets/483e31bb-4024-48db-ba85-2d66ab7e6329)

sudo tail /var/log/apache2/access.log|nl  tarkastin lokin ja siellä näkyi yritykset, joissa lakki ei vielä toiminut ja lopula toimiva kysely:
![image](https://github.com/user-attachments/assets/9769d3fb-f258-49bd-81ee-d88ac89f00c1)

Lopuksi muutin lakki.example.com hakemiston index.html sivun tekstiksi lakki.example.com

![image](https://github.com/user-attachments/assets/c9345b3f-c718-4349-8d3e-716365f1090a)

Nimi näkyi tiedoston nimessä, ServerName muuttujassa ja etusivulla:
![image](https://github.com/user-attachments/assets/0cfc36fd-670d-47d1-ae27-67caa507eba0)

![image](https://github.com/user-attachments/assets/a8b6d96a-af23-48a9-b824-14e9842d0ecd)




# e) Tee validi HTML5 sivu.
Aloitin lukemalla ohjeen sivulta Tero Karvinen 2012 https://terokarvinen.com/2012/short-html5-page/ 

siirryin home/roosa/Public/lakki.example.com hakemistoon ja avasin index.html tiedoston muokkaamista varten:
![image](https://github.com/user-attachments/assets/e1e8aa0f-49e5-4bb4-a31d-0ee8f813d46b)

Määritin documentin tyypiksi HTML. Lisäsin head-osioon otsikon ja metatietoihin merkkisetiksi utf-8 ääkkösiä varten.
![image](https://github.com/user-attachments/assets/be10fa9e-da3a-47d6-a2ce-d28649c6f5e2)

Sivu näytti samat tiedot komentorivillä avattuna:
![image](https://github.com/user-attachments/assets/7e4a744a-4e38-4b4f-8209-47020338adfe)

Sivusto toimi selaimessa ja näyttti sen mitä lisäsin html tiedostoon:
![image](https://github.com/user-attachments/assets/a9c8280c-b878-45a2-a982-6bd8f19034f6)

Muokkasin index.html sivua vielä niin, että käytän ääkkösiä. Testasin curl komennolla ja selaimella, ääkköset näkyvät oikein:

![image](https://github.com/user-attachments/assets/6fc5d582-e081-4fe0-ac25-fd6492937fa7)

![image](https://github.com/user-attachments/assets/65f0887a-f4b4-4f30-9df3-8eef88630695)

Testasin sivua validator.w3.org sivulla, mutta sain virheviestin, jonka tulkitsen niin, että testiä ei voi tehdä, koska sivulla ei ole host-companya?
![image](https://github.com/user-attachments/assets/dbdb27d0-e429-4559-a237-07e02789f597)

Testasin sivuston avulla html-koodin ja sain varoituksen, jossa kehhoitetaan lisäämään kielen määritelmä.
![image](https://github.com/user-attachments/assets/3fb60369-fad6-4af3-b822-98d870af4397)

Lisäsin lang="fi" määritelmän html tägiin ja testasin uudestaan curl, selaimen ja validatorin:
![image](https://github.com/user-attachments/assets/5eca0d7a-12a8-4005-aee5-eadee8a35936)

![image](https://github.com/user-attachments/assets/2edd3254-3631-4130-ab23-6c7cfafb348d)

![image](https://github.com/user-attachments/assets/10b5df79-2a06-417e-831b-74eb011a04fc)


# f) Anna esimerkit 'curl -I' ja 'curl' -komennoista. Selitä 'curl -I' muutamasta näyttämästä otsakkeesta (response header), mitä ne tarkoittavat.

Tutkin ensin man curl komennolla mitä curl -i on tarkoitus tehdä:
![image](https://github.com/user-attachments/assets/6929817f-a064-4935-972d-48dea364c964)

esimerkki curl

![image](https://github.com/user-attachments/assets/f8ddff95-73ce-43cd-ba2e-8076eed1479d)


esimerkki curl-i

![image](https://github.com/user-attachments/assets/5b033491-0832-4a94-9fea-38698a7a98f6)

-i muotoinen komento antoi alkuun 9 riviä lisää:
HTTP/1.1 200 OK  -> kertoo statuksen, joka on ok
Date: Sat, 07 Sep 2024 09:46:16 GMT -> komennon ajankohta
Server: Apache/2.4.62 (Debian) -> apachen versio ja missä käyttöjärjestelmässä se on
Last-Modified: Sat, 07 Sep 2024 09:32:38 GMT -> viimeinen muokkausajankohta
ETag: "cc-62184345fcac5" -> sivun versiokohtainen tunniste lähde: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/ETag 
Accept-Ranges: bytes -> selain kertoo, että se tukee latausta tavuina lähde: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Accept-Ranges
Content-Length: 204 -> sisällön pituus
Vary: Accept-Encoding -> en osannut tulkita tämän tarkoitusta: https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Vary 
Content-Type: text/html -> sisältö on html tekstimuodossa


