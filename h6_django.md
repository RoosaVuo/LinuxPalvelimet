## a) Tee yksinkertainen esimerkkiohjelma Djangolla.
Ohjeet:
Voit käyttää testipalvelinta, kunhan se ei näy Internetiin.
Riittää, kun ohjelmasi näkyy esimerkiksi Django Adminsissa.
Voit halutessasi tehdä aivan samanlaisen kuin Teron CRM-esimerkissä. Jos olet jo taitavampi, voit hieman soveltaa.

Aloitus 29.9. klo 14.55

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
Voit halutessasi tehdä asennuksen omalle, paikalliselle virtuaalikoneelle. Sen ei tarvitse näkyä Internetiin.
Karvinen 2021: Deploy Django 4 - Production Install


