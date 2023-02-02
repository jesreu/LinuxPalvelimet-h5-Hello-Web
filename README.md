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

kuve

Vaihetoehtoisesti sivun testaukseen voit käyttää komentoa `curl 'http://localhost/'`.

Nyt voimme päivittää esimerkkisivun se onnistuu komennolla:

    echo "Tämä lukee sivulla" | sudo tee /var/www/html/index.html

Nyt voimme testata onnistuiko muutos edellä näytetyllä curl komennolla. 

kuve

Toisaalta nyt jos avaamme sivun selaimessa huomaamme, että ääkkoset eivät toimi:

kuve

Olettaisin ongelman johtuvan siitä, että index.html tiedostoon ei ole määritelty oikeaa merkistöä, jotta se tukisi ääkkosiä. 

## b) 10:20
Käyttäjän kotisivut apache2 palvelimella.

    sudo a2enmod userdir
    sudo systemctl restart apache2
    
Suorittamalla komennot asetat käyttäjän kotisivut mahdolliseksi ja voimme testata onnistuiko komennot curl komennolla. Localhostin jälkeen oleva 

    curl "http://localhost/~jesser/"
    
Kuve
    
Komento antaa 403 virheviestin, koska emme ole määritelleet kotisivua. Sivun määrittelemiseksi ajamme komennot:

    cd
    mkdir public_html
    cd public_html/
    micro index.html
    curl "http://localhost/~jesser/"

Voimme ihailla kotisivua nyt nettiselaimessa. 

kuve

## c) 10.50
Uudelle käyttäjälle kotisivut. Luomme uuden testi käyttäjän kommennoilla:

    sudo adduser testi1
    
Aseta vahva salasana, ja lisää terminaalin kysymät tiedot käyttäjälle. Kun terminaalin promptit on käyty loppuun, voit kirjautua ulos nykyiseltä käyttäjältäsi, ja vaihtaa uuteen testi käyttäjään. Nyt voimme ajaa kohdasta b) komennot:

    cd
    mkdir public_html
    cd public_html/
    micro index.html
    curl "http://localhost/~testi1/"

kuve

Nyt olemme onnistuneesti luoneet uudellä käyttäjälle omat nettisivut. Voimme poistaa nyt turhan käyttäjän komennolla `deluser testi1` ajamalla sen normaalilla käyttäjällämme. Valittevasti komento ei mene välttämättä läpi jos käyttäjällä on aktiivisia prosesseja, voit lopettaa käyttäjän kaikki prosessit komennolla `sudo pkill -u testi1`.
## d)


## Lähteet

https://terokarvinen.com/2023/linux-palvelimet-2023-alkukevat/
https://www.indiehackers.com/podcast/196-david-perell
https://www.sitepoint.com/a-minimal-html-document-html5-edition/
https://askubuntu.com/questions/393321/unable-to-delete-user


