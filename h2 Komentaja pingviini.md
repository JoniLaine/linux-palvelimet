# h2 Komentaja pingviini

Työn aloitus: 0:00

## Command line basics revisited 
-	Minimum privilige käytännön lähtökohta on antaa niin vähän käyttöoikeuksia käyttäjille kuin se käytön kannalta on mahdollista.
-	Koko järjestelmään vaikuttavat komennot vaativat järjestelmänvalvojan käyttöoikeudet, eli ”sudo”-komennon. Näihin kuuluvat mm. käyttäjien luominen, käyttöoikeuksien muuttaminen ja ohjelmien asennus tai poisto.
-	Käytä tabulatuuria tiedostojen nimien valmiiksi kirjoittamiseen kirjoitusvirheiden välttämiseksi.
-	Käytä nuolinäppäimiä syöttääkseni aiempia komentoja, jottei niitä tarvitse kirjoittaa uudestaan.

Aikaa kulunut 0:45



## f) Raudan selitys ja analysointi

Tiesin, että koneella ei ollut valmiina asennettua tarvittavaa ohjelmaa, joten asensin sen komennolla:

`$ sudo apt install lshw`

Terminaali pyysi salasanaa ja syötin sen ja painoin Enter.
Ohjelma asentui ja tämän jälkeen annoin komennon:

`$ sudo lshw -short -sanitize`



## Lähdeluettelo


-	Tero Karvinen, Command Line Basics Revisited: (https://terokarvinen.com/2020/command-line-basics-revisited/?fromSearch=command%20line%20basics%20revisited)
