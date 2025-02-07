# h4 Maailma tulee

Aikaa kulunut: 0:00

##	x) Lue ja tiivistä. Tiivistelmäksi riittää muutama ranskalainen viiva per artikkeli. 

Aikaa kulunut: 0:00

##	a) Oman virtuaalipalvelimen vuokraus

Valitsin näkymästä ensimmäisenä Start Free Trial ja annoin sinne pyydetyt omat tiedot. Tämän jälkeen UpCloud lähetti vahvistuskoodin sähköpostiini ja kävin vahvistamassa tämän ja loin tunnuksen.
Kirjauduin palveluun juuri luomillani tunnuksilla.

 ![Add file: Upload](h4_Kuva1.png)

Valitsin verify account ja täytin tarvittavat tiedot luottokortin (tai debit-kortin) rekisteröintiä varten ja vahvistin tiedot.

 ![Add file: Upload](h4_Kuva2.png)
 
Valitsin Deploy now ja Server.

 ![Add file: Upload](h4_Kuva3.png)

Serverin sijainniksi valitsin FI-HEL1 (Suomesta).

 ![Add file: Upload](h4_Kuva4.png)

Plan valinnassa otin valinnan:
1CPU core, 1GB memory, 10GB Storage, 3€ Price/month
Käyttöjärjestelmäksi valitsin Debian GNU/Linux 12 (Bookworm)

 ![Add file: Upload](h4_Kuva5.png)

Mainitsematta jätetyille valinnoille en tehnyt muutoksia, koska näille ei ollut tarvetta.
Siirryin SSH-avaimen luomiseen ja virtuaalikoneelle.

Siirryin public-sites -kansioon ja syötin komennot:

`$  sudo apt-get install openssh-client`

`Enter`

`$ ssh-keygen`

`Enter`

Terminaali pyytä luomaan salasanan, mutta tämän ohitin jättämällä ne tyhjiksi Enterillä.
Tämän jälkeen avain ja avaimen randomart-kuva generoitiin automaattisesti.

 ![Add file: Upload](h4_Kuva7.png)
 
Valitsin Login Method kohdasta SSH keys:

 ![Add file: Upload](h4_Kuva8.png)
 
Palasin virtuaali koneella juureen ja siirryin ssh-kansion sisältöön komennoilla:

`$ cd /home/joni/`

`$ cd .ssh`

`$ls`

 ![Add file: Upload](h4_Kuva9.png)
 
Käytin komentoa:

`$ Cat id_rsa.pub`

Ja kopioin saadun julkisen avaimen.

 ![Add file: Upload](h4_Kuva10.png)

Palasin UpCloudin puolelle ja liitin julkisen avaimen Add an SSH key näkymään:

 ![Add file: Upload](h4_Kuva11.png)
 
Ja valitsin Save he SSH key.
Klikkasin Deploy ja odotin, että serveri valmistuu.

 ![Add file: Upload](h4_Kuva12.png)

Odottaessa siirryin jo valmiiksi virtuaalikoneella oikeaan sijaintiin ja varmistin sijaintini komennoilla:

`$ cd`

`$ pwd`

`$  ls`

 ![Add file: Upload](h4_Kuva13.png)

Serverin valmistuttua (vei noin 3 minuuttia) klikkasin kuvan mukaista See how to connect linkkiä:

 ![Add file: Upload](h4_Kuva15.png)

Ja seurasin ohjeita linkin takana valitsemalla ohjeeksi virtuaalikoneeni käyttöjärjestelmälle sopivan ohjeen (from linux):

 ![Add file: Upload](h4_Kuva16.png)

Eteeni tuli varmistus, haluanko varmasti yhdistää ja jatkaa. Tarkistin IP-osoitteen ja kirjoitin komentoriville `yes` ja painoin `Enter`

 ![Add file: Upload](h4_Kuva17.png)
 
Ja lopuksi valitsin `Y` ja `Enter`

Lisäsin käyttäjän vielä sudo-ryhmään:

`$ sudo adduser joni sudo`

`Enter`

Ja kirjauduin pois root-käyttäjältä:

`$exit`

Aikaa kulunut: 0:00



