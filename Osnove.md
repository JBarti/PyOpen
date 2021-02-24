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

## Varijable i tipovi podataka

Varijable se koriste za pohranjivanje koje ćemo kasnije koristiti i kojima ćemo manipulirati u toku programa. Podaci koje spremamo u varijable imaju svoj tip. Osnovni tipovi podataka u Pythonu su:
 - **int**, **float**, complex (numerički tipovi)
 - **str** (tekst)
 - **list**, **tuple**, range (*iterabilni* tipovi)
 - **dict** (dict tipovi... jel, kao)
 - **set**, frozenset (skupovni tipovi)
 - **bool** (True/False)
 - bytes, bytearray, memoryview (binarni tipovi)


Prema način tretiranja varijabli i podataka Python klasificiramo kao *dynamically typed* i *strong typed* programski jezik.

Dinamička tipiziranost govori nam da u Pythonu tip podatka vežemo za neku vrijednost, a ne za samu varijablu. Zbog toga u pythonu deklaracija varijable na *"tradicionalan"* način nije potrebna, tj. pri stvaranju varijable nemoramo eksplicitno reči koji će biti njen tip. To nam omogućava i da unutar *runtimea* programa mijenjamo tip podatka koji je vezan za varijablu.

Za razliku od C programskog jezika gdje ovakav kod rezltira kompajlerskom pogreškom.

``` C
int varijabla = 10;
varijabla = "Tekst";
```

U Pythou su takve stvari dozvoljene.

```Python
varijabla = 10
varijabla = "Tekst"
```

Međutim, to što su nam dozvoljene, ne znaći nužno da su dobra praksa. Nije poželjno drastično mijenjati tip varijable unutar rada programa. Možete se voditi pravilom da je to u redu dok god koristite tipove iz jedne familije podataka (npr. pridruživanje inta i floata istoj varijabli).

To primarno nije dobra praksa zbog toga što narušava konzistentnost samog koda (a konzistencija je ključna stvar dobrog programa) već nam može prouzročiti nepredvidive greške u programu, što nas dovodi u drugu familiju programskih jezika u koju Python spada, *strongly typed* jezici. Strongly typed jezici nemaju super dobru definiciju, ali laički rečeno, to znaći da varijable ne mogu *"magično"* promjeniti svoj tip podatka. Vjerojatno će te lakše shvatiti o čemu pričamo na primjeru:

U JavaScript programskom jeziku ovaj izraz je potpuno legalan:

```JavaScript
"2" + 2 
// "22"
```

Dok python to prepoznaje kao grešku.

```Python
"2" + 2
# TypeError: can only concatenate str (not "int") to str
```

Problem se javlja zbog toga što Python će nas upozoriti na ovu grešku samo ako program izvrši ovu liniju koda. Ako nismo konzstentni u tipovima podataka koje pridružujemo varijablama može nam se dogoditi da unutar koda imamo duboko zasijanu ilegalnu operaciju između dva nepodržana tipa podataka, koja će nakon 2 godine u produkciji i 10 000 updateova poslije prouzročiti budućem vama-programeru debugging glavobolju.

Idući kod će interpreter pokrenuti bez problema zbog toga što nikada neće doći do 3. linije koda, ali svejedno ona predstavlja potencijalnu *program breaking* grešku posijanu u kodu koja samo čeka dan kada će ju netko trigerati.

```Python
x = 0
if x == 1:
	x = x + "1"
else:
	x = x + 2
```


### Implementacija tipova

> Nemamo normalnih tipova u Pythonu. Nego sve neki tamo čudni.
>
> -- <cite>Adriano Dijan</cite>


Zanimljivo je pogledati način na koji Python implementira osnovne tipove podataka. Za to prvo moramo pogledati funkciju `type()` koja kao argument prima objekt i vraća klasu od koje je nastao taj objekt. Ako pokušamo toj funkciji proslijediti kao argument varijablu koja u sebi ima pohranjen broj dobijemo idući rezultat.

```Python
x = 10
type(x)
# <class 'int'>
```

Iz ovoga možemo zaključiti da su brojevi (pa tako i svi ostali tipovi podataka), samo objekti neke klase. Ali što bi se dogodilo kada bi samu klasu proslijedili funkciji `type()`


```Python
type(int)
# <class 'type'>
```

Sada dolazimo do jako bitnog zaključka. Sve u Pythonu je objekt i svi objekti su na neki način povezani sa izvornom metaklasom type. Čak je i metaklasa type objekt klase type. To jeziku u pozadini omogućava da sve "različite" tipove podataka tretira kao jedan osnovni tip i zbog toga možemo mijenjati tip podataka koji se nalazi u pojedinoj varijabli tokom rada programa, a vidjet ćemo poslije da možemo i unutar listi spremati više podataka različitih tipova.


### Korištenje osnovnih tipova podataka

#### Numerički podaci

Numerički podaci u Pythonu su zanimljivi zbog toga što je veličina broja kojeg možemo u pisati u varijablu ograničena samo našom radnom memorijom. 

Cjelobrojne vrijenosti možemo zadati i pomoću prefiksa baze brojevnog sustava kojeg koristimo.

```Python
print(0o10)
# 8
print(0x10)
# 16
print(0b10)
# 2
```

#### Stringovi

String je nepromjenjivi niz characterova. Navodi se unutar jednostrukih ili dvostrukih navodnika.

```Python
broj = 123
broj_string = "123"
broj_string_drugi = '123'
```

Osnovne operacije koje su nam definirane nad stringovima su:
 - indeksiranje
 - zbrajanje
 - množenje ???

Iako je indeksiranje dozvoljeno zamjena pojedinog charactera unutar stringa nije.

```Python
string = "Ja sam niz characterova"
string[5] = "B"
# TypeError: 'str' object does not support item assignment
```

Zbrajanje je moguće primjeniti samo između dva stringa i ono nam generira novi string sastavljen od dva zbrojena.

```Python
prvi_string = "Luka"
drugi_string = "Ja san ti ćaća"

popularna_referenca = prvi_string + drugi_string
# ili 
prvi_string += drugi_string
```

Množenje, je nešto neobičniji operator nad stringovima, za njega je bitno da string možemo množiti samo sa brojem što rezultira uzastopnom zbrajanju stringa samim sa sobom. 

```Python
prvi_string = "preko " * 3
print(prvi_string)
# "preko preko preko "
```

Stringovi su nešto složeniji tip podataka od brojeva. Već smo zaključili da su svi podaci samo objekti pojedinih klasa što omogućava definiranja i izvršavanje metoda i preopterećivanje operatora nad samim podacima. Neke od bitnijih metoda koje se mogu primijeniti nad stringovima su:
 - `string.count(substring)` -> vraća broj ponavljanja substringa unutar stringa
 - `string.find(substring)` -> vraća poziciju prve pojave traženog substringa unutar stringa, ako substring nije pronađen vraća vrijednost `-1`
 - `string.index(substring)` -> vraća poziciju prve pojave traženog substringa unutar stringa, ako substring nije pronađen baca grešku
 - `string.format(arg1, arg2,...)` -> ubacuje argumente metode na predviđenja polja u stringu
 - `string.split(separator)` -> razdvoji string u listu prema određenom separatoru


Dvije vrlo korisne ali nešto kompleksnije metode sa kojima se možda još niste susreli su `format()` i `split()`.
Formatiranje se primarno koristi pri ubacivanju vrijednosti varijabli u stringove.

```Python
string = "Ja imam {} godina i zovem se {}"
ime = "Denis"
broj_godina = 12
string.format(broj_godina, ime)
print(string) # Ja imam 12 godina i zovem se Denis
```

Međutim metoda `format()` se sve rijeđe koristi i zamijenjena je f-stringovima. Oni nam omogućavaju direktnu injekciju varijabli u stringove.

```Python
ime = "Denis"
broj_godina = 12
string = f"Ja imam {broj_godina} godina i zovem se {ime}"
print(string) # Ja imam 12 godina i zovem se Denis
```

Postoji još puno opcija formatiranja stringova za koje bi mogli napisati cijelo predavanje (a to mi se neda).

### Liste


## Grananja

Grananja u Pythonu započinjemo ključnom riječi `if`, nakon toga 
