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
Sivun tulee näkyä suoraan palvelimen etusivulla http://localhost/. Sivua pitää pystyä muokkaamaan normaalina käyttäjänä, ilman sudoa. Tee uusi, laita vanhat pois päältä. Uusi sivu on hattu.example.com, ja tämän pitää näkyä: asetustiedoston nimessä, asetustiedoston ServerName-muuttujassa sekä etusivun sisällössä (esim title, h1 tai p).

Seuraan Tero Karvisen ohjetta: https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/ 
Ensin poistan esimerkkisivun komennolla echo "Default"|sudo tee /var/www/html/index.html
Kävin katsomassa, että html-tiedosto on oikeassa paikassa ja avasin sen:

![image](https://github.com/user-attachments/assets/27e8f3c9-7119-4e42-b796-389ecaf7dea7)

![image](https://github.com/user-attachments/assets/05ead494-06bc-4ca8-88ac-ee332cdb6d32)

Seuraavaksi teen uuden name based virtual hostin komennolla sudoedit /etc/apache2/sites-available/hattu.example.com.conf
jotain meni pieleen ja saan virheviestin No such file or diretory

![image](https://github.com/user-attachments/assets/00a209ae-8d5d-4f62-9a70-d4c77488e36c)

Mietin johtuiko tämä sen hetken hakemistosta ja siirryn juurihakemistoon, mutta komennon jälkeen avautuu tällainen ikkuna: 
![image](https://github.com/user-attachments/assets/54456eb7-5579-4d2f-aace-7e0053cc0644)
Tämä ei auttanut, joten kysyin chatgptltä apua, kuvasin ongelman ja virheviestin ja chat gptn ohjeella tajusin täyttää tyhjään näkymään tiedot:

![image](https://github.com/user-attachments/assets/45c3163c-69a5-4eca-8a40-ce92916ada74)

Tämän jälkeen tiedot näyttivät oikeilta: 
![image](https://github.com/user-attachments/assets/ba91e692-47d6-44af-8ff7-6eea1b7bf304)

Aktivoin virtualhostin ja käynnistin apachen uudelleen:

![image](https://github.com/user-attachments/assets/81828faf-a9f4-4e52-9a57-53135a581946)

Testasin välissä mitä curl komento kertoo: host puuttuu:

![image](https://github.com/user-attachments/assets/79f85ccd-3be4-446a-b982-053d5a15f9ee)


seuraavaksi koitin luoda webbisivut, mutta huomasin, että jotain on mennyt pieleen. En saa luotua www-hakemiston alle kansiota, mutta var hakemistoon on tullut www.hattu.example.com hakemisto 
![image](https://github.com/user-attachments/assets/bbd1cf8d-4818-4e75-a868-e75c05a0abfb)

Olin tehtävän kanssa jumissa ja päätin aloittaa alusta. Pysäytin apachen komennolla sudo systemctl stop apache2

Tutkin ohjetta tarkemmin ja päätin kokeilla eri hakemistoa. Katsoin mitä roosa hakemiston alta löytyy ja tarkemmin Public hakemistoa. Uusi yritys tehdä uusi virtual host ja webbisivu polkuun /home/roosa/Public/lakki.example.com/

![image](https://github.com/user-attachments/assets/69a52e2c-617b-43e9-897f-4ed06d0e706f)

Aloitin alusta komennolla sudoedit /etc/apache2/sites-available/lakki.example.com.conf
Täytin tiedot, jotka näkyvät cat /etc/apache2/sites-available/lakki.example.com.conf komennolla:

![image](https://github.com/user-attachments/assets/6fcc22e7-bb0c-4e18-8aac-e788724e0567)

Käynnistin apachen uudestaan:

![image](https://github.com/user-attachments/assets/a65f69b0-3d00-4e9f-937b-db2b25f2f162)


Loin hakemiston lakki.example.com/ polkuun /home/roosa/Public/ Ja tarkastin, että se löytyy oikeasta paikasta.
![image](https://github.com/user-attachments/assets/7d5db42d-fe98-4ce6-971c-d3e70885e2aa)

Loin html-tiedoston kansioon ja tarkastin, että se on siellä:
![image](https://github.com/user-attachments/assets/08113a2b-08cb-49ce-8ad9-54537c45a78d)

Ja tarkastin selaimesta, että "lakki" näkyy:
![image](https://github.com/user-attachments/assets/b79e418a-92bc-415b-8c40-d413d2b9dafb)

Testausta: curl -H 'Host: lakki.example.com' localhost antaa forbidden virheviestin, jota käytiin myös oppitunnilla.
curl localhost toimii. Koitan korjata 403 virheviestin komennolla 
 'chmod ugo+x $HOME $HOME/Public/', 'ls -ld $HOME $HOME/Public/' -> sain virheviestin No such file or direcotry:
 
![image](https://github.com/user-attachments/assets/8f1c3f02-b81c-484d-a15c-e22eb4ab8952)

TArkastin käyttöoikeudet ls -ld komennolla.
Uusi yritys toisella polulla, joka vastaa tiedostoa chmod ugo+x /home/roosa/Public/lakki.example.com/
chmod komennon kohdalla ei tullut nyt virheviestiä, mutta komento curl -H 'Host: lakki.example.com' localhost antaa silti virheviestin. Koitin sammuttaa ja käynnistää uudelleen Apachen.

![image](https://github.com/user-attachments/assets/09c447b7-03b7-4c9b-80dd-31bc601184fe)

Vieläkään ei toimi:
![image](https://github.com/user-attachments/assets/2ce8e4b4-392b-44e0-983d-08f47a4eaa1a)

Kysyn chat gptltä neuvoa ja saan ohjeen koittaa uudelleen latausta: sudo systemctl reload apache2
Tämäkään ei auta ja seuraava neuvo on tarkastaa error loki: sudo tail /var/log/apache2/error.log




# e) Tee validi HTML5 sivu.

# f) Anna esimerkit 'curl -I' ja 'curl' -komennoista. Selitä 'curl -I' muutamasta näyttämästä otsakkeesta (response header), mitä ne tarkoittavat.
