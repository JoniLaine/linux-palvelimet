# h6 Salataampa

Tässä osiossa luodaan SSL-salaus (hhtps) weppisivustolle.

Aikaa kulunut: 0:00

## x) Lue ja tiivistä. Tiivistelmäksi riittää muutama ranskalainen viiva per artikkeli. (Tässä alakohdassa ei tarvitse tehdä testejä tietokoneella)

## a) Let's. Hanki ja asenna palvelimellesi ilmainen TLS-sertifikaatti Let's Encryptilta. Osoita, että se toimii.

Kirjauduin SSH-käyttäjälle, asensin Legon ja sille oman kansion komennoilla:

`$ cd /home/joni/`

`$ sudo apt-get install lego`

`$ cd`

`$ mkdir lego`

Ja tarkistin kansion olevan luotu:

`$ ls`

![Add file: Upload](h6_Kuva100.png)

Loin testiympäristön SSL-sertifikaatin toimivuuden varmistamiseksi. Tämän vaiheen tein, koska `Let's encrypt` rajoittaa yritysten määrän viiteen (5) yritykseen, jonka jälkeen uuden yrityksen saa tehdä vasta tietyn ajan kuluttua. Dokumentaation mukaan aikaraja olisi yksi (1) tunti.

Käytin testiympäristön luonnissa komentoa:

```
lego --server=https://acme-staging-v02.api.letsencrypt.org/directory --accept-tos --email="joni.tk.laine@gmail.com" --domains="ikolainen.com" --domains="www.ikolainen.com" --http --http.webroot="/home/joni/public_sites/ikolainen.com/" --path="/home/joni/lego/" --pem run

```

Sähköpostiksi annoin oman sähköpostini ja domaintiedoiksi aiemmin luomani domainin tiedot. Sertifikaatin sijainniksi annoin polun omalle ikolainen.com tiedostolle. Lopussa näkyvä `run`-komento ajoi annetun käskyn.

![Add file: Upload](h6_Kuva101.png)

Yllä oleva kuva näyttää sertifikaation luonnin onnistuneen. Kokeilin siis nimetä kyseisen tiedoston uudelleen toiselle nimelle, jotta pääsen kokeilemaan todellisen sertifikaatin luontia.

Käytin komentoja:

`$ cd /home/joni/`

`$ pwd`

`$ mv -n lego testilego`

`$ ls`

![Add file: Upload](h6_Kuva102.png)

Loin uuden lego-kansion komennolla:

`$ mkdir lego`

![Add file: Upload](h6_Kuva104.png)

Latasin oikean sertifikaatin komennolla:

```
lego --accept-tos --email="joni.tk.laine@gmail.com" --domains="ikolainen.com" --domains="www.ikolainen.com" --http --http.webroot="/home/joni/public_sites/ikolainen.com/" --path="/home/joni/lego/" --pem run

```

![Add file: Upload](h6_Kuva105.png)

Sertifikaatin luonti näytti onnistuneen, muttta tarkistin tilanteen vielä käyttämällä alla olevaa kometoa:

`$ find /home/joni/lego/`

![Add file: Upload](h6_Kuva103.png)


![Add file: Upload](h6_Kuva106.png)

Avasin portin SSl-yhteyttä varten (443) komennolla:

`$ cd /etc/apache2/sites-available/`

`$ sudo ufw allow 443/tcp`

![Add file: Upload](h6_Kuva107.png)

Tarkistin komennon toimineen:

`$ /etc/apache2/sites-available`

`$ sudo ufw status`

![Add file: Upload](h6_Kuva109.png)

Kävin muokkaamassa juuri avatun portin ikolainen.com.conf-tiedostoon tarvittavan lisäyksen SSL-yhteyttä varten:

```
<VirtualHost *:443>
  ServerName ikolainen.com
  ServerAlias www.ikolainen.com
  SSLEngine On
  SSLCertificateFile '/home/joni/lego/certificates/ikolainen.com.crt'
  SSLCertificateKeyFile '/home/joni/lego/certificates/ikolainen.com.key'
  DocumentRoot /home/joni/public_sites/ikolainen.com
  <Directory /home/joni/public_sites/ikolainen.com>
    Require all granted
  </Directory>
</VirtualHost>
```

![Add file: Upload](h6_Kuva108.png)


![Add file: Upload](h6_Kuva110.png)

![Add file: Upload](h6_Kuva111.png)

![Add file: Upload](h6_Kuva112.png)

## b) A-rating. Testaa oma sivusi TLS jollain yleisellä laadunvarmistustyökalulla, esim. SSLLabs (Käytä vain tavanomaisia tarkistustyökaluja, ei tunkeutumistestausta eikä siihen liittyviä työkaluja)

## c) Vapaaehtoinen: Tee weppilomake, jossa on käyttäjätunnus ja salasana. Käytä salaamatonta http-yhteyttä. Sieppaa liikennettä (esim. Wireshark, ngrep). Mitä havaitset? Mitä vaikutuksia tällä on tietoturvaan?



## Lähdeluettelo

- Tero Karvinen, Linux Palvelimet 2025: https://terokarvinen.com/linux-palvelimet/





## Tekijä

### Joni Laine

### Haaga-Helia, IT-Tradenomiopiskelija

Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. (http://www.gnu.org/licenses/gpl.html)

