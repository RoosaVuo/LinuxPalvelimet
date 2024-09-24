Lähtötilanne:
Virtuaalikone VirtualBoxin kautta

RAM muisti 2GiB

Virtuaalikoneella käytettävissä 64GB levy

käyttöjärjestelmänä Debian Linux

Host kone Windows 11 Home, jonka levy 474Gt

prosessori AMD Ryzen 5 5500U with Radeon Graphics

## a) Kotisivu. Tee vähintään kolmen erillisen weppisivun kotisivu ja kopioi se näkymään palvelimellesi. Käytä name based virtual hosting tekniikkaa. Sivujen muokkaamisen pitää onnistua ilman pääkäyttäjän oikeuksia, niiden kopioiminen pääkäyttäjänä testisivun paikalle ei käy. Kotisivujen ei tarvitse olla hienoja, mutta niiden tulee olla validia HTML:ää ja linkittää toisiinsa.

23.9. aloitus 12.00 lopetus klo 14.24

Aloitin muokkaamalla toisella kurssilla tehtyä nettisivupohjaa. Käytin navigaatiorakennetta hyödyksi, mutta muutin sisältöä ja tyyliä. 
Seuraavaksi tutkin "scp -r" komentoa "man scp" komennolla. Tulkitsin tehtävänannon niin, että teen webbisivu hakemiston tiedoistoineen ensin virtualboxin virtuaalikoneelle ja sitten kopioin sen DigitalOceanin kautta vuokratulle palvelimelle. 

Tutkin mkdir käyttöohjetta ja sen jälkeen tein public_html kansion ja sen alle tiedostot:

![image](https://github.com/user-attachments/assets/fb0da562-8058-4295-a2a1-bfcd35ee2f22)

Koitin editoida tiedostoja, mutta olinkin tosiaan luonut hakemistot, enkä tiedostoja. Poistin index, helloworld, heimaailma ja styles hakemistot ja tein tilalle tiedostot. heimaailmaan tuli virhe, joten muokkasin sivua heti uudestaan:

![image](https://github.com/user-attachments/assets/0fcc36aa-e926-4297-8d82-18ae55998484)

Lisäsin koodit kuhunkin tiedostoon:

![image](https://github.com/user-attachments/assets/521dfde0-6f99-457d-997e-e3cb501ab11f)

Avasin uuden terminaalin ja otin ssh yhteyden palvelimelle: 

![image](https://github.com/user-attachments/assets/6e769b10-eda4-44f3-8136-55561916ca17)

Loin public_html -kansion:

![image](https://github.com/user-attachments/assets/914094c0-b4f2-4600-91ed-0cc38504b5b6)

Tutustuin vielä scp komentoon ja tulkintani mukaan tämä varmistaa turvallisen tiedostojen kopioinnin kahden palvelimen välillä. Lähde: https://www.techrepublic.com/article/how-to-use-scp-command-send-files-securely/

Kopioin kansion public_html:

![image](https://github.com/user-attachments/assets/0cbcf563-24d0-4a00-ab97-58483d9e970b)

Komennonssa oli tullut ajatusvirhe ja olin luonunt public_html kansion alle toisen public_html kansion, jossa tiedostot ovat. Mielestäni tämä ei haittaa tehtävän suorittamista, joten jatkan tehtävää:

![image](https://github.com/user-attachments/assets/2cfe4549-3877-4503-8935-10566f89829b)

Kertasin name based virtualhost tekniikkaa Teron sivulta: https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/ 

Käytin sudoedit komentoa, mutta tajusin, että tässä kuului olla palvelimen nimen kanssa samanniminen kansio, joten toinen yritys rvuorela.me.conf päätteellä. Täyttäessäni name based virtualhostin tietoja tajusin myös, että minulta puuttuu kansio rvuorela.me. Olin luonut public_html kansion alle toisen public_html kansion ja nimesin sen uudestaan rvuorela.me. 

![image](https://github.com/user-attachments/assets/27835a3e-ef74-443b-84a8-de0e7c8e6b73)

Täytin virtualhostin tiedot:

![image](https://github.com/user-attachments/assets/6538af4d-8305-4f67-b7b3-7979eff3860d)

Seuraavaksi syötin komennot sudo sudo a2ensite rvuorela.me ja sudo systemctl reload apache2:

![image](https://github.com/user-attachments/assets/d1232b05-b9f8-41ff-aabc-4c95090504d9)

Lisäsin rvuorela.me nimen Host listaan:

![image](https://github.com/user-attachments/assets/caf91eaf-fae5-4437-883b-a601c3f65804)

Testasin sivua selaimella ja sain virheviestin: 

![image](https://github.com/user-attachments/assets/791410bf-938a-42dc-a92a-70856f3f6a0f)

Tarkastin oikean hakemistopolun ja tarkastin onko configurointi oikein "cat /etc/apache2/sites-available/rvuorela.me.conf" :

![image](https://github.com/user-attachments/assets/a10882a1-7d3a-49d0-93c1-fff8776f4841)

Polku ja tiedot näyttivät olevan oikein.
Tarkastin, että rvuorela.me.conf löytyy apache2/sites-available alta:

![image](https://github.com/user-attachments/assets/7c780aea-75ea-4069-8e6e-d038423506d0)

Tässä kohtaaa kysyi ChatGptltä apua. Kerroin mitä olen tekemässä ja millaisen virheviestin saan. Ohjeiden perusteella tarkastin host määritykset ja ip-osoitteessa oli virhe. Chat ohjasi tarkastamaan login ja vaikutti siltä, että apachelta puuttuu oikeuksia: 

![image](https://github.com/user-attachments/assets/804344cb-08ee-4c47-8a04-8cbefeb4907c)

Tarkastin oikeudet komennoilla ls -ld /home/roosa ja ls -ld /home/roosa/public_html
Oikeudet näyttivät olevan puutteelliset, joten chat gptn ohjeella korjasin ne sudo chmod 711 /home/roosa ja sudo chmod 755 /home/roosa/public_html

ChatGptn selvennys:

![image](https://github.com/user-attachments/assets/07f91d28-b226-4261-90be-365459e5e98e)

Latasin apachen uudelleen ja sivu alkoi toimimaan. Testasin sivujen linkityksen:

![image](https://github.com/user-attachments/assets/d447b27a-3498-471f-99ab-50ad315a6a64)

![image](https://github.com/user-attachments/assets/3533f56f-4a61-4c9d-8b69-2491cbb90dc5)

![image](https://github.com/user-attachments/assets/b57d2e49-d1ff-4272-9234-d8073878352e)

Huomasin etusivulla kirjoitusvirheen, joten muokkasin sivua tavallisena käyttäjänä. Micro-ohjelmaa ei löytynyt vielä, joten asensin sen sudo apt-get -y install micro -komennolla. 

![image](https://github.com/user-attachments/assets/2b09492c-895e-42d1-aa6e-8beeb83e32e5)

![image](https://github.com/user-attachments/assets/ebd3599f-57a3-4a2e-a3ec-70b923218db1)

![image](https://github.com/user-attachments/assets/4183cc1b-c170-4408-98a9-51479af1eec0)

![image](https://github.com/user-attachments/assets/d38d0496-4f62-468d-bf07-38d958b06508)

Curl-komento antaa oikean nettisivun koodin:

![image](https://github.com/user-attachments/assets/b4499ecc-0c67-4ddb-87a1-86e21851b55e)

Tarkastin https://validator.w3.org sivulla, että html sivu on validi:

![image](https://github.com/user-attachments/assets/db41fd21-fded-441f-8fe2-e07afe40c82a)



## b) Alidomain. Tee kaksi uutta alidomainia, jotka osoittava omaan koneeseesi. Esimerkiksi palvelu on example.com -> linuxkurssi.example.com. Tee toinen alidomain A-tietueella ja toinen CNAME-tietueella. Alidomainit ovat tyypillisesti ilmaisia, kun sinulla on päädomain (example.com).

23.9. aloitus 14.35 lopetus 14.46

Käytin lähteenä namecheapin omaa ohjetta: https://www.namecheap.com/support/knowledgebase/article.aspx/9776/2237/how-to-create-a-subdomain-for-my-domain/ 

Kirjauduin namecheapiin ja valitsin valikosta Domain List ja domainin vierestä Manage:

![image](https://github.com/user-attachments/assets/dd14a927-24c2-43cf-8f2f-136eb8501d1c)

Valitsin yläavalikosta Advanced DNS.
Loin yhden A Recordin, jolloin roosa.rvuorela.me osoittaa IP osoitteeseen.
Loin CNAME Recordin, jolloin linuxkurssi.rvuorela.me osoite osoittaa rvuorela.me osoitteeseen.

![image](https://github.com/user-attachments/assets/599f8763-194c-445b-8588-e0443463e82a)

Molemmat alidomainit näyttävät oletussivun:

![image](https://github.com/user-attachments/assets/67f21cd7-0eee-4d27-87d4-d3a2c2b65bc0)

![image](https://github.com/user-attachments/assets/816d92e7-ee3c-40b1-9acc-829020471186)





## c) Pubkey. Automatisoi kirjautuminen julkisella SSH-avaimella.

23.9. ohjeiden lukemista ja lähteiden etsimistä 15.30-15.50 
klo 16.38 - 16.55 varsinainen tehtävä

Tutkin erilaisia lähteitä ja tämä vaikutti luotettavalta sivulta, joten käytin lähteenä: https://www.ssh.com/academy/ssh/keygen ja https://www.ssh.com/academy/ssh/copy-id

Aloitin luomalla avaimen komennolla: ssh-keygen -t rsa -b 4096. Oletustiedosto ja passphrase kohdat jätin tyhjiksi: 

![image](https://github.com/user-attachments/assets/31763c79-2e8c-4ad2-a8ca-27a7be626157)

Seuraavaksi kopioin avaimen palvelimelle, jotta siitä tulee "authorized key" ja voin kirjautua ilman salasanaa:

![image](https://github.com/user-attachments/assets/3409e99c-2d35-4515-9ff8-c49f0a2a12bb)

Testasin vielä avaamalla uuden teriminaalin ja ottamalla uuden yhteyden käyttäjään. Avain toimi halutusti, eikä salasanaa tarvitse syöttää:

![image](https://github.com/user-attachments/assets/9c1b1f7b-d538-4c67-8883-1df2ed14f621)


## d) Tutki jonkin nimen DNS-tietoja 'host' ja 'dig' -komennoilla. Käytä kumpaakin komentoa kaikkiin nimiin ja vertaa tuloksia. Katso man-sivulta, miten komennot toimivat - esimerkiksi miten 'dig' näyttää kaikki kentät. Analysoi tulokset. Etsi tarvittaessa uusia lähteitä haastaviin kohtiin. Sähköpostin todentamiseen liittyvät SPF ja DMARC -tietojen yksityiskohdat on jätetty vapaaehtoiseksi lisätehtäväksi. 

Tutkittavat nimet:
  rvuorela.me (Oma domain-nimesi). Vertaa tuloksia nimen vuokraajan (namecheap.com, name.com...) weppiliittymässä näkyviin asetuksiin.
  pieniharrastepuoti.com Jonkin pikkuyrityksen, kerhon tai yksittäisen henkilön weppisivut. (Ei kuitenkaan kurssikaverin tällä viikolla vuokrattua nimeä).
  haaga-helia.fi Jonkin suuren ja kaikkien tunteman palvelun tiedot.

Aloitus 24.9. 12.50 lopetus
Manuaaleja ei löytynyt suoraan ja selvisi, että host ja dig komentoja ei ole asennettuna. Koitin asentaa ne sudo apt-get -y install host dig -komennolla. Hostin osalta latasi bind9-hos ohjelman. Tältä sivulta löysin, että molemmat komennot host ja dig löytyvät bind9 alta: https://bind9.readthedocs.io/en/v9.18.14/manpages.html Latasin bind9n komennolla sudo apt-get -y install bind9:

![image](https://github.com/user-attachments/assets/c6fabbdc-07aa-468a-9130-7b22b367f5e8)

![image](https://github.com/user-attachments/assets/03846285-f58a-4b20-bff7-97524643e2dd)

Jostain syystä en saa manuaaleja auki komentoriviltä, joten käytän nettisivua apuna: https://bind9.readthedocs.io/en/v9.18.14/manpages.html#host-dns-lookup-utility

Dokumentaation mukaan host komento muuttaa nimen IP-osoitteeksi ja toisin päin.
Koitin host komentoa rvuorela.me nimelle, mutta sain taas virheviestin bash: host: command not found. Tässä kohtaa pyysin chat-Gptltä apua ja vastauksena sain, että minun täytyy asentaa dnsutensils. Asensin siis komennolla: sudo apt-get -y install dnsutils. Tämän jälkeen pääsin myös man host komennolla manuaaliin. 

Tein uuden yrityksen host rvuorela.me:

![image](https://github.com/user-attachments/assets/86f73e3f-0bab-44e8-9769-d08604f75ca3)

host pieniharrastepuoti.com

![image](https://github.com/user-attachments/assets/7f1ca999-963c-44e8-ba69-5dfc0ba10396)

host haaga-helia.fi

![image](https://github.com/user-attachments/assets/a09d2141-a860-4427-9a66-68f5db157ef2)

Rivien selitykset: 

has address - kertoo domainin IPv4-osoitteen. 
has IPv6 address - kertoo domainin IPv6 osoitteen
- rvuorela.me yksi IP-osoite, joka vastaa Digital Oceanista vuokrattua IP-osoitetta ja namecheapin asetuksissa olevaa IP-osoitetta
- pieni pieniharrastepuoti.com yksi IP-osoite ja yksi IPv6 osoite
- haaga-helia.fi kolme IP-osoitetta

mail is handled by - kertoo mikä sähköpostipalvelin vastaanottaa sähköpostit. Tästä oli vaikea löytää tietoa, mutta tämä sivu kertoi, että kyseinen rivi on MX record https://www.tecmint.com/linux-host-command-examples-for-querying-dns-lookups/ ja täältä löytyi selitys MX recordille: https://www.cloudflare.com/learning/dns/dns-records/dns-mx-record/ 

Dig comentoa käytetään usein vianmäärityksessä: https://bind9.readthedocs.io/en/v9.18.14/manpages.html#std-iscman-dig 

dig 164.90.201.37 rvuorela.me

![image](https://github.com/user-attachments/assets/1c019848-a2c5-45d9-9def-581424420b54)

dig 95.217.27.158 pieniharrastepuoti.com

![image](https://github.com/user-attachments/assets/0a84891f-5f04-4103-a780-a4f12db909fd)


dig 104.26.1.90 haaga-helia.fi

![image](https://github.com/user-attachments/assets/5468fe0b-7f87-4ee9-a5a5-5190a322164e)








  

