# LinuxPalvelimet-h5-Hello-Web
    Kirjoittanut: Jesse Reunamo
    Kurssi:       Linux-palvelimet
    Linkki:       https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/

## x) Klo: 9:20
Kuuntelin Indie Hackers podcastin episodin: Turning a Weak Skill into Your Best Asset with David Perell of Write of Passage.
Tiivistelmää:
- David Perell kertoo ideoiden jakamisen internetissä olevan heikosti hyödynnettyä.
- Kirjoittamalla omista ideoista voit kasvattaa omaa yleisöäsi, jonka avulla voit tehdä rahaa. 
- Perell selittää, että nykypäivänä hyvällä kirjoittamisella on erittäin suuri kysyntä, koska oman tekstin julkaiseminen on helppoa.
- Käyttämällä julkisia sivustoja voit ohjata yleisösi omille sivuillesi ja näin välttää välikäsiä omassa toiminnassasi.
- Hyödynnä omaa työtäsi ja käytä työsi tulosta useassa eri paikassa. 

## a) Klo 9:55
Apachen esimerkkisivun muuttaminen. Apache palvelimen asentaminen onnistuu komennoilla:

    sudo apt-get update
    sudo apt-get -y install apache2
    sudo systemctl start apache2
    
Komennot suoritettuasi palvelimen tulisi olla asennettuna ja toiminnassa. Voit kokeilla toimiiko palvelin menemällä selaimeen ja kirjoittamalla http://localhost/ osoitteeksi.

![default2](https://user-images.githubusercontent.com/112503770/216285860-ef62385e-fb1b-4a1b-a55e-55d2af640aa3.png)


Vaihetoehtoisesti sivun testaukseen voit käyttää komentoa `curl 'http://localhost/'`.

Nyt voimme päivittää esimerkkisivun se onnistuu komennolla:

    echo "Tämä lukee sivulla" | sudo tee /var/www/html/index.html

Nyt voimme testata onnistuiko muutos edellä näytetyllä curl komennolla. 

![defupdate](https://user-images.githubusercontent.com/112503770/216287066-2a8343ab-70da-49f1-b6d7-cb0cd84a2cd9.png)

Toisaalta nyt jos avaamme sivun selaimessa huomaamme, että ääkkoset eivät toimi:

![aakkosten_toimimattomuus](https://user-images.githubusercontent.com/112503770/216287099-34b404ad-5123-4abf-9577-2afdb6a1fbf2.png)

Olettaisin ongelman johtuvan siitä, että index.html tiedostoon ei ole määritelty oikeaa merkistöä, jotta se tukisi ääkkosiä. 

## b) 10:20
Käyttäjän kotisivut apache2 palvelimella.

    sudo a2enmod userdir
    sudo systemctl restart apache2
    
Suorittamalla komennot asetat käyttäjän kotisivut mahdolliseksi ja voimme testata onnistuiko komennot curl komennolla. Localhostin jälkeen tulee ~käyttäjänimi, joka määrittää kotisivun nimen.

    curl "http://localhost/~jesser/"
    
![403curl](https://user-images.githubusercontent.com/112503770/216286498-63661b9c-4d03-4870-a5be-b0b9e4860d87.png)

    
Komento antaa 403 virheviestin, koska emme ole määritelleet kotisivua. Sivun määrittelemiseksi ajamme komennot:

    cd
    mkdir public_html
    cd public_html/
    micro index.html
    curl "http://localhost/~jesser/"

Voimme ihailla kotisivua nyt nettiselaimessa. 

![kotisivut1](https://user-images.githubusercontent.com/112503770/216286693-9702b366-bcf0-400f-a235-e5858ca3471f.png)


## c) 10.50
Uudelle käyttäjälle kotisivut. Luomme uuden testikäyttäjän kommennoilla:

    sudo adduser testi1
    
Aseta vahva salasana, ja lisää/ohita terminaalin kysymät tiedot käyttäjälle. Kun terminaalin promptit on käyty loppuun, voit kirjautua ulos nykyiseltä käyttäjältäsi, ja vaihtaa uuteen testi käyttäjään. Nyt voimme ajaa kohdasta b) komennot:

    cd
    mkdir public_html
    cd public_html/
    micro index.html
    curl "http://localhost/~testi1/"

![uuden_kyttjn_kotisivut](https://user-images.githubusercontent.com/112503770/216286058-d7aaa1db-5b3e-4c1c-a5df-c9e4a787cfb5.png)


Nyt olemme onnistuneesti luoneet uudellä käyttäjälle omat nettisivut. Voimme poistaa nyt turhan käyttäjän komennolla `deluser testi1` ajamalla sen normaalilla käyttäjällämme. Valittevasti komento ei mene läpi, jos käyttäjällä on aktiivisia prosesseja. Lopettaaksesi käyttäjän kaikki prosessit aja komento `sudo pkill -u testi1`.
## d) 11:15
Päivitämme käyttäjän kotisivut validiksi html5 sivuksi.

    cd
    cd public_html
    micro index.html

Kun editori on auki, kannattaa etsiä jokin html template. Käytin sitepointin minimal html documenttia pohjana. Kuvassa näkyy html dokumentti.

![validi_html5](https://user-images.githubusercontent.com/112503770/216286275-fb782d84-b966-4b6c-a276-32f3a3903d31.png)

Mikäli avaat sivun selaimessa huomaat, että validissa html5 dokumentissa ääkköset toimivat, toisin kuten kohdassa a) puhtaassa tekstitiedostossa.
Voimme vielä tarkistaa onko dokumentti validi syöttämällä se w3schools html validator sivulle. Voit kopioida html sivun tekstin suoraan microsta ja asettaa sen validate by direct input kohtaan tarkistusta varten.

![Validoituhtml5](https://user-images.githubusercontent.com/112503770/216286860-aad1dbf3-6031-4fb6-a604-16d25c305416.png)

Kaikki OK, eli dokumentti on validi.
Lopetus aika 11:30
## Lähteet

https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/
https://www.indiehackers.com/podcast/196-david-perell
https://www.sitepoint.com/a-minimal-html-document-html5-edition/
https://askubuntu.com/questions/393321/unable-to-delete-user
https://validator.w3.org

