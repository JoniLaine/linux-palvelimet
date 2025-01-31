# h3 Hello Web Server

Aikaa kulunut: 0:00

## Weppipalvelin localhost-osoitteessa ja Apache

Apache-weppipalvelin oli valmiina asennettuna koneelle.
Testasin weppipalvelimen vastaamisen terminaalissa komennolla:

´$systemctl restart apache2´

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

-	Analysoidaan yksi rivi, joka on muodostunut yhdestä weppisivun latauksesta. Tässä tapauksessa tarkastellaan siis kahta alinta riviä komennon antamasta vastauksesta:
`sivu.example.com:80 127.0.0.1 - - [30/jan/2025:18:59:33 +0200] "GET  / HTTP/1.1" 304 247 "-" "Mozilla/5.0 (X11; Linux x86_64; rv:128.0) Gecko/20100101 Firefox/128.0"`

### sivu.example.com: 

palvelimen nimi

### 80: 

palvelimen portti

### 127.0.0.1

palvelimelle pyynnön tehneen IP-osoite (127.0.0.1 viittaa samaan laitteeseen kuin missä palvelin sijaitsee)

### [30/jan/2025:18:59:33 +0200]

pyynnön tekoaika (30. tammikuuta 2025; kello 18:59:33 UTC +2) 

### GET  / HTTP/1.1

GET-tyypin http-pyyntö sivun juurisivulle (`/`); http-versio (`1.1`)

### 304 

vastauskoodi pyyntöön (304 = sisällössä ei muutosta viimeisimpään pyyntöön)

### 247

vastauksen koko tavuina (B)

### -

viittauslähde, joka on tyhjä (arvona voisi olla esimerkiksi https://google.com, jos pyynnön tekijä siirtyi sivustolle toisen sivuston linkkiä käyttämällä)

### Mozilla/5.0 (X11; Linux x86_64; rv:128.0) Gecko/20100101 Firefox/128.0

käyttäjäagentti: kertoo pyynnön olevan tehty Linux OS:llä ja käyttäen Firefox-selainta


Aikaa kulunut: 1:40
 

## Lähdeluettelo

- Apache HTTP Server Project, Name based virtual host support: Name-based Virtual Host Support - Apache HTTP Server Version 2.4
-	Karvinen 2018: Name Based Virtual Hosts on Apache – Multiple Websites to Single IP Address
