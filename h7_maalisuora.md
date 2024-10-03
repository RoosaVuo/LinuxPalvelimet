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

https://terokarvinen.com/2024/arvioitava-laboratorioharjoitus-2024-linux-palvelimet/

## d) Asenna itsellesi tyhjä virtuaalikone arvioitavaa labraa varten. Suosittelen Debian 12-Bookworm amd64, riittävästi RAM ja kovalevyä. Koneella saa olla päivitetyt ohjelmistot (apt-get dist-upgrade) ja tulimuuri. Koneella ei saa olla mitään muita demoneja tai ohjelmia asennettuna kuin nuo ja asennuksen mukana tulevat. Virtuaalikoneella ei saa olla luottamuksellisia tiedostoja, koska opettaja saattaa tarkastella sitä. [Update 2024-10-03 w40 Thu: Tästä d-osioista ei tarvitse kirjoittaa raporttia. Koneelle voi asentaa haluamansa graafisen käyttöliittymän oletusasetuksilla, suosittelen xfce-työpöytää.]
