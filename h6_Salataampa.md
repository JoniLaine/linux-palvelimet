# h6 Salataampa

Huomioitavaa: raportissa on käytetty aikaa pituusmääreenä virheellisesti kellonajan ja päivämäärän sijaan.

Tässä osiossa luodaan SSL-salaus (hhtps) weppisivustolle.

Aikaa kulunut: 0:00

## x) Tiivistettynä. Katso lähdeluettelo artikkeleista.

- CSR sisältää julkisen avaimen ja on allekirjoitettu vastaavalla yksityisellä avaimella. Agentti allekirjoittaa koko CSR:n valtuutetulla avainparilla, jotta (tässä tapauksessa käytetty) Let’s Encrypt CA tietää, että agentti on valtuutettu.
- Agentti on ohjelmisto, joka hallinnoi sertifikaatteja verkkopalvelimella.
- Hakemiston, tulee olla julkisesti näkyvissä domainilla, jotta validointi onnistuu.
- Portti 443 mahdollistaa SSL-yhteyden.

Aikaa kulunut: 0:45

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

Yritin käynnistää uudestaan Apachen:

`$ sudo systemctl restart apache2`

Sain kuvan mukaisen virheilmoituksen ja muistin, etten ikinä ottanut käyttöön avaamaani yhteyttä, joten annoin seuraavat komennot:

`$ sudo a2enmod ssl`

`$ sudo apache2ctl configtest`

![Add file: Upload](h6_Kuva110.png)

Tulos oli OK joten käynnistin Apachen vielä uudestaan:

`$ sudo systemctl restart apache2`

![Add file: Upload](h6_Kuva111.png)

Ja kokeilin toiminta selaimessa lataamalla sivun pitämällä pohjassa `shift`-näppäintä:

![Add file: Upload](h6_Kuva112.png)

Aikaa kulunut: 1:45

## b) A-rating. Oman sivun TLS testaus laadunvarmistustyökalulla (SSLLabs)

![Add file: Upload](h6_Kuva113.png)

![Add file: Upload](h6_Kuva114.png)

Aikaa kulunut: 1:50


## Lähdeluettelo

- Tero Karvinen, Linux Palvelimet 2025: https://terokarvinen.com/linux-palvelimet/
- https://letsencrypt.org/how-it-works/
- https://go-acme.github.io/lego/usage/cli/obtain-a-certificate/index.html#using-an-existing-running-web-server
- https://httpd.apache.org/docs/2.4/ssl/ssl_howto.html#configexample
- https://www.ssllabs.com/
- https://github.com/gianglex/Linux-palvelimet/blob/main/h6/h6-salataampa.md


## Muokkaukset

- 3.6.2025: Lisätty huomio raportin alkuun virheellisestä aikamääreen käytöstä


## Tekijä

### Joni Laine

### Haaga-Helia, IT-Tradenomiopiskelija

Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. (http://www.gnu.org/licenses/gpl.html)

