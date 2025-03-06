# h3 Hello Web Server

Huomioitavaa: raportissa on käytetty aikaa pituusmääreenä virheellisesti kellonajan ja päivämäärän sijaan.

Aikaa kulunut: 0:00

## Weppipalvelin localhost-osoitteessa ja Apache

Apache-weppipalvelin oli valmiina asennettuna koneelle.
Testasin weppipalvelimen vastaamisen terminaalissa komennolla:

`$systemctl restart apache2`

Komento promptasi salasanan syöttöruudun, johon annoin salasanan ja painoin `Enter`.

Kokeilin sivun vastaamisen Firefox-selaimella osoitteella http://localhost sekä https://127.0.0.1

 ![Add file: Upload](h3_Kuva1.png)
 
 ![Add file: Upload](h3_Kuva2.png)

Aikaa kulunut: 0:05

## Loki weppipalvelimella olevan sivun lataamisesta:

Latasin sivustoni kaksi kertaa uudestaan Firefox-selaimessa.
Palasin terminaaliin ja varmistin olevasi kotihakemistossa komennoilla:

`$ cd /`

`$ pwd`

Yritin lukea lokit seuraavalla komennolla:

`$sudo tail -3 var/log/apache2/access.log`

Komento ei antanut ollenkaan tuloksia. Tarkistin muut lokivaihtoehdot komennolla:

`$ sudo ls var/log/apache2`

 ![Add file: Upload](h3_Kuva5.png)

 Kokeilin lokia other_vhosts_access.logia (koska access.log.1 ja other_vhosts_access.log.1 ovat vanhemmat lokit/historia):

`$ sudo tail -3 var/log/apache2/other_vhosts_access.log`

 ![Add file: Upload](h3_Kuva4.png)

Komento antoi toivotusti kolme viimeistä lokia nähtäville.

Aikaa kulunut: 0:20

## Nimipohjainen - vs. IP-pohjainen virtuaali-isäntä (host)

-	IP-pohjaiset virtuaali hostit määrittävät virtuaali-isännän IP-osoitteen avulla ja tarvitsevat siksi oman IP:n jokaisella hostille
-	Nimi-pohjainen virtuaali host saa clientilta http-otsikon mahdollistaen näin useamman hostin jakaa saman IP:n
-	Nimipohjainen virtuaali hosting on ensisijaisesti käytettävä tapa nykyään ja helpommin hallinnoitava ja sitä tulisi suosia myös rajallisten IP-osoitteiden vuoksi, ellei IP-pohjainen virtuaali hostaus ole ehdotonta esimerkiksi laitekannan vuoksi
  
## Miten palvelin valitsee oikean virtuaali-isännän
-	Nimipohjainen virtuaali-isäntä rajaa ensin osuvimman IP-osoitteen ja etsii sitten sopivimman virtuaali-isännän
-	Ollessa useampi nimipohjainen isäntä samalla osoitteella ja portilla, jatkuu tarkimman osuman hakeminen ServerNamella ja ServerAliaksella, jos jälkeen mainituista ei löydy osumaa, käytetään ensimmäistä osumaa löydetyltä virtuaali-isäntien listalta
  
## Nimipohjaisten virtuaali-isäntien käyttö
-	Jokainen virtuaali-isäntä -lohko (`<VirtualHost>` ) tarvitsee ServerNamen ja DocumentRootin (vähimmäisvaatimus)
-	Oletusvirtuaali-isäntä on järkevää luoda, kun olemassa olevaan palvelimeen luodaan uusia virtuaali-isäntiä, joilla käytetään samaa konfiguraatiota
-	ServerName periytyy peruspalvelimen konfiguraatiosta, mikäli sitä ei ole erikseen määritelty virtuaali-isännälle, tämän vuoksi se on aina syytä tehdä parhaan resoluution saavuttamiseksi
-	Parempien osuvuuksien saamiseksi erilaisilla sivuston kirjoitusasuilla, tulee tehdä muutokset sekä DNS-palvelimelle että ServerName tai ServerAliakseksi
-	Nimipohjaisten virtuaali-isäntien avulla on mahdollista ei ainoastaan olla monta weppisivua saman IP-osoitteen takana vaan myös useampia domaineja

Aikaa kulunut: 1:10

## Lokin analyysi:

 ![Add file: Upload](h3_Kuva4.png)

Analysoidaan yksi rivi, joka on muodostunut yhdestä weppisivun latauksesta. Tässä tapauksessa tarkastellaan siis kahta alinta riviä komennon antamasta vastauksesta:
  
`sivu.example.com:80 127.0.0.1 - - [30/jan/2025:18:59:33 +0200] "GET  / HTTP/1.1" 304 247 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:128.0) Gecko/20100101 Firefox/128.0"`

#### sivu.example.com

Palvelimen nimi.

#### 80

Palvelimen portti, johon pyyntö lähetetään. Kyseinen portti 80, on tarkoitettu erityisesti http-liikenteelle ja on kyseistä protokollaa käyttävän liikenteen oletusportti.

#### 127.0.0.1

Palvelimelle pyynnön tehneen clientin IP-osoite (127.0.0.1 viittaa samaan laitteeseen kuin missä palvelin sijaitsee).

#### [30/jan/2025:18:59:33 +0200]

Pyynnön tekoaika (30. tammikuuta 2025; kello 18:59:33 UTC +2).

#### GET  / HTTP/1.1

GET-tyypin http-pyyntö sivun juurisivulle (`/`); http-versio (`1.1`). GET on hakupyyntö, eli pyytää tietoja palvelimelta. Tässä tapauksessa weppisivua ja sen sisältöä.

#### 304 

Vastauskoodi pyyntöön. Saatu vastauskoodi 304 tarkoittaa, että sisällössä ei ole muutosta viimeisimpään pyyntöön nähtynä.

#### 247

Vastauksen koko tavuina(B).

#### -

Viittauslähde, joka on tyhjä tässä tapauksessa. Arvona olisi voinut olla esimerkiksi https://google.com, jos pyynnön tekijä siirtyi sivustolle sen sivuston linkkiä käyttämällä.

#### Mozilla/5.0 (X11; Linux x86_64; rv:128.0) Gecko/20100101 Firefox/128.0

Käyttäjäagentin jälki (User Agent), joka tässä tapauksessa kertoo pyynnön olevan tehty Linux OS:llä (Linux x86_64) ja käyttäen Firefox-selainta (Firefox/128.0), sekä kummankin versiot. Rivin alun Mozilla/5.0 viittaa Mozilla-selaimeen, joka on nykyään tunnettu nimeltään Firefox.
X11 viittaa Unix-pohjaiseen OS:ään, joka on tässä tapauksessa Linux. Rv:128.0 on selaimen versio, joka mainitaan myös jäljen käyttäjäagentin antamassa päätteessä toistamiseen. Gecko/20100101, kertoo kyseessä olevan Mozillan kehittämästä Gecko renderöintimoottorista, joka pystyy mm. verkkosivujen näyttämiseen; 20100101 on tämän kyseisen Geckon versionumero.


Aikaa kulunut: 1:50

## Uusi etusivu hattu.example.com sekä validi HTML5-sivu

Siirryin hakemistoo, `public_sites` ja loin tarvittavan hakemiston komennnolla:

`$ cd mkdir hattu.example.com`

 ![Add file: Upload](h3_Kuva8.png)

 Ja tarkistin käyttöikeudet käyttäjälle joni:

  ![Add file: Upload](h3_Kuva9.png)

Tein seuraavat komennot:

`$ cd /`

`$ cd etc/apache2/`

Tarkistin kansioiden nimet:

`$ cd ls`

Ja siirryin tarvitsemaani sijaintiin:

`$ cd sites-enabled`

Ja suljin aiemman sivuston:

`$  sudo a2dissite sivu.example.com.conf`

Käynnistin Apachen uudestaan:

`$ cd systemctl restart apache2`

  ![Add file: Upload](h3_Kuva11.png)

Loin hattu.example.com.conf tiedoston komennolla:

`$ cd nano hattu.example.com.conf`

  ![Add file: Upload](h3_Kuva12.png)

Tein komennot tallentaakseni ja sulkeakseni tiedoston:

`ctrl + O` 
`Enter` 
`ctrl + X`

Aktivoin hattu.example.com sivun ja käynnistin Apachen uudestaan:

`$ cd sudo a2ensute hattu.example.com`

`$ cd sudo systemctl restart apache2`

  ![Add file: Upload](h3_Kuva14.png)

Siirryin takaisin juurivalikkoon ja menin tarkistamaan public_sites kansion tilanteen:

`$ cd home/joni`

`$ cd public_sites`

`$ ls`

 ![Add file: Upload](h3_Kuva15.png)

Tarkistin varmuudeksi, että vanha sivu oli epäaktivoitu ja uusi aktivoitu:

 ![Add file: Upload](h3_Kuva16.png)

Seuraavaksi siirryin kirjoittamaan sisällön hattu.example.com tiedostoon:

`$ cd`

`$ cd etc/apache2/`

`$ nano hattu.example.com`

Valitsin Virtuaalikoneen välilehdeltä Devices > Shared clipboard > Host To Guest, koska olin kirjoittanut hattu.example.com sivulle HTML5 scriptin, jonka olin testannut käyttäen validaattoria https://validator.w3.org/, ja kopioin tekstin host-koneelta hatty.example.com tiedostoon virtuaalikoneelle.

![Add file: Upload](h3_Kuva17.png)

Annoin seuraavat komennot tallentaakseni ja sulkeakseni tiedoston ja käynnistin Apachen uudestaan:

`ctrl + O`

`Enter`

`ctrl + X`

`$ systemctl restart apache2`

Latasin Firefox-selaimen http://localhost sivun uudelleen ja sain seuraavan virheen:

![Add file: Upload](h3_Kuva18.png)

Menin tarkistamaan virhelokin sisällön:

`$ cd /`

`$ cd var/ log`

`$ sudo tail -1 apache2/error.log`

![Add file: Upload](h3_Kuva19.png)

Huomasin, että index.html ei ollut määritelty ja että myös hattu.example.com.conf tiedosto oli tyhjä.
Tein komennon päästäkseni antamaan tarvittavat tiedot hattu.example.com.conf tiedostolle:

`$ sudo nano /etc/apache2/hattu.example.com.conf`

 Lisäsin tiedostoon sisällöksi:

 ![Add file: Upload](h3_Kuva17.png)

Annoin seuraavat komennot tallentaakseni ja sulkeakseni tiedoston:

`ctrl + O`

`Enter`

`ctrl + X`

Siirryin hattu.example.com kansioon seuraavilla komennoilla:

`$ cd /`

`$ cd public_sites`

`$ cd hattu.example.com`

`$ nano index.html`

ja annoin tiedostolle haluamani HTML-sisällön:

 ![Add file: Upload](h3_Kuva19.png)

Annoin seuraavat komennot tallentaakseni ja sulkeakseni tiedoston:

`ctrl + O`

`Enter`

`ctrl + X`

Sain seuraavan virheen ladattuani selaimella sivun uudestaan:

 ![Add file: Upload](h3_Kuva20.png)

Menin tarkistamaan jälleen virhelokin:

`$ cd /`

`$  cd var/log/`

`$ sudo tail -1 apache2/error.log`

 ![Add file: Upload](h3_Kuva18.png)

En ollut täysin varma, mitä kyseinen virhe tarkoitti, joten kävin läpi aiemmin tekemäni vaiheet, joissa huomasin kirjoitusvirheen tiedostossa hattu.example.com.conf ja kävin korjaamassa tämän. Vian syy ei ollut kyseinen virhe, mutta korjasin tämän kuitenkin, kun sen huomasin.

![Add file: Upload](h3_Kuva20.png)

Siirryin seuraavaksi korjaamaan hosts-tiedoston sisällön viittaamaan oikeaan sivuun:

`$ cd /`
 
`$ cd /etc/`

`$ sudo nano hosts`

Vaihdoin uuden URL:in tiedostoon:

![Add file: Upload](h3_Kuva20.png)

Käynnistin Apachen uudestaan:

`$ systemctl restart apache2`

Ja latasin Firefox-selaimessa sivun uudestaan. Sivu ei edelleenkään toiminut vaan antoi samaa virhettä.

Aikaa kulunut: 2:50

**Tämän jälkeen alkoi armoton vianselvitys, jonka suosittelen jättämään välistä ja siirtymään suoraan ratkaisuun. Sillä voi säätyä paljolta ylimääräiseltä vaivalta. Ratkaisu on merkitty paksunnetusti tekstillä "RATKAISU""**

Luin jälleen Apachen error.login, mutta se ei valitettavsti tuottanut juurikaan iloa, enkä löytänyt syytä virheelle.

![Add file: Upload](h3_Kuva21.png)

Kokeilin tässä vaiheessa huvikseni kokeilla siirtyä selaimessa suoraan sivulle http://hattu.example.com ja huomasin sen toimivan oikein:

![Add file: Upload](h3_Kuva23.png)

Lopputulema oli siis, että ylemmän kuvan mukaisesti suora URL sivulle toimi, mutta http://localhost antoi nyt virheen `404`:

 ![Add file: Upload](h3_Kuva24.png)

Koska olin tarkistanut, että ainoastaan hattu.example.com.conf, hattu.example.com, index.htlm sekä hosts-tiedosto olivat kaikki sisällöltään oikein ja ainoastaan sivusto hattu.example.com oli aktiivisena lähdin kokeilemaan selaimessa asiaa eteenpäin. Yritin päivittää sivun pitäen pohjassa shift-painiketta, mutta edelleenkään http://localhost ei vastannut vaan antoi samaa `404` virhettä. Kokeilin että sekä http://hattu.example.com että http://127.0.0.1 vastasivat kumpikin oikein.

**RATKAISU**

Päätin sulkea koko Firefox-selaimen ja avata sen uudestaan. Tämän jälkeen myös http://localhost näytti sivun oikein:

 ![Add file: Upload](h3_Kuva25.png)

Aikaa Kulunut: 4:00

## cURL -I ja cURL

### Mitä `curl -I` kertoo?

`$ curl -I  localhost`

 ![Add file: Upload](h3_Kuva27.png)

 CURL- I hakee vastausotsakkeiden perusteella yksinkertaisemman analyysin sisällöstä ja on yleensä riittävä testejä varten.

### Otsakkeiden selitteet:

**HTTP/1.1 200 OK**

HTTP-versio (`1.1`) ja tilakoodi (`200 OK`).

**Date: Sat, 01 Feb 2025 16:56:28 GMT**

Aikaleima, joka kertoo, milloin palvelin lähetti vastauksen.

**Server: Apache/2.4.62 (Debian)**

Palvelimen ohjelmiston nimi ja versio.

**Last-Modified: Sat, 01 Feb 2025 13:10:38 GMT**

Viimeisin sivun muokkausaika.

**ETag: "1a3-62d1462b41fd0"**

Entity Tag, selaimet käyttävät otsaketta välimuistin hallintaan. Resurssin (sivun) muuttuessa myös ETag muuttuu.

**Accept-Ranges: bytes**

Otsake ilmoittaa resurssin osittaisen latauksen olevan mahdollista. Palvelimelle voi lähettää esimerkikis pyynnön otsakkeella `Range: bytes= 0-30`, jolloin palvelin antaa osittaisen vastauksen, joka sisältää sivuston tavut väliltä 0-30 (`206 Partial Content`).

**Content-Length: 419**

Sisällön pituus tavuina (B).

**Vary: Accept-Encoding**

Selain voi lähettää Accept-Encoding otsakkeen palvelimelle ja ilmoittaa näin palvelimelle, mitä pakkausmenetelmää voi käyttää sivun vastauksessa.

**Content-Type: text/html**

Sisällön tyyppi (teksti/html).

### Mitä `curl` tekee?

`$ curl localhost`

 ![Add file: Upload](h3_Kuva26.png)

CURL -komento näyttää terminaalissa sivun (tässä tapauksessa oletussivun localhost) sisällön.

Aikaa kulunut: 4:40


## Lähdeluettelo

- Tero Karvinen: [Linux-palvelimet](https://terokarvinen.com/linux-palvelimet/)
  
- Apache HTTP Server Project, Name based virtual host support: [Name based virtual host support](https://httpd.apache.org/docs/2.4/vhosts/name-based.html)
  
-	Tero Karvinen 2018: [Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address](https://terokarvinen.com/2018/04/10/name-based-virtual-hosts-on-apache-multiple-websites-to-single-ip-address/)
  
- Baeldung Linux: [Guide to the Linux curl Command with examples](https://www.baeldung.com/linux/curl-guide)
  
- Hostinger Tutorials: [What is the cURL-command? Understanding the syntax, options and examples](https://www.hostinger.com/tutorials/curl-command)
  

## Muokkaukset

- 6.3.2025: Muokattu tekijä-osio vastaavaksi muiden raporttien kanssa; Selkeytetty turhan vianetsinnän muotoilua siten, että lukija löytää helpommin, missä ratkaisu on; Siistitty lähdeluettelon ulkoasua
  

## Tekijä

### Joni Laine

### Haaga-Helia, IT-Tradenomiopiskelija

Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. (http://www.gnu.org/licenses/gpl.html)
