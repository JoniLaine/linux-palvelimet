# h6 Salataampa

Tässä osiossa luodaan SSL-salaus (hhtps) weppisivustolle.

Aikaa kulunut: 0:00

## x) Lue ja tiivistä. Tiivistelmäksi riittää muutama ranskalainen viiva per artikkeli. (Tässä alakohdassa ei tarvitse tehdä testejä tietokoneella)

## a) Let's. Hanki ja asenna palvelimellesi ilmainen TLS-sertifikaatti Let's Encryptilta. Osoita, että se toimii.

Asennetaan Lego ja sille kansio.

![Add file: Upload](h6_Kuva100.png)

Testiympäristö SSL-sertifikaatille.

![Add file: Upload](h6_Kuva101.png)

Toimii. Nyt voin kokeilla poistaa tämän testiversion:

![Add file: Upload](h6_Kuva102.png)

Ja latasin oikean SSL-sertifikaatin.

![Add file: Upload](h6_Kuva103.png)

![Add file: Upload](h6_Kuva104.png)

![Add file: Upload](h6_Kuva105.png)

lego --accept-tos --email="joni.tk.laine@gmail.com" --domains="ikolainen.com" --domains="www.ikolainen.fi" --http --http.webroot="/home/joni/public_sites/ikolainen.com/" --path="/home/joni/lego/" --pem run

![Add file: Upload](h6_Kuva106.png)

![Add file: Upload](h6_Kuva107.png)

![Add file: Upload](h6_Kuva108.png)

![Add file: Upload](h6_Kuva109.png)

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

