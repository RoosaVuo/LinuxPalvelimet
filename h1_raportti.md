# Raportin kirjoittaminen

- Hyvän raportin 4 tunnusmerkkiä: toistettavuus, täsmällisyys, helppolukuisuus ja lähteisiin viittaaminen 
- Raportissa kerrotaan mitä on tehnyt, milloin ja millaisessa ympäristössä 
- Ongelmat tulee myös raportoida
- Raportissa ei saa sepitää, plagioida tai käyttää luvatonta kuvaa
Lähde Karvinen, Tero 2006: Raportin kirjoittaminen. https://terokarvinen.com/2006/raportin-kirjoittaminen-4/ 

# FSF Free Software Definition
- Free Software eli vapaa ohjelmisto täyttää neljä vapauden kriteeriä: vapaus käyttää ohjelmaa haluamallaan tavalla, vapaus selvittää miten ohjelmisto toimii ja muuttaa sitä, vapaus jakaa ohjelmiston kopiota ja vapaus jakaa ohjelmiston muokattun version kopiota.
- Ohjelmistoa ei voi pitää vapaana ohjelmistona, jos siitä puuttuu yksikin neljästä kriteeristä.
- Vapaata ohjelmistoa voi käyttää kaupalliseen tarkoitukseen.
Lähde: Free Software Foundation, Inc. 2024: What is Free Software. https://www.gnu.org/philosophy/free-sw.html


# Linuxin asennus
Lähtötiedot: Koneeni on Lenovon 82R4 kannettava. OS Windows 11 Home 64. VirtualBox asennettuna jo koneelle.
Tein harjoituksen kotona perjantaina 23.8.2024
## Lataaminen
17.45 Aloitin lataamisen [sivuston kautta](https://terokarvinen.com/2021/install-debian-on-virtualbox/) klikkaamalla linkkiä debian-live-12.6.0-amd64-xfce.iso . Tuplaklikkasin ladattua tiedostoa ja sen jälkeen kilkkasin "Avaa" ponnahdusikkunassa.

## Uuden virtuaalikoneen luominen
17.48 siirryin VirtualBoxiin. Klikkasin "New" painiketta ja uudessa ikkunassa "Expert Mode" painiketta. Lisäsin seuraavat tiedot: 
![image](https://github.com/user-attachments/assets/4691cc87-7ba2-4351-b793-dd9f61b3717f)

![image](https://github.com/user-attachments/assets/171a8b9f-5fc6-4b05-9baf-3e8f770b9f35)

![image](https://github.com/user-attachments/assets/cd2f065e-4820-4988-8f26-8e6ed710773d)

Lopuksi klikkasin "Finish"

## Debian ISO Image virtuaalikoneen CDROM
17.57 Virtuaalikone on valittu vastemmalta ja klikkasin "Settings". Valitsin vasemmalta "Storage" Controller:IDEn alta valitsin "Empty" Klikkasin oikealta levyn kuvaa ja valitsin Choose/Create a Virtual Optical Disk.
Klikkasin avautuvasta ikkunasta Add ja valitsin debian-live-12.6.0-amd64-xfce sen jälkeen klikkasin "choose". Tämän jälkeen klikkasin "Ok"

## Testaaminen Livellä

18.04 tulpaklikkasin virtuaalikonetta. Valitsin valikosta "Live system (amd64)" ja painon enteriä. Työpöytä aukesi ja kilkkasin vasemmasta yläkulmasta "Applications" ja sieltä "Web Browser". Testasin selaimen toiminnan kirjoittamalla osoiteriveille terokarvinen. Sivu löytyi Googlesta ja klikkasin linkkiä, joka vei minut sivulle.
Suljin selaimen klikkamalla ruksia. Näppäimisto ja hiiri toimivat tässä testissä.

## Deabianin asennus virtuaalikoneelle

18.17. klikkasin virtuaalikoneen työpöydältä "Install Debian". Näyölle tuli seuraava popup, josta klikkasin "Launch anyway". Asennusikkuna tarjoaa kieleksi American English, klikkaan Next. Klikkasin kartalta Suomen ja sen jälkeen Next. Seuraavassa Keyborad näkymässä valitsin vasemmalla olevasta valikosta Finnish, oikeanpuoleiseen valikkoon jäi valinta Default ja klikkasin Next.
Partitions välilehti: klikkasin Erase Disk valinnan. Encrypt system valinnan jätin tyhjäksi. Boot loader location kohtaan jätin oletusvalinnan "Master Boot Record of VBOX HARDDISK". ja Klikkasin Next.
Users välilehti Users: Täytin järjestyksessä nimeni, kirjautumisnimen, koneen nimen ja salasanan. Valinta "Log in automaticallt without asking for password" valinnan jätin tyhjäksi. Ja kilkkasin Next

18.35 Summary välilehti: silmäilin läpi, että kaikki on kuten yllä kuvattu. Klikkasin "Install"

18.47 Asennus on valmis, näkymässä on oletuksena valittu "Restart now" jätän sen valinnan. Klikkaan "Done" ja kone käynnistyi uudelleen.

## Kirjautuminen ja testaus kirjautuneena

18.51 Kirjautumisnäkymä avautui. Kirjauduin sisään omilla tunnuksilla. Valitsin vasemmalta Applications ja sieltä Web Browser. Kirjoitin osoitekenttään haaga-helia.fi. Sivu aukesi ja hiiri sekä näppäimistö toimivat normaalisti. Suljin selaimen raksista.

## Sovellusten päivitys ja palomuurin asennus

19.07 Avasin terminaalin klikkaamalla Applications ja Terminal Emulator. Annoin komennon sudo apt-get update. Terminaali kysyi salasanaa ja syötin sen. Annoin uuden komennon sudo apt-get -y dist-upgrade
19.18 päivitykset valmistuivat. Asensin palomuurin komennolla apt-get -y install ufw. Tästä tuli virheviesti "Could not open lock file ja Unable to acquire the dpkg." Kokeilin uudestaan komennolla sudo apt-get -y install ufw ja onnistui. Syötin komennon sudo ufw enalble. Palomuuri aktivoitui.

19.25 Valitsin Applications valikosta Log out ja Restart. Uudelleenkäynnistyksen jälkeen kirjauduin sisään omilla tunnuksilla.
Tässä välissä pidin tauon.  

## Virtuaalikoneen Guest Additions

19.39 Valitsin ylimmästä valikosta "Devices" ja sieltä "Insert Guest Additions CD image.." Sitten avasin Applications valikon ja avasin "File Manager" osion. Avasin vasemmalta cd-kuvakkeen "VBox_GAs_7...". Avasin Applications valikon ja sieltä Terminal Emulator. Valitsin tiedoston komennolla cd /media/*/VBox*. Syötin komennon ls. ja komennon "sudo bash VBoxLinuxAdditions.run".
19.52 Käynnisitin uudelleen: Valitsin Applications -> Log out -> Restart
19.57. Kirjauduin sisään omilla tunnuksilla. Edellinen komento toimi, eli näyttö laajeni koko ruudulle.
Seuraavaksi valitsin ylimmästä valikosta Machine ja Take snapshot. Annoin nimeksi Snapshot 23.8. ja kuvaukseksi Asennus valmis.
20.05 Lopuksi valitsin Applications -> Log Out -> Shut Down

ASennuksen pohjana Tero Karvinen 2024: Linux kurssi, http://terokarvinen.com ja 2023: https://terokarvinen.com/2021/install-debian-on-virtualbox/ 

