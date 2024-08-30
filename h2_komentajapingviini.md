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


# b) Apt. Asenna kolme itsellesi uutta komentoriviohjelmaa. Kokeile kutakin ohjelmaa sen pääasiallisessa käyttötarkoituksessa. Ota ruutukaappaus. Kaikki terminaaliohjelmat kelpaavat, TUI (text user interface) ja CLI (command line interface). Osaatko tehdä apt-get komennon, joka asentaa nämä kolme ohjelmaa kerralla?
En tiennyt mistä ja millaisia ohjelmia alan etsiä. Löysin tällaisen sivun (https://www.linux.fi/wiki/Komentorivikomennot), jonka perusteella etsin ohjelmia komennolla: apt-cache search (text editor, ssh, units) ja asensin: sudo apt-get -y install nano ssh units

nanosta tuli ilmoitus, että se on jo ladattu ja päivitetään uusimpaan versioon:
![image](https://github.com/user-attachments/assets/c06fc5f2-df36-441b-a911-7e6893beed5b)

Tämän jälkeen oli pitkä lista unpacking/selecting/setting up -rivejä. En erottanut missä kohtaa units asennettiin, joten annoin vielä uuden asennuskäskyn, jonka jälkeen tulikin tieto, että ohjelma on asennettu:
![image](https://github.com/user-attachments/assets/4af31a05-3b04-4d7a-8e3c-d3f10fb0b28c)



# c) FHS. Esittele kansiot, jotka on listattu "Command Line Basics Revisited" kappaleessa "Important directories". Näytä kuvaava esimerkki kunkin tärkeän kansion sisältämästä tiedostosta tai kansiosta. Jos kyseessä on tiedosto, näytä siitä kuvaava esimerkkirivi. Työskentele komentokehotteessa ja näytä komennot, joilla etsit esimerkit.


# d) The Friendly M. Näytä 2-3 kuvaavaa esimerkkiä grep-komennon käytöstä. Ohjeita löytyy 'man grep' ja tietysti verkosta.


# e) Pipe. Näytä esimerkki putkista (pipes, "|").


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
