cd ..# x) Tiivistelmä Command Line Basics Revisited
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


# b) Apt. Asenna kolme itsellesi uutta komentoriviohjelmaa. Kokeile kutakin ohjelmaa sen pääasiallisessa käyttötarkoituksessa. Ota ruutukaappaus. Kaikki terminaaliohjelmat kelpaavat, TUI (text user interface) ja CLI (command line interface). Osaatko tehdä apt-get komennon, joka asentaa nämä kolme ohjelmaa kerralla?
En tiennyt mistä ja millaisia ohjelmia alan etsiä. Löysin tällaisen sivun (https://www.linux.fi/wiki/Komentorivikomennot), jonka perusteella etsin ohjelmia komennolla: apt-cache search (text editor, ssh, units) ja asensin: sudo apt-get -y install nano ssh units

nanosta tuli ilmoitus, että se on jo ladattu ja päivitetään uusimpaan versioon:
![image](https://github.com/user-attachments/assets/c06fc5f2-df36-441b-a911-7e6893beed5b)

Tämän jälkeen oli pitkä lista unpacking/selecting/setting up -rivejä. En erottanut missä kohtaa units asennettiin, joten annoin vielä uuden asennuskäskyn, jonka jälkeen tulikin tieto, että ohjelma on asennettu:
![image](https://github.com/user-attachments/assets/4af31a05-3b04-4d7a-8e3c-d3f10fb0b28c)



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
grep -i "sana" tiedoston nimi = etsii kaikki vastaavuudet tiedostosta, ei huomioi pieniä ja suuria kirjaimia
grep -c "sana" tiedoston nimi = laskee montako kertaa sana esiintyy
grep -l "sana" * = näyttää missä tiedostoissa sana löytyy


# e) Pipe. Näytä esimerkki putkista (pipes, "|").
Kokeilin komentoa ls /etc|less
![image](https://github.com/user-attachments/assets/6bf45d68-87f1-4a70-9e96-c478fb0f2caf)

![image](https://github.com/user-attachments/assets/de067952-e8e6-4b32-8030-01f7561e1dc9)

Välilyönnillä pääsee eteenpäin ja b:llä taaksepäin. En löytänyt oikein muita kansioita, joissa olisi ollut paljon sisältä putkituksen testaamiseksi.

# f) Rauta. Listaa testaamasi koneen rauta (‘sudo lshw -short -sanitize’). Asenna lshw tarvittaessa. Selitä ja analysoi listaus.




Ohjelmien asennus
sudo apt-get update
apt-cache search version control
apt-cache show git
sudo apt-get -y install git
Selitä ja analysoi - rautatehtävässä tärkeää on siis oma analyysi ja selitys, ei pelkkä listaus
Lokit
journalctl -f
sudo journalctl
