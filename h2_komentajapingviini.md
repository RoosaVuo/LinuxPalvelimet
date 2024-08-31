# x) Tiivistelmä Command Line Basics Revisited
Komentoriviohjelmassa liikutaan ja syötetään komentoja hakemistoissa (directory). Alla esimerkkejä komennoista eri tarkoituksiin:
- liikkuminen ja lukeminen: pwd, ls, cd, less, |
- tiedostojen muokkaaminen: mkdir, mv, cp, remdir, rm, rm -r
- turvallinen etäyhteys: ssh, exit, scp -r
- apu/neuvot: man, ls --help, wget -h
- yksi tab painallus täydentää aloitetun tekstin ja kaksi painallusta esittää vaihtoehdot. Tabiä kannattaa käyttää tiedoston lisäämisessä, jotta välttyy kirjoitusvirheiltä
- historia: history
- tärkeät hakemistot: / (juuri), /home/, /home/roosa/, /etc/, /media/, /var/log/
- ylläpitokomennot tehdään sudo -alkuisina
- ohjelmien hallinta: apt-get update, apt-cache search, apt-get -y install, dpkg, apt-get purge
Lähde Tero Karvinen 2020: Command line basics revisited https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited 

Materiaalissa oli paljon uusia komentoja, mutta tunnilla ja materiaalissa käytiin niitä hyvin läpi, joten olen melko luottavainen, että seuraavat tehtävät onnistuvat hyvin.

# a) Micro asennettu:
![image](https://github.com/user-attachments/assets/282bd7b8-7817-46b8-9269-4234cff8439b)


# b) Apt. Asenna kolme itsellesi uutta komentoriviohjelmaa. 
En tiennyt mistä ja millaisia ohjelmia alan etsiä. Löysin tällaisen sivun (https://www.linux.fi/wiki/Komentorivikomennot), jonka perusteella etsin ohjelmia komennolla: apt-cache search (text editor, ssh, units) ja asensin: sudo apt-get -y install nano ssh units

nanosta tuli ilmoitus, että se on jo ladattu ja päivitetään uusimpaan versioon:
![image](https://github.com/user-attachments/assets/c06fc5f2-df36-441b-a911-7e6893beed5b)

Tämän jälkeen oli pitkä lista unpacking/selecting/setting up -rivejä. En erottanut missä kohtaa units asennettiin, joten annoin vielä uuden asennuskäskyn, jonka jälkeen tulikin tieto, että ohjelma on asennettu:
![image](https://github.com/user-attachments/assets/4af31a05-3b04-4d7a-8e3c-d3f10fb0b28c)

Esimerkit:
## SSH 
tutkin ohjeita ja koitin yhteyden ottamista, mutta sain alla olevan viestin, jonka jälkeen en ollut varma miten jatkaa: 
![image](https://github.com/user-attachments/assets/60e3bb35-0d58-451d-aa7b-4afe8a3f2ccc)

## nano
uuden tiedoston luominen:
![image](https://github.com/user-attachments/assets/5b1dc8d6-e0d7-4b0c-91e6-f6bb5567409e)
lisäsin tekstiä:
![image](https://github.com/user-attachments/assets/79281a96-8965-487f-a087-8cf4bc73aab4)

## units 
testasin 1.6 metrin muuttamista jaloiksi: units "1.6 meters" feet:
![image](https://github.com/user-attachments/assets/e65db1b8-6762-4722-ac4d-3b06c0418401)


# c) FHS. "Important directories"
/	Juurihakemisto, ylin hakemisto: 
![image](https://github.com/user-attachments/assets/1cef84e0-d39e-4b53-8b1d-89fd6dc5fec5)

/home/	Home hakemiston alla on kaikkien käyttäjien hakemistot, tässä tapauksessa vain yksi: 
 ![image](https://github.com/user-attachments/assets/ac2ca093-47db-4d4e-b098-0ebf6b6a065e)

/home/roosa/	Käyttäjän kotihakemisto:
![image](https://github.com/user-attachments/assets/745e83ac-f89b-4228-98c6-9086a41b652a)

Esimerkkikansio Desktop omasta kotihakemistosta. Koitin listata hakemiston sisällön, mutta mitään ei tullut. Ihmettelin tätä ja kokeilin tab-toimintoa, jotta saan varmasti oikean kansion auki (napautuksien määrässä on vielä opeteltavaa). Ilmeisesti Desktop kansiossa ei ole kuitenkaan sisältöä.
![image](https://github.com/user-attachments/assets/da6c2a49-bb3e-45f5-b56b-e0a785cbf832)

/etc/	kansion sisältö:
![image](https://github.com/user-attachments/assets/73a27c40-8309-43a7-b167-7483bc45f45a)

Esimerkkitiedosto crontab:
![image](https://github.com/user-attachments/assets/023cce46-d3fc-463d-8b73-cf5901501a9e)

![image](https://github.com/user-attachments/assets/bd492788-6732-4264-85f9-893dc8c3eea7)

/media/ kansion alta löyty yksi kansio: roosa, joka ei näyttäisi sisältävän mitään:
![image](https://github.com/user-attachments/assets/930ad37b-b7e4-4be5-9b7b-fcb2142269bf)

/var/log/	alta löytyvät kansiot:
![image](https://github.com/user-attachments/assets/49ec37a2-0335-425d-a9bb-5f0164a81c91)

Esimerkki alternatives log:
![image](https://github.com/user-attachments/assets/f025c34e-ca3d-426e-923b-678d3093530c)

![image](https://github.com/user-attachments/assets/fcdae216-1ef9-43f6-9173-01ed544a0f5d)


# d) The Friendly M. Näytä 2-3 kuvaavaa esimerkkiä grep-komennon käytöstä. Ohjeita löytyy 'man grep' ja tietysti verkosta.
![image](https://github.com/user-attachments/assets/3ccac8f0-4ee6-4696-8b86-d63e9fd705f1)
testissä komennot   
grep -i "sana" tiedoston nimi = etsii kaikki vastaavuudet tiedostosta, ei huomioi pieniä ja suuria kirjaimia. Tämä ei jotenkin onnistunut, luetteli kaikki vaikka piti tulla vain lammaskoira ja vesikoira

![image](https://github.com/user-attachments/assets/8f8d9c84-daa8-47fa-af44-9dfc5ad211be)

grep -c "sana" tiedoston nimi = laskee montako kertaa sana esiintyy. Samoin tässä tuli virhe. Onkohan tiedostossani vikaa, kun laskee kaikki sanat yhdeksi

![image](https://github.com/user-attachments/assets/9657c194-8d6b-4f9b-b62f-fdd71e2b662d)

grep -l "sana" * = näyttää missä tiedostoissa sana löytyy

![image](https://github.com/user-attachments/assets/f33c215a-dcc1-44d1-8952-83c907c8a5cc)



# e) Pipe. Näytä esimerkki putkista (pipes, "|").
Kokeilin komentoa ls /etc|less
![image](https://github.com/user-attachments/assets/6bf45d68-87f1-4a70-9e96-c478fb0f2caf)

![image](https://github.com/user-attachments/assets/de067952-e8e6-4b32-8030-01f7561e1dc9)

Välilyönnillä pääsee eteenpäin ja b:llä taaksepäin. En löytänyt oikein muita kansioita, joissa olisi ollut paljon sisältä putkituksen testaamiseksi.

# f) Rauta. Listaa testaamasi koneen rauta (‘sudo lshw -short -sanitize’). 
![image](https://github.com/user-attachments/assets/ee1f68cf-1a89-4f86-92db-b5b136209bce)
Järjestelmä on VirtualBox
Listauksessa kerrotaan muisti: 128LiB BIOS ja 2GiB System memory (RAM-muisti).
Prosessori, johon on intergtoitu grafiikkakortti AMD Ryzen 5 5500U with Radeon Graphics. 
input: PnP laitteet PNP0303 ja PNP0f03 - olisivatkohan nämä hiiri ja näppäimistö? Lisäksi integraatio VirtualBoxin hiireen, virtapainike, kaiuttimet ym.
tallennstilaa on 82gt?
levyn tyyppi on cd-asema, jonka koko on 64GB 
display - SVGA 2 Adapter - olisko tämä toinen näyttö?
Lisäksi host-koneeseen viitataan muutamassa kohtaa, mutta en osannut tulkita mitä nämä tarkoittavat



