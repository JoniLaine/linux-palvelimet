# h3 Hello Web Server

Aikaa kulunut: 0:00

## Weppipalvelin localhost-osoitteessa ja Apache

Apache-weppipalvelin oli valmiina asennettuna koneelle.
Testasin weppipalvelimen vastaamisen terminaalissa komennolla:

´$systemctl restart apache2´

Komento promptasi salasanan syöttöruudun, johon annoin salasanan ja painoin `Enter`.

Kokeilin sivun vastaamisen Firefox-selaimella osoitteella http://localhost sekä https://127.0.0.1



## Loki weppipalvelimella olevan sivun lataamisesta:


`$ cd /`

`$ sudo tail -3 var/log/apache2/error.log`



`$sudo tail -3 var/log/apache2/access.log`

ei antanut ollenkaan tuloksia. tarkistin siis vaihtoehdot:

`$ sudo ls var/log/apache2`


 ja kokeilin lokia other_vhosts_access.log (koska access.log.1 on vanhemmat lokit/historia)

`$ sudo tail -3 var/log/apache2/other_vhosts_access.log`

## Nimipohjainen- vs. IP-pohjainen virtuaali isäntä (host)

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


## Lähdeluettelo

- Apache HTTP Server Project, Name based virtual host support: Name-based Virtual Host Support - Apache HTTP Server Version 2.4
