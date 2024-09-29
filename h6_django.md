## a) Tee yksinkertainen esimerkkiohjelma Djangolla.
Ohjeet:
Voit käyttää testipalvelinta, kunhan se ei näy Internetiin.
Riittää, kun ohjelmasi näkyy esimerkiksi Django Adminsissa.
Voit halutessasi tehdä aivan samanlaisen kuin Teron CRM-esimerkissä. Jos olet jo taitavampi, voit hieman soveltaa.

Aloitus 29.9. klo 14.55 lopetus 16.05

Ensin asensin kehitysympäristön sudo apt-get -y install virtualenv 

![image](https://github.com/user-attachments/assets/808c3f04-8b3b-4d99-994e-859a8d94949b)

Loin env/ nimisen kansion ja asensin python3 ohjelman komennolla virtualenv --system-site-packages -p python3 env/.
Kansio löytyy polusta /home/roosa/env 

![image](https://github.com/user-attachments/assets/0044479c-38fe-4340-b9b1-4ca11caa391e)

Otin virtuaaliympäristön käyttöön komennolla: source env/bin/activate.
Rivin alussa (env) kertoi, että olin virtuaaliympäristössä. 
Tarkastin which pip -komennolla, että olen oikeassa hakemistossa:

![image](https://github.com/user-attachments/assets/ea2b0577-eefb-4f73-a319-7d532cf908bc)

Avasin Python-paketin microlla: micro requirements.txt ja kirjoitin pakettiin django. Tarkastin tiedoston sisällön komennolla cat requirements.txt:

![image](https://github.com/user-attachments/assets/3d0f115b-6754-4807-bc8b-f0f7932b09a3)

Seuraavaksi djangon requirements.txt-tiedoston avulla komennolla pip install -r requirements.txt. Tarkastin asennetun Djangon version komennolla django-admin --version:

![image](https://github.com/user-attachments/assets/bb6d743b-a04b-4c82-9c08-dd470161909f)

Aloitin projektin nimellä roosaproj: django-admin startproject roosaproj.
Siirryin projektiin: cd roosaproj ja käynnistin kehityspalvelimen: ./manage.py runserver

![image](https://github.com/user-attachments/assets/6c131bae-7c3e-49cb-86d5-721d821a8f58)

Avasin kehityspalvelimen http://127.0.0.1:8000/ ja se näytti toivotun aloitussivun: 

![image](https://github.com/user-attachments/assets/32920100-8832-4684-8359-1e8d4f721a84)

Päivitin tietokantaa ja lisäsin superuserin. Jätin nimikohdan tyhjäksi, jolloin nimeksi tulee roosa, lisäsin sähköpostiosoitteen ja salasanan, jonka loin komennolla: pwgen -s 20 1. Pwgen komentoa ei ensin löytynyt, joten asensin sen.

![image](https://github.com/user-attachments/assets/3b6fa477-a4c1-48b3-9478-4a85078cc9b1)

![image](https://github.com/user-attachments/assets/da0d4326-a29f-451b-8039-f631fc253785)

![image](https://github.com/user-attachments/assets/47c076d2-651b-47f2-9b1c-25614b704353)

Testasin superuseria http://127.0.0.1:8000/admin/ -sivulla, mutta sain ensin virheviestin, sillä olin sulkenut palvelimen: Unable to connect Firefox can’t establish a connection to the server at 127.0.0.1:8000. Käynnistin palvelimen uudelleen komennolla ./manage.py runserver ja testasin uudelleen. Pääsin kirjautumissivulle: 

![image](https://github.com/user-attachments/assets/f95511cf-a9d2-4f36-9bb2-e998b8ff3dff)

Pääsin sisälle hallintanäkymään: 

![image](https://github.com/user-attachments/assets/92eae48e-a4c5-406a-ace0-f974491a2c29)

Seuraavaksi aloitin luomaan CRM sovellusta komennolla  ./manage.py startapp crm
Tarkastin, että kansio näkyy. Seuraavaksi lisäsin sovelluksen settings.py-kansioon: micro roosaproj/settings.py

![image](https://github.com/user-attachments/assets/8210ae52-7551-403e-8521-dc1413381fef)

INSTALLED_APPS oli jo muuten kunnossa, joten lisäsin sinnen vain crm-osan:

![image](https://github.com/user-attachments/assets/d724a8eb-187d-48ee-be3f-a64c7cdd9318)

Sitten lisäsin crm/ kansioon mallit komennolla micro crm/models.py. Lisäsin tiedostoon määritykset asiakas-taulua varten:

![image](https://github.com/user-attachments/assets/774f6d43-da91-42e0-ad31-81c887843ba9)

![image](https://github.com/user-attachments/assets/f3e1921a-e84c-4c93-9f2f-ae02ca764cdd)

Otin muutokset käyttöön: ./manage.py makemigrations ja ./manage.py migrate 

![image](https://github.com/user-attachments/assets/2ee43ca4-7ad2-468a-a55d-5237e65e0f6c)

Ja rekisteröin tietokannan adminin nähtäväksi micro crm/admin.py 

![image](https://github.com/user-attachments/assets/87b1f3df-57df-4342-8837-d78ce0dd8e57)

Käynnistin palvelimen uudelleen ./manage.py runserver -komennolla. Tarkastin, että CRM-sovellus ja se Customers-taulu oli tullut näkyviin:

![image](https://github.com/user-attachments/assets/3b81b9bd-1e11-4a99-b686-69d39cf6a802)

Testasin +add toiminnolla lisäämistä ja se toimi:

![image](https://github.com/user-attachments/assets/5c7dde8e-fa15-4ab2-acdd-2ccb710cb89c)

Lisäsin vielä 2 asiakasta ja poistin yhden asiakkaan klikkaamalla haluttua riviä ja sen jälkeen Delete-nappia ja Yes, I'm sure vahvistusnappia:

![image](https://github.com/user-attachments/assets/0f7a0efb-e219-4389-80eb-1d78664439b4)

Sivulla näkyy oikein kolme asiakasta: 

![image](https://github.com/user-attachments/assets/bbab8920-cc23-4be7-8524-23cc2f8a8509)

Muokkasin näkymää niin, että listalla näkyy asiakkaiden nimet. Muokkasin models.py tiedostoa micro crm/models.py:

![image](https://github.com/user-attachments/assets/fcf9cb38-301a-4570-a7e4-db7aedd54523)

Käynnistin kehityspalveimen uudestaan (komento: ./manage.py runserver)  ja testasin, että nimet näkyvät. Nimet näkyvät, eli toimi: 

![image](https://github.com/user-attachments/assets/32f6f69e-2a25-4bb1-909d-e0db63266bf5)




Lähde Karvinen 2021: Django 4 Instant Customer Database Tutorial https://terokarvinen.com/2022/django-instant-crm-tutorial/ 

## b) Tee Djangon tuotantotyyppinen asennus
Ohje: Voit halutessasi tehdä asennuksen omalle, paikalliselle virtuaalikoneelle. Sen ei tarvitse näkyä Internetiin.
Lähde: Karvinen 2021: Deploy Django 4 - Production Install https://terokarvinen.com/2022/deploy-django/ 

29.9. aloitus klo 17.35 lopetus 19.15 välissä tauko uusi aloitus 20.15

Testasin localhostin aloitussivun, olin muokannut sitä aiemmin niin, että näky teksti "Default":

![image](https://github.com/user-attachments/assets/1698d3d8-9910-4446-91dd-9cfc2edfeaa4)

![image](https://github.com/user-attachments/assets/ea081afe-fca1-4a3a-bf15-9680ca915279)

Tein kotihakemistoon hakemistot publicwsgi/roosaproj/static/ ja sinne oletustekstin komennolla: 
echo "roosaproj/static toimii"|tee publicwsgi/roosaproj/static/index.html

![image](https://github.com/user-attachments/assets/41e4d2e6-09cc-4db6-b4ff-d4f5efad5b5b)

Loin uuden Virtualhostin komennolla sudoedit /etc/apache2/sites-available/roosaproj.conf ja lisäsin tarvittavat tiedot:

![image](https://github.com/user-attachments/assets/a9ca1777-5ed2-4dba-a0ea-657489c1a64d)

Aktivoin uuden sivun (sudo a2ensite roosaproj.conf) ja otin muut pois käytöstä (sudo a2dissite 000-default.conf ).
Tarkastin konfiguroinnin (/sbin/apache2ctl configtest). Teron ohjeen mukaan AH00558 + Syntax ok, on ok ja voi jatkaa. Katson toimiiko sivu AH00112 varoituksesta huolimatta.

![image](https://github.com/user-attachments/assets/8235d400-faf9-4bad-a842-73e89bea0e8b)

Käynnistin apachen uudelleen komennolla sudo systemctl restart apache2. Sain virheviestin 404 Not Found 

![image](https://github.com/user-attachments/assets/9b9dfeb9-9107-48a1-9946-17ebe59f7480)

Otin hattu.example.comin pois käytöstä, mutta se ei auttanut:

![image](https://github.com/user-attachments/assets/72951850-686f-4283-9fc2-c93fe196822b)

Kysyin chatGptltä nuevoa ja koitin antaa read and execute -oikeudet, jotta apache voi operoida, mutta tämäkään ei auttanut: 

![image](https://github.com/user-attachments/assets/05e2d4bb-91f6-440a-a116-e2dd4c2635ae)

Menin index.html tiedostoon ja se näyttikin tyhjältä, vaikka olin aiemmin lisännyt tekstiä. Lisäsin uudestaan tekstiä, mutta silti sain 404 virheviestin:

![image](https://github.com/user-attachments/assets/96e4c6d0-8c67-4f5b-9379-577406630283)

Accesslog:

![image](https://github.com/user-attachments/assets/a0d1e343-9b8b-437c-be51-fda1b8c6964d)

ErrorLog:

![image](https://github.com/user-attachments/assets/ad4abe97-d8a3-4253-93d3-883b6aaf2810)

Tarkastin tiedostojen nimet ja polut ja koitin uudelleen ottaa muut sivut pois käytöstä ja käynnistin apachen uudelleen, mutta virhe pysyi silti:

![image](https://github.com/user-attachments/assets/e6afda81-d154-4000-8e70-c679c61d69b1)

Siirryin katsomaan hosts tietoja: sudoedit /etc/hosts. Otin This host address -kohdasta kaikki aiemmilla viikoilla lisäämäni pois:

![image](https://github.com/user-attachments/assets/32ebd001-aeaf-4bfd-8330-359580c43c94)

Tämäkään ei auttanut vaan sain edelleen 404 virheilmoituksen:

![image](https://github.com/user-attachments/assets/269d6d76-5f24-42de-b126-232bd6d50f8a)

Pidin välissä tauon. Sammutin virtuaalikoneen ja käynnistin uudelleen. 






