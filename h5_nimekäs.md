Tehtävänanto:

a) Kotisivu. Tee vähintään kolmen erillisen weppisivun kotisivu ja kopioi se näkymään palvelimellesi. Käytä name based virtual hosting tekniikkaa. Sivujen muokkaamisen pitää onnistua ilman pääkäyttäjän oikeuksia, niiden kopioiminen pääkäyttäjänä testisivun paikalle ei käy. Kotisivujen ei tarvitse olla hienoja, mutta niiden tulee olla validia HTML:ää ja linkittää toisiinsa.

23.9. aloitus 12.00

Aloitin muokkaamalla toisella kurssilla tehtyä nettisivupohjaa. Käytin navigaatiorakennetta hyödyksi, mutta muutin sisältöä ja tyyliä. 
Seuraavaksi tutkin "scp -r" komentoa "man scp" komennolla. Tulkitsin tehtävänannon niin, että teen webbisivu hakemiston tiedoistoineen ensin virtualboxin virtuaalikoneelle ja sitten kopioin sen DigitalOceanin kautta vuokratulle palvelimelle. 

Tutkin mkdir käyttöohjetta ja sen jälkeen tein public_html kansion ja sen alle tiedostot:

![image](https://github.com/user-attachments/assets/fb0da562-8058-4295-a2a1-bfcd35ee2f22)

Koitin editoida tiedostoja, mutta olinkin tosiaan luonut hakemistot, enkä tiedostoja. Poistin index, helloworld, heimaailma ja styles hakemistot ja tein tilalle tiedostot:



Lisäsin koodit kuhunkin tiedostoon:

![image](https://github.com/user-attachments/assets/521dfde0-6f99-457d-997e-e3cb501ab11f)



Sivujen kopiointi palvelimelle onnistuu kätevästi ssh:n mukana tulevalla 'scp -r kansio/ tero@example.com:public_html/'. Tai jos haluat tehokkaan, mutta opettelua ja huolellisuutta vaativan työkalun, myös 'rsync' tukee ssh:ta.
https://validator.w3.org


b) Alidomain. Tee kaksi uutta alidomainia, jotka osoittava omaan koneeseesi. Esimerkiksi palvelu on example.com -> linuxkurssi.example.com. Tee toinen alidomain A-tietueella ja toinen CNAME-tietueella. Alidomainit ovat tyypillisesti ilmaisia, kun sinulla on päädomain (example.com).

c) Pubkey. Automatisoi kirjautuminen julkisella SSH-avaimella.

d) Tutki jonkin nimen DNS-tietoja 'host' ja 'dig' -komennoilla. Käytä kumpaakin komentoa kaikkiin nimiin ja vertaa tuloksia. Katso man-sivulta, miten komennot toimivat - esimerkiksi miten 'dig' näyttää kaikki kentät. Analysoi tulokset. Etsi tarvittaessa uusia lähteitä haastaviin kohtiin. Sähköpostin todentamiseen liittyvät SPF ja DMARC -tietojen yksityiskohdat on jätetty vapaaehtoiseksi lisätehtäväksi. Tutkittavat nimet:
  Oma domain-nimesi. Vertaa tuloksia nimen vuokraajan (namecheap.com, name.com...) weppiliittymässä näkyviin asetuksiin.
  Jonkin pikkuyrityksen, kerhon tai yksittäisen henkilön weppisivut. (Ei kuitenkaan kurssikaverin tällä viikolla vuokrattua nimeä).
  Jonkin suuren ja kaikkien tunteman palvelun tiedot.

