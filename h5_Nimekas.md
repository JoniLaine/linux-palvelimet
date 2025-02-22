# h5 Nimekäs

## 	a) Julkinen nimi osoittamaan omaan koneeseen

Käytin oman domain-nimen hankintaan NameCheap-palvelua. Valitsin vapaan nimen ikonlainen.com ja lisäsin NameCheapin portaalissa kaksi A-tietuetta (`@`, eli juuri, sekä `www`, joka osoitti samaan IP-osoitteeseen kuin `@`-tietue). Käytetty IP-osoite, oli aiemmassa h4-tehtävässä toteuttamani IP varaamallani palvelimella.

Domainin DNS-tietueet näiden lisäysten jälkeen:

![Add file: Upload](h5_Kuva1.png)

Vahvistin antamani yhteystiedot uudella domainilla NameCheapissa vaatimuksen mukaisesti. Tähän vaiheeseen pääsi helposti seuraamalla NameCheap-portaalin antamaa ilmoitusta seuraamalla.

A-tietueiden lisäämisen jälkeen oli juuri luomani domain ohjattu näyttämään aiemmin virtuaalikoneella luomani index.html ja ohjaus toimi sekä [ikolainen.com](http://ikolainen.com) että www.ikolainen.com osoitteilla:

![Add file: Upload](h5_Kuva2.png)

## b) Name Based Virtual Host näkyville uudessa nimessä

Kirjauduin virtuaalipalvelimelleni ja loin uuden käyttäjän sivujen muokkausta varten:

![Add file: Upload](h5_Kuva60.png)

Loin uuden hakemiston ikolainen.com ja sisäsin omistajaoikeudet uudelle käyttäjälle `muokkaaja`.

![Add file: Upload](h5_Kuva61.png)

Lopuksi annoin vielä tarvittavat oikeudet käyttäjälle `muokkaaja` ja tarkistin näiden olevan nyt oiekin sivuston muokkaamista varten:

![Add file: Upload](h5_Kuva62.png)

Seuraavaksi loin nano-editorilla ikolainen.com.conf -tiedoston (käytin nanoa, koska micro-editor ei tukenut `copy-paste`-toimintoa hostin ja guestin välillä, ja konfigurointitiedosto oli valmiina kirjoitettuna host-koneellani):

![Add file: Upload](h5_Kuva64.png)

Liitin host-koneella olevan sisällön guest-koneelle tiedostoon:

```
<VirtualHost *:80>
  ServerName ikolainen.com
  ServerAlias www.ikolainen.com
  DocumentRoot /var/www/ikolainen.com
  <Directory /var/www/ikolainen.com>
    Require all granted
  </Directory>
</VirtualHost>
```

![Add file: Upload](h5_Kuva63.png)

Aktivoin sivun ja käynnistin uudestaan Apachen:

`$ a2ensite ikolainen.com.conf`

`$ sudo systemctl restart apache2`

Ja tarkistin selaimessa sivun tilanteen:

![Add file: Upload](h5_Kuva65.png)

Päätin seuraavaksi luoda ikolainen.com sivustolle index.html -tiedoston.

`$ cd /var/www/`

`$ ls`

`$ cd ikolainen.com`

`$ ls`

`$ micro index.html`

![Add file: Upload](h5_Kuva66.png)

Lisäsin HTML-sisältöä tiedostoon:

![Add file: Upload](h5_Kuva67.png)

```
<!DOCTYPE html>
<html lang="fi">
<head>
    <meta charset="UTF-8">
    <title>Ikolainen-sivusto</title>
</head>
<body>
    <header>
        <h1>Tervetuloa etusivulle!</h1>
    </header>
    <body>
        <p>Tänne tulee sisältöä.</p>
    </body>
    <footer>
        <p>Tämä on Linux-palvelimet kurssille tehty sivusto.</p>
    </footer>
</body>
</html>
```

Tarkistin jälleen selaimessa sivuston päivitettyäni selaimen `shift` ja päivitä valinnoilla:

![Add file: Upload](h5_Kuva68.png)

## c) Alasivujen luonti ja muokkaus näkyville nimellä

Kopioin index.html sivun kahdeksi erilliseksi html-sivuksi (testaus ja projektit):

`$ cp index.html testaus.html`

`$ cp index.html projektit.html`

![Add file: Upload](h5_Kuva69.png)

![Add file: Upload](h5_Kuva70.png)

Muokkasin testaus.html ja projektit.html tiedostoja siten, että sivut olivat tunnistettavissa helpommin toisistaan. Muokkasin siis kummankin tiedoston otsikkoa sekä `nav`-osiota kertomaan selvästi, mikä sivu oli kyseessä.

Tarkistin, että linkkiviittaukset sivustojen välillä toimivat selaimessa:

![Add file: Upload](h5_Kuva71.png)

![Add file: Upload](h5_Kuva72.png)

![Add file: Upload](h5_Kuva73.png)

## d) Alidomainien luonti omalle nimelle

Menin takaisin NameCheapin-portaaliin ja lisäsin kaksi vapaavalintaista alidomainia (joni.ikolainen.com ja test.ikolainen.com), joille asetun saman TTL:n kuin juurisivulle ja www-tietueelle (5min). Päätin tehdä testaus.ikolainen.com sivusta A-tietueen ja projektit.ikolainen.com sivusta CNAME-tietueen:

![Add file: Upload](h5_Kuva48.png)

## e) Tutki jonkin nimen DNS-tietoja 'host' ja 'dig' -komennoilla. Käytä kumpaakin komentoa kaikkiin nimiin ja vertaa tuloksia. Katso man-sivulta, miten komennot toimivat - esimerkiksi miten 'dig' näyttää kaikki kentät. Analysoi tulokset, keskity nimipalvelimelta tulleisiin kenttiin (dig näyttää paljon muutakin tietoa). Etsi tarvittaessa uusia lähteitä haastaviin kohtiin. Sähköpostin todentamiseen liittyvät SPF ja DMARC -tietojen yksityiskohdat on jätetty vapaaehtoiseksi lisätehtäväksi. Tutkittavat nimet:

o	Oma domain-nimesi. Vertaa tuloksia nimen vuokraajan (namecheap.com, name.com...) weppiliittymässä näkyviin asetuksiin.

![Add file: Upload](h5_Kuva8.png)

o	Jonkin pikkuyrityksen, kerhon tai yksittäisen henkilön weppisivut. (Ei kuitenkaan kurssikaverin tällä viikolla vuokrattua nimeä).

![Add file: Upload](h5_Kuva10.png)

o	Jonkin suuren ja kaikkien tunteman palvelun tiedot.

![Add file: Upload](h5_Kuva9.png)

##  f) Vapaaehtoinen bonus: 

Aakkossalaattia sähköpostiin. Etsi palvelu, jonka DNS-tiedoissa on SPF ja DMARC.
Selitä näiden kenttien osat ja vaikutukset yksityiskohtaisesti. Voit halutessasi käyttää tulkinnan apuna jotain ohjelmaa tai palvelua, kunhan selität ja tulkitset lopputuloksen myös itse.

### SPF-haku:

![Add file: Upload](h5_Kuva5.png)

SPF-tietue:

`v=spf1 include:spf.protection.outlook.com include:mail.zendesk.com include:mailoutspf.cygrids.net -all`

![Add file: Upload](h5_Kuva6.png)

SPF-tietueen, eli Sender Policy Framen, tehtäv on määrittää palvelimet, jotka saavat käyttää domainia sähköpsotien lähettämiseen. 

**v=spf1**

SPF-tietueen versio.

**include:**

Tämän jälkeen aloitetaan luettelo sallituista palvelimista.

**spf.protection.outlook.com**

Sallii Outlookin.

**include:mail.zendesk.com**

Sallii Zendeskin.

**include:mailoutspf.cygrids.net**

Sallii Cygridsin.

**-all**

Päättää sallittujen palvelinten listan. Mikäli tämän jälkeen kirjoittaa uusia sallittuja palvelimia, eivät nämä saa lähetyslupaa.

### DMARC-haku:

![Add file: Upload](h5_Kuva3.png)

DMARC-tietue:

`v=DMARC1; p=none;`

![Add file: Upload](h5_Kuva4.png)

Tietue on kokonaisuudessaan tarkoitettu sähköpostin verkkotunnuksen suojaamiseen väärennöksiltä ja varmistamaan sähköpostin tunnistus oikeaksi lähettäjäksi vastaanottavan palvelimen puolella.

**v=DMARC1**

DMARC1 on DMARC-protokollan versio.

**p=none**

Määrittää, mitä epäonnistuneille viesteille tehdään. Tässä tapauksessa `none` kertoo, että ainoastaan raportit viesteistä kerätään, mutta muita erityisiä toimia ei suoriteta.



## Lähdeluettelo

- Tero Karvinen, Linux Palvelimet 2025: https://terokarvinen.com/linux-palvelimet/

- MXtoolbox (supertool): https://mxtoolbox.com/

- TNNet, Niko Niinijärvi 2024, DNS-hallinta - Mitä se on?: https://tnnet.fi/blogi/dns-hallinta-mita-se-on/

- CloudFlare, What are DMARC, DKIM, and SPF?: https://www.cloudflare.com/en-gb/learning/email-security/dmarc-dkim-spf/

- Host komento: https://linux.die.net/man/1/host

- Dig komento: https://linux.die.net/man/1/dig




## Tekijä

### Joni Laine

### Haaga-Helia, IT-Tradenomiopiskelija

Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. (http://www.gnu.org/licenses/gpl.html)
