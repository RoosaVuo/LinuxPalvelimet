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
# a) testaa localhost-osoite 
 Asenna Apache-weppipalvelin, jos se ei ole jo asennettuna.

# b) Loki
Etsi lokista rivit, jotka syntyvät, kun lataat omalta palvelimeltasi yhden sivun. Analysoi rivit (eli selitä yksityiskohtaisesti jokainen kohta ja numero, etsi tarvittaessa lähteitä).

# c) Etusivu uusiksi. 
Tee uusi name based virtual host. Sivun tulee näkyä suoraan palvelimen etusivulla http://localhost/. Sivua pitää pystyä muokkaamaan normaalina käyttäjänä, ilman sudoa. Tee uusi, laita vanhat pois päältä. Uusi sivu on hattu.example.com, ja tämän pitää näkyä: asetustiedoston nimessä, asetustiedoston ServerName-muuttujassa sekä etusivun sisällössä (esim title, h1 tai p).

# e) Tee validi HTML5 sivu.

# f) Anna esimerkit 'curl -I' ja 'curl' -komennoista. Selitä 'curl -I' muutamasta näyttämästä otsakkeesta (response header), mitä ne tarkoittavat.
