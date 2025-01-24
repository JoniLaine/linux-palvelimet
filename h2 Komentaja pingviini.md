# h2 Komentaja pingviini

Työn aloitus: 0:00

## Command line basics revisited 
-	Minimum privilige käytännön lähtökohta on antaa niin vähän käyttöoikeuksia käyttäjille kuin se käytön kannalta on mahdollista.
-	Koko järjestelmään vaikuttavat komennot vaativat järjestelmänvalvojan käyttöoikeudet, eli ”sudo”-komennon. Näihin kuuluvat mm. käyttäjien luominen, käyttöoikeuksien muuttaminen ja ohjelmien asennus tai poisto.
-	Käytä tabulatuuria tiedostojen nimien valmiiksi kirjoittamiseen kirjoitusvirheiden välttämiseksi.
-	Käytä nuolinäppäimiä syöttääkseni aiempia komentoja, jottei niitä tarvitse kirjoittaa uudestaan.

Aikaa kulunut 0:45

## a)	Asenna micro

Annoin terminaalissa seuraavat komennot:

`$ sudo apt-get update`

(Terminaali pyysi tässä kohtaa salasananaani ja syötin sen, sekä painon `Enter`, jonka jälkeen komento suoritettiin)

`$ sudo apt install micro`
 
 ![Add file: Upload](h2_Kuva1.png)

Kulunut aika: 0:50

## b)	Kolme minulle uutta komentoriviohjelmaa

Päätin kokeilla seuraavien komentoriviohjelmien asennusta ja toimintaa:

`nano`: tekstieditori

`rsync`: tiedostojen synkronointityökalu

`tmux`: mahdollistaa siirtymät usean työkalun välillä samassa terminaalissa

Valintaani vaikuttivat kuvaukset, joita löysin hyödylliseksi koettujen ohjelmien joukosta. Kokemusta minulla ei ollut entuudestaan oikein mistään cmd pohjaisesta ohjelmasta linux-ympäristössä, mutta lähdin liikenteeseen avoimen uteliaasti.

Kaikki asennukset suoritin yhdellä komennolla:

`$ sudo apt install nano rsync tmux`

Kulunut aika: 1:45

### Nano

Annoin terminaaliin komennon:

`$nano`

ollessani yhä omassa kotivalikossani.

Komennolla avautui tyhjä tekstitiedosto, johon voi alkaa kirjoittamaan suoraan ilman muita lisävalintoja:

 ![Add file: Upload](h2_Kuva2.png)

Tiedoston sai tallennettua suoraan painamalla `ctrl + O` (näkymässä alareunassa olevan ohjeen mukaan, koska `^O` tarkoittaa tätä näppäinyhdistelmää).
Tämä siirsi valikon tiedoston nimeämiseen, johon voi kirjoittaa suoraan tiedoston nimen ja vahvistaa tämän painamalla `Enter`.

![Add file: Upload](h2_Kuva3.png)

Tallennus tapahtui painamalla `ctrl + X`.

![Add file: Upload](h2_Kuva4.png)

Tekstitiedosto tallentui siihen hakemistoon, jossa olin nanon avaamisen hetkellä. Asian pystyi varmistamaan komennolla:

`$ ls` 

![Add file: Upload](h2_Kuva5.png)

Tiedostoa pääsi muokkaamaan komennolla:

`$ nano nanolla_kirjoitettu_tekstitiedosto.txt`

![Add file: Upload](h2_Kuva6.png)

Muokkauksen tallennus tapahtui samaan tapaan kuin alkuperäisen tiedoston luonti seuraavilla komenoilla:

`ctrl + o`

`Enter`

`ctrl + X`

Tekstitiedoston sisällön pystyi tarkistamaan tallentuneen muokattuun muotoon komennolla:

`$ nano nanolla_kirjoitettu_tekstitiedosto.txt`

Ja palaamaan takaisin tekemättä uusia muokkauksia valinnalla `ctrl + X`.

Kulunut aika: 1:15

Lähtiessäni kokeilemaan muita valitsemiani ohjelmia selvisi, että tmux ja rsync eivät olleet järkeviä valintoja sen hetken virtuaalikoneen tiedostomäärälle ja ohjelmamäärälle. En poistanut nätä ohjelmia, koska ajattelin niistä olevan amhdollisesti iloa virtuaalikoneen datamäärän kasvaessa.
Valitsin asennettavaksi näiden tilalle seuraavat uuden tutkinnan jälkeen:

`tree`: luo visuaalisen puumaisen rakenteen hakemistosta ja alihakemistoista

`locate`: hakuohjelma, joka osaa etsiä vastaavuudet hakemistoista

Asensin uudet valitsemani ohjelmat tällä kertaa erillisillä komennoilla:

`$ sudo apt install tree`

`$ sudo apt install locate`

Aikaa kulunut 2:15

### Tree

Tree on tarkoitettu helpottamaan hakemistorakenteen hahmottamista muodostamalla puumaisen kaavan hakemistoista (samaan tapaan kuin esimerkiksi resurssienhallinta GUI versiossa).

Kokeilin tree:n toimintaa komennolla:

`$ tree`

 ![Add file: Upload](h2_Kuva7.png)

Tree mahdollisti myös määritellä, miten syvälle tiedostorakenteeseen halusi nähdä komennolla:

`$ tree -L 1` 

[ numeron pystyi korvata haluamallaan määrällä ja se määritti hakemistojen tason, jonne asti puu näytti tulokset]

![Add file: Upload](h2_Kuva8.png) 

Tree oli todella positiivinen löytö ja tulen sitä varmasti hyödyntämään jatkossa. Ohjelma on erityisen hyödyllinen, mikäli kansiorakenteen hahmottamisessa on haasteita tai sitä vasta harjoittelee.

Aikaa kulunut 2:30

### Locate

Asennus onnistui komennolla:

`$ sudo apt install locate`

Kokeilin locaten toimintaa komennolla:

`$ locate kissa.txt`

, mutta tämä ei toiminut tehnyt yhtään mitään. Tästä löysin nopeasti tiedon jo samasta lähteestä, että toimiakseen locate vaati myös komennon:

`$ sudo updatedb`

Tämän jälkeen kokeilin uudestaan hakua, tällä kertaa toisella tiedostolla:

`$ locate koira.txt`

![Add file: Upload](h2_Kuva9.png)
 
Kokeilin toiminnan myös alkuperäisellä kokeilulla:

`$ kissa.txt`

ja ohjelma toimi nyt oikein.

Aikaa kulunut 3:00

## c)	Important directories

Root-hakemisto:

`/`

Kotihakemisto (sisältää kaikkien käyttäjien kotihakemistot:

`/home/`

Tietyn käyttäjän kotihakemisto (tässä tapauksessa joni-nimisen käyttäjän):

`/home/joni/`

Järjestelmäasetukset (koko järjestelmän laajuinen):

`/etc/`

Siirrettävät mediatiedostot:

`/media/`

Järjestelmälokit (koko järjestelmän laajuinen), josta on mahdollista hakea tietyn järjestelmän lokitiedot:

`/var/log/`

## d) Grep-komento

 
## f) Raudan selitys ja analysointi

Tiesin, että koneella ei ollut valmiina asennettua tarvittavaa ohjelmaa, joten asensin sen komennolla:

`$ sudo apt install lshw`

Terminaali pyysi salasanaa ja syötin sen ja painoin Enter.
Ohjelma asentui ja tämän jälkeen annoin komennon:

`$ sudo lshw -short -sanitize`

![Add file: Upload](h2_Kuva10.png)

![Add file: Upload](h2_Kuva11.png)

![Add file: Upload](h2_Kuva12.png)

## Lähdeluettelo


-	Tero Karvinen, Command Line Basics Revisited: [Command line basics revisited](https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited)
