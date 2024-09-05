# X) Tiivistelmät
Name-based Virtual Host Support 
- nimiperusteinen vs ip-perusteinen: ip-perusteisessa tarvitaan erillinen Ip-osoite jokaiselle hostille. Nimiperusteisessa nimi ilmoitetaan HTTP otsikossa ja usempi hostilla voi olla sama ip-osoite.
- nimiperusteisen osoitteen valinta: palvelin etsii mahdollisimman tarkan vastaavuuden Ip-osoitteen ja portin avulla. Jos vaihtoehtoja on useampi, verrataan myös ServerName ja ServerAlias.
- VirtualHostia varten täytyy luoda VirtuaHost block ja antaa sille ServerName ja DocumentRoot
- VirtualHostille voi antaa ServerAlias määreen, joka kertoo muut nimet, jotka johtavat samaan IP-osoitteeseen. Esim www.example.com ja example.com
- Lähde The Apache Software Foundation 2023: Apache HTTP Server Version 2.4 Documentation https://httpd.apache.org/docs/2.4/vhosts/name-based.html

  
- ensin asennetaan apache2 ja korvataan oletussivu index.html tiedostolla
- seuraavaksi luodaan nimiperusteinen Virtual host
- sitten tehdään kansio kotisivulle ja sinne index.html sivu
- testataan toimivuutta komentorivin curl käskyillä ja selaimessa valitulla ServerNamella. Testaan, että sisältö on eri localhost ja virtualhost osoitteilla.
- Lähde Tero Karvinen 2018: Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/


Tehtävänannot:

Lähtötilanne: 5.9.2024 klo 16.10. Apache on jo asennettu. 

# a) testaa localhost-osoite 
Testaan localhostin selaimella kirjoittamalla osoiteriville "localhost" ja saan seuraavan näkymän, joka kertoo, että sivu toimii:
![image](https://github.com/user-attachments/assets/c965f1a0-b0d5-43be-a6dc-ef65468acd04)


Testasin toiminnan myös komentorivillä "curl localhost" komennolla ja html koodi vastaa selaimella näkymyttä sivua, joten sivu toimii:
![image](https://github.com/user-attachments/assets/43362c0b-fc03-4aea-805f-9ee054bc9007)


# b) Loki
Aloitin selvittämällä millä komennolla loki löytyy. Olin kirjoittanut tunnilta muistiin komennon sudo tail /var/log/apache2/access.log|nl 

Tutkin vielä Apachen dokumenttia ja totesin, että tämän komennon pitäisi sopia tarkoitukseen: https://httpd.apache.org/docs/current/logs.html 

Komennon tuloksena tulee: 
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

Lokissa on merkintöjä eiliseltä (4.9.) ja tältä päivältä (5.9.) 

Tältä päivältä näkyy äskeisen kohdan testaukset ensin selaimella ja sitten komentorivin curl komennolla riveillä 7-10.

7, 8 ja 10 rivit antavat 200 koodin, eli pyynnöt ovat onnistuneet. 9 rivin 404-koodi kertoo virheestä favicon.ico pyynnön osalta. 7-9 rivien loppuosat kertovat, että käytössä on ollut Firefox-selain ja Linux järjestelmä.




# c) Etusivu uusiksi. 
Tee uusi name based virtual host. Sivun tulee näkyä suoraan palvelimen etusivulla http://localhost/. Sivua pitää pystyä muokkaamaan normaalina käyttäjänä, ilman sudoa. Tee uusi, laita vanhat pois päältä. Uusi sivu on hattu.example.com, ja tämän pitää näkyä: asetustiedoston nimessä, asetustiedoston ServerName-muuttujassa sekä etusivun sisällössä (esim title, h1 tai p).

# e) Tee validi HTML5 sivu.

# f) Anna esimerkit 'curl -I' ja 'curl' -komennoista. Selitä 'curl -I' muutamasta näyttämästä otsakkeesta (response header), mitä ne tarkoittavat.
