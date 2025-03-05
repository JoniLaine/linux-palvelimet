# h7 Maalisuora

Aikaa kulunut: 0:00

## a) Kirjoita ja aja "Hei maailma" kolmella kielellä.

Aloitin valitsemalla ohjelmointikieliksi Javan, Pythonin ja C:n.

Asensin ensimmäisenä virtuaalikoneen käyttäjälle Java Development Kit (JDK) -paketin komennolla:

`$ sudo apt-get install openjdk-17-jdk`

Asennuksessa kysytään vahvistusta, johon vastasin `y` ja `Enter`.

Asennus vei jonkin aikaa. Omalla koneellani noin 30 sekuntia.

![Add file: Upload](h7_Kuva1.png)

Loin Hello.java tiedoston micro-editorilla komennolla:

`$ micro Hello.java`

![Add file: Upload](h7_Kuva3.png)

Kirjoitin tiedoston sisälle lyhyen Hei maailma -javaskriptin. Huomioitavaa on, että luokan (class) nimi tulee olla sama kuin tiedoston nimi:

```
class Hello {
  public static void main(String[] args){
    System.out.println("Hei maailma");
  }
}
```

![Add file: Upload](h7_Kuva2.png)

Tallensin skriptitiedoston ja suljin tämän.
Muutin Hello.java luettavaan muotoon java-tulkille komennolla:

`$ javac Hello.java`

Ja tarkistin tässä kohtaa käyttöoikeudet:

`$ ls -l`

![Add file: Upload](h7_Kuva4.png)

![Add file: Upload](h7_Kuva5.png)

Nämä näyttivät olevan kunnossa, jotta voisin suorittaa juuri tehdyn Hello.java skriptin. Annoin komennon kokeillakseni tätä:

![Add file: Upload](h7_Kuva6.png)

Tämä toimi hienosti, joten siirryin Pythonin pariin.

Aikaa kulunut: 0:20

Lähdin asentamaan Pythonin-tulkkia, mutta muistin komennon annon jälkeen tehneeni tämän jo luennon aikana edeltävänä päivänä tauon aikana:

`$ sudo apt-get install python3`

![Add file: Upload](h7_Kuva7.png)

Loin Python-kielellä lyhyen Hello.python -skriptin komennolla:

`$ micro Helllo.python`

![Add file: Upload](h7_Kuva8.png)

Ja sisällöksi koodin:

```
print("Hei maailma")
```

![Add file: Upload](h7_Kuva9.png)
  
## b) Lähdeviitteet. Tarkista ja tarvittaessa lisää lähdeviitteet kaikkiin raportteihisi h1 alkaen.
Tarkista, että olet viitannut lähteisiin: tehtäväsivuun, kurssiin, muiden opiskelijoiden raportteihin, man-sivuihin, kotisivuihin ja ylipäänsä kaikkiin käyttämiisi lähteisiin. 
  Lähdeviite tulee olla jokaisessa raportissa tai sivussa, jossa lähdettä on käytetty. Kaikki tehtävät perustuvat tämän sivun tehtävänantoihin, joten ainakin tämä viite on syytä löytyä. (Tästä alakohdasta ei tarvitse kirjoittaa vaiheittaista raporttia)


## c) Laita Linuxiin uusi, itse tekemäsi komento niin, että kaikki käyttäjät voivat ajaa sitä.

## d) Ratkaise vanha arvioitava laboratorioharjoitus soveltuvin osin.

## e) Asenna itsellesi tyhjä virtuaalikone arvioitavaa labraa varten. Suosittelen Debian 12-Bookworm amd64, riittävästi RAM ja kovalevyä. Koneella saa olla päivitetyt ohjelmistot (apt-get dist-upgrade), tulimuuri (esim. ufw). 
Koneella ei saa olla mitään muita demoneja tai ohjelmia asennettuna kuin nuo ja asennuksen mukana tulevat. Virtuaalikoneella ei saa olla luottamuksellisia tiedostoja, koska opettaja saattaa tarkastella sitä. 
(Tästä d-osioista ei tarvitse kirjoittaa raporttia. 
  Tavalliseen käyttöjärjestelmän asennuksen yhteydessä tulevat ohjelmat saavat olla mukana, esim. graafinen työpöytä tulee yleensä asennuksen mukana.)


## Lähdeluettelo

- Tero Karvinen, Linux Palvelimet 2025: https://terokarvinen.com/linux-palvelimet/


## Tekijä

### Joni Laine

### Haaga-Helia, IT-Tradenomiopiskelija

Tätä dokumenttia saa kopioida ja muokata GNU General Public License (versio 2 tai uudempi) mukaisesti. (http://www.gnu.org/licenses/gpl.html)
