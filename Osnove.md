# Osnove Pythona

U ovom poglavlju objasniti ćemo osnovnu sintaksu Python programskog jezika.

## Sintaksa

Pythonova sintaksa istovremeno je razlog zbog ćega ga ljudi koji ga vole, vole, a ljudi koji ga mrze, mrze.

Za većinu ljudi koji su tokom svog obrazovanja navikli pisati programske jezike čija je sintaksa inspirirana C programskim jezikom, Python će izgledati kao programski jezik iz najdubljih krugova pakla.

To je zbog toga što je primarni fokus kod Pythona deskriptivnost, čitljivost i pristupačnost bezjacima (neprogramerima). Ako se prisječate iz prethodnog poglavlja, Guido van Rossum osmislio je ovaj programski jezik sa svrhom da se primjenjuje kao alat pri sistem administraciji na Amoeba operacijskom sustavi. Baš zbog toga se i danas jako često primjenjuje za server side scripting.

Najprimjetnije dvije razlike u sintaksi su pri definiraju blokova koda i manjak točkastozareznosti.

Dok u većini drugih jezika blok koda označavamo korištenjem vitičastih zagrada:

``` C
if(1 == 0) {
    uradiNesto();
}
```

U Pythonu koristimo najvećeg neprijatelja prosječnog programera sa fesba, pravilnu indentaciju:


``` Python
if 1 == 0:
    uradiNesto()

```

Početak bloka koda označavamo dvotočkom a sam kod postavljamo u taj blok indentirajući ga pomoću spaceova ili tabova.

Početnici često nailaze na problem kada žele blok koda ostaviti praznim.

``` Python
if 1 == 0:

uradiNesto()

```

Ako pokrenemo ovaj kod, on će rezultirati errorom: `IndentationError: expected an indented block.`

Zbog toga je u python dodan izraz `pass`, koji ne radi apsolutno ništa, kako bi mogli imati prazne blokove koda.

```Python
if 1 == 0:
    pass
uradiNesto()
```

Sada se postavlja pitanje, koristimo li tabove ili spaceove za indentaciju. Vi odlučite, ali što god odlučite, nemojte koristit i tabove i spaceove (primarno jer vam se program neće pokrenuti, a i zbog toga što bi mogli završiti pod giljotinom), ali na kraju dana što god odlućite da je bolje i urednije, koristite spaceove, jer Guido Van Rossum tako kaže, a Guido Van Rossum je vjerojatno mnogo pametniji od vas.

[The Silicon Valley: Spaces vs Tabs](https://youtu.be/SsoOG6ZeyUI)


Također, Pythonu ništa u životu ne znači znak ASCII koda 59 tako da tipku za ; možete slobodno istrgnuti sa vaše tipkovnice.


## Komentari

Ionako ih vjerojatno nećete koristiti, ali za početak komentara koristi se oznaka ljestve (ilitiga hešteg) #

``` Python
# Ovo je komentar
```

## Varijable

Varijabla je memorijski prostor unutar kojeg spremamo neke podatke.

> Nemamo normalnih tipova u Pythonu. Nego sve neki tamo čudni,
> Adriano Dijan

## Grananja

Grananja u Pythonu započinjemo ključnom riječi `if`, nakon toga 
