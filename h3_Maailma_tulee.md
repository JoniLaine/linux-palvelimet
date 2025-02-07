# h4 Maailma tulee

##	x) Lue ja tiivistä. Tiivistelmäksi riittää muutama ranskalainen viiva per artikkeli. 

##	a) Oman virtuaalipalvelimen vuokraus

Valitsin näkymästä ensimmäisenä Start Free Trial ja annoin sinne pyydetyt omat tiedot. Tämän jälkeen UpCloud lähetti vahvistuskoodin sähköpostiini ja kävin vahvistamassa tämän ja loin tunnuksen.
Kirjauduin palveluun juuri luomillani tunnuksilla.

Kuva1

Valitsin verify account ja täytin tarvittavat tiedot luottokortin (tai debit-kortin) rekisteröintiä varten ja vahvistin tiedot.
Kuva2
Valitsin Deploy now ja Server.
Kuva3

Serverin sijainniksi valitsin FI-HEL1 (Suomesta).

Kuva4

Plan valinnassa otin valinnan:
1CPU core, 1GB memory, 10GB Storage, 3€ Price/month
Käyttöjärjestelmäksi valitsin Debian GNU/Linux 12 (Bookworm)

Kuva5


Mainitsematta jätetyille valinnoille en tehnyt muutoksia, koska näille ei ollut tarvetta.
Siirryin SSH-avaimen luomiseen ja virtuaalikoneelle.

Siirryin public-sites -kansioon ja syötin komennot:

`$  sudo apt-get install openssh-client`
`Enter`
`$ ssh-keygen`
`Enter`

Terminaali pyytä luomaan salasanan, mutta tämän ohitin jättämällä ne tyhjiksi Enterillä.
Tämän jälkeen avain ja avaimen randomart-kuva generoitiin automaattisesti.

Kuva7 
Valitsin Login Method kohdasta SSH keys:

Kuva8
Palasin virtuaali koneella juureen ja siirryin ssh-kansion sisältöön komennoilla:
`$ cd /home/joni/`
`$ cd .ssh`
`$ls`

Kuva9
Käytin komentoa:

`$ Cat id_rsa.pub`

Ja kopioin saadun julkisen avaimen.

Kuva10

Palasin UpCloudin puolelle ja liitin julkisen avaimen Add an SSH key näkymään:

Kuva11
Ja valitsin Save he SSH key.
Klikkasin Deploy ja odotin, että serveri valmistuu.

Kuva 13

Odottaessa siirryin jo valmiiksi virtuaalikoneella oikeaan sijaintiin ja varmistin sijaintini komennoilla:

`$ cd`
`$ pwd`
`$  ls`

Kuva 14

Serverin valmistuttua (vei noin 3minuuttia) klikkasin kuvan mukaista See how to connect linkkiä:
Kuva15
Ja seurasin ohjeita linkin takana valitsemalla ohjeeksi virtuaalikoneeni käyttöjärjestelmälle sopivan ohjeen (from linux):

Kuva16

Eteeni tuli varmistus, haluanko varmasti yhdistää ja jatkaa. Tarkistin IP-osoitteen ja kirjoitin komentoriville `yes` ja painoin `Enter`

Kuva17
Ja lpuksi valitsin Y ja `Enter`

Lisäsin käyttäjän vielä sudo-ryhmään:

`$ sudo adduser joni sudo`
`Enter`

Ja kirjauduin pois root-käyttäjältä:

`$exit`


