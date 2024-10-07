## a) Kirjoita ja aja "Hei maailma" kolmella kielellä.

3.10. Aloitus klo 20.26 lopetus 20.46
Valisin kieliksi Pythonin, Bashin ja Rubyn. Lähteenä Teron https://terokarvinen.com/2018/hello-python3-bash-c-c-go-lua-ruby-java-programming-languages-on-ubuntu-18-04/

### Python
Loin tiedoston heimaalila.py ja lisäsin sinne koodia:  

![image](https://github.com/user-attachments/assets/4717f08f-64ee-4623-a43c-1c0e7dd2eabf)

Ajoin koodin Pythonilla ja sain oikean tekstin "Hei maailma":


![image](https://github.com/user-attachments/assets/fd835467-e611-4600-9f08-d1fc3700781c)

### Bash

Loin tiedoston heimaailma.sh ja lisäsin sinne komennon:

![image](https://github.com/user-attachments/assets/8043595c-c620-484d-aa39-136f63daa4d3)

bash-komennolla tuli haluttu teksti:

![image](https://github.com/user-attachments/assets/92d063d6-c925-4669-9f7a-a0a35cc7bf36)

### Ruby

Loin tiedoston heimaailma.rb ja lisäsin sinne koodin:

![image](https://github.com/user-attachments/assets/506f013b-f176-44ce-9cf6-9503f35e2713)

Koitin ajaa koodin ruby-komennolla, mutta Rubya ei löytynyt, joten asensin sen:

![image](https://github.com/user-attachments/assets/5cf88493-4ce0-4520-b656-b9c2aee3fd49)

Koitin toisen kerran ajaa koodin ja se toimi: 

![image](https://github.com/user-attachments/assets/8133c261-8f71-4141-89c5-57c17323b18b)



## b) Laita Linuxiin uusi komento niin, että kaikki käyttäjät voivat ajaa sitä.

3.10. aloitus: 21.00 lopetus 21.34

Tutkin ensin Teron ohjetta, jota käytin lähteenä: https://terokarvinen.com/2007/12/04/shell-scripting-4/

Tein tiedoston lspwd ja lisäsin sinne komennot:

![image](https://github.com/user-attachments/assets/94f24da7-72b5-4f11-9cc0-81a16197cbf4)

Käytin komentoa chmod a+x lspwd, joka lisää kaikille käyttäjille (a) oikeuden suorittaa/käynnistää kyseisen tiedoston (x) Lähde man chmod:

![image](https://github.com/user-attachments/assets/7f95db10-2418-4e57-a8ec-8cb01bd76eb2)

Suoritin lspwd:n ja sain halutun näkymän, eli sen hetkisen hakemiston sisällön ja polun:

![image](https://github.com/user-attachments/assets/4561e2e3-fc7f-44d5-b3dd-84c598c2e9ef)

Seuraavaksi kopioin tiedoston polkuun /usr/local/bin/ komennolla sudo cp lspwd /usr/local/bin/. Testasin toimivuutta siirtymällä hakemistossa kaksi kertaa ylemmäs ja suorittamalla lspwd:n. Tulos oli oikein, eli toimi:

![image](https://github.com/user-attachments/assets/01e5f63a-c4d3-434f-80d8-81111a84fee8)

Loin uuden käyttäjän testaamista varten: 

![image](https://github.com/user-attachments/assets/71c91c50-37d3-49f5-bc79-10f4110f7aae)

Otin ssh yhteyden esteritesteri käyttäjään:

![image](https://github.com/user-attachments/assets/e6697c90-5ebe-4d15-bf93-7abd714ae4bb)

Ja testasin, että lspwd toimii ja se toimi = näytti kyseisen kansion sisällön ja polun:

![image](https://github.com/user-attachments/assets/69e08c8f-41e2-4fb9-89b1-c90999bb443e)


## c) Ratkaise vanha arvioitava laboratorioharjoitus soveltuvin osin.

Valitsin laboratorioharjoitukseksi: 
https://terokarvinen.com/2024/arvioitava-laboratorioharjoitus-2024-linux-palvelimet/

Alkutiedot: asensin uuden virtuaalikoneen, päivitin sen ohjelmat ja asensin palomuurin. 
Aloitus 7.10. klo 8.53

Asensin micron sudo apt-get -y install micro. Loin kotihakemistoon kansion mkdir report ja tiedoston micro index.md
Harjoituksessa sanottiin, että ei tarvitse raportoida joka kohtaa, mutta tein ainakin jonkinlaisen raportin itseäni varten.

### c) Ei kolmea sekoseiskaa - Suojaa raportti Linux-oikeuksilla niin, että vain oma käyttäjäsi pystyy katselemaan raporttia

![image](https://github.com/user-attachments/assets/0171b8f3-8a03-44b7-9a4d-9fbabba0eb15)

### d) 'howdy' Tee kaikkien käyttäjien käyttöön komento 'howdy'. Tulosta haluamaasi ajankohtaista tietoa. Komennon tulee toimia kaikilla käyttäjillä työhakemistosta riippumatta

En ollut varma miten IP-osoitteen sai tarkastettua, joten kysyin ChatGptltä apua ja sain vastauksena komennon ip addr show. Tein tiedoston, johon lisäsin komennot ls, pwd, date ja ip addr show. Muutin oikeuksia ja kopioin komennon kaikkien käyttöön:

![image](https://github.com/user-attachments/assets/46247d22-2d02-41aa-832f-bdb2582a3ab6)

![image](https://github.com/user-attachments/assets/896eb4cb-76cf-496e-84df-10cc1050ff63)

### e) Etusivu uusiksi "AI Kakone" kotisivu. Kotisivu tulee näkyä koneesi IP-osoitteella suoraan etusivulla. Sivua pitää päästä muokkaamaan normaalin käyttäjän oikeuksin (ilman sudoa). Liitä raporttiisi listaus tarvittavien tiedostojen ja kansioiden oikeuksista.
Asensin Apache-weppipalvelimen komennolla sudo apt-get -y install apache2.
Korvasin oletussivun komennolla echo "Default"|sudo tee /var/www/html/index.html
UUden virtualhostin luominen: sudoedit /etc/apache2/sites-available/aikakone.example.com.conf

![image](https://github.com/user-attachments/assets/c71a178e-44a7-4661-b26f-681b804ae18e)

![image](https://github.com/user-attachments/assets/f6ac3e3c-c4e9-4b72-968c-9622bb45d740)

![image](https://github.com/user-attachments/assets/7b3f171e-4685-436a-bd73-91a82aa93a67)

![image](https://github.com/user-attachments/assets/1872a24f-6a16-4bbf-b05f-e0ace6579b55)

Etusivun muokkaaminen: echo "AI Kakone" > /home/roosa/publicsites/aikakone.example.com/index.html

![image](https://github.com/user-attachments/assets/3c6415a5-f5bb-4def-b839-00536e1f151e)

![image](https://github.com/user-attachments/assets/f28be02b-2cd2-4f58-a2f8-80e5de63d957)

Lisäsin hosts tiedostoon ip-osoitteen + aikakone.example.com

![image](https://github.com/user-attachments/assets/2197fb5a-a20f-45d1-b6c7-58e53a2df776)

![image](https://github.com/user-attachments/assets/1be13117-9696-46a4-abb8-299f63444591)

ip-osoitteella tuli vielä oletussivu, joten otin sen pois käytöstä komennolla: sudo a2dissite 000-default.conf. Nyt myös IP-osoitteella tulee AI Kakone -sivu:

![image](https://github.com/user-attachments/assets/f9677304-c459-4801-9e3e-8a425e44585b)

![image](https://github.com/user-attachments/assets/c529cb1c-1682-4082-88f7-f4668c5556a2)

![image](https://github.com/user-attachments/assets/27682bde-97c5-457e-b169-a367424ce1fb)

### g) Salattua hallintaa
Asensin ssh:n sudo apt-get -y install ssh

Tein uuden käyttäjän:  roosate. Komenot sudo adduser roosate

![image](https://github.com/user-attachments/assets/91ac9570-c6c4-4531-ac90-1d6e3479790a)


Automatisoi ssh-kirjautuminen julkisen avaimen menetelmällä, niin että et tarvitse salasanoja, kun kirjaudut sisään. Voit käyttää kirjautumiseen localhost-osoitetta




### h) Djangon lahjat
Asenna omalle käyttäjällesi Django-kehitysympäristö
Tee tietokantaan lista tekoälyistämme, jossa on nämä ominaisuudet
Kirjautuminen salasanalla
Tietokannan muokkaus wepissä Djangon omalla ylläpitoliittymällä (Django admin)
Käyttäjä Erkille, jossa ei ole ylläpito-oikeuksia
Taulu Assistants, jossa jokaisella tietueella on nimi (name)
Jos haluat, voit lisäksi bonuksena laittaa mukaan kentän koko (size)
### h) Tuotantopropelli
Jos olet tässä kohdassa, olet kyllä työskennellyt todella nopeasti (tai sitten teet tätä tehtävää huviksesi kurssin jälkeen). Mutta älä huoli, tässä haastetta, jotta et joudu pyörittelemään peukaloita.
Tee tuotantotyyppinen asennus Djangosta
Laita Django-lahjatietokanta tuotantotyyppiseen asennukseen
Voit vaihtaa tämän sivun näkymään etusivulla staattisen sivun sijasta



## d) Asenna itsellesi tyhjä virtuaalikone arvioitavaa labraa varten. Suosittelen Debian 12-Bookworm amd64, riittävästi RAM ja kovalevyä. Koneella saa olla päivitetyt ohjelmistot (apt-get dist-upgrade) ja tulimuuri. Koneella ei saa olla mitään muita demoneja tai ohjelmia asennettuna kuin nuo ja asennuksen mukana tulevat. Virtuaalikoneella ei saa olla luottamuksellisia tiedostoja, koska opettaja saattaa tarkastella sitä. [Update 2024-10-03 w40 Thu: Tästä d-osioista ei tarvitse kirjoittaa raporttia. Koneelle voi asentaa haluamansa graafisen käyttöliittymän oletusasetuksilla, suosittelen xfce-työpöytää.]
