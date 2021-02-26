# Osnove Pythona

U ovom poglavlju objasniti ćemo osnovne gradivne elemente koje nam Python pruža pri dizajniranju i izradi softwarea.

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
 - **str** , **list**, **tuple**, **set**, frozenset (iterabilni podatci)
 - **dict**
 - **bool** (True/False)
 - bytes, bytearray, memoryview (binarni tipovi)

Prema način tretiranja varijabli i podataka Python klasificiramo kao *dynamically typed* i *strong typed* programski jezik.

Dinamička tipiziranost govori nam da u Pythonu tip podatka vežemo za neku vrijednost, a ne za samu varijablu. Zbog toga u pythonu deklaracija varijable na *"tradicionalan"* način nije potrebna, tj. pri stvaranju varijable nemoramo eksplicitno reči koji će biti njen tip. To nam omogućava i da unutar *runtimea* programa mijenjamo tip podatka koji je vezan za varijablu.

Za razliku od C programskog jezika gdje ovakav kod rezultira kompajlerskom pogreškom.

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

Brojevi, numerički podatci su brojevi, što reći još.

Dobra stvar za napomenuti bila bi da Python iz nekog razloga nema definiranu operaciju inkrementacije `var++`, umjesto toga morat će te kao kakvi prljavi, neoptimizirani špiljski čovjek koristiti izraz `var += 1`.

Numerički podaci u Pythonu su zanimljivi zbog toga što je veličina broja kojeg možemo u pisati u varijablu ograničena samo radnom memorijom uređaja. 

Cjelobrojne vrijenosti možemo zadati i pomoću prefiksa baze brojevnog sustava kojeg koristimo.

```Python
print(0o10)
# 8
print(0x10)
# 16
print(0b10)
# 2
```

#### String

String je nepromjenjivi niz characterova. Navodi se unutar jednostrukih ili dvostrukih navodnika.

```Python
broj = 123
broj_string = "123"
broj_string_drugi = '123'
```

Osnovne operacije definirane nad stringovima su:
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

Množenje, je nešto neobičniji operator nad stringovima, za njega je bitno da string možemo množiti samo sa cijelim brojem što rezultira uzastopnom zbrajanju stringa samim sa sobom. 

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
print(string) # "Ja imam 12 godina i zovem se Denis"
```

Međutim metoda `format()` se sve rijeđe koristi i zamijenjena je f-stringovima. Oni nam omogućavaju direktnu injekciju varijabli u stringove.

```Python
ime = "Denis"
broj_godina = 12
string = f"Ja imam {broj_godina} godina i zovem se {ime}"
print(string) # "Ja imam 12 godina i zovem se Denis"
```

Postoji još puno opcija formatiranja stringova za koje bi mogli napisati cijelo predavanje (a to mi se neda).


#### Lista

Lista je tip podatka koji nam omogućava pohranjivanje više podataka unutar jedne varijable i njena osnovna svojstva su:
 - možemo promijeniti pojedini element
 - dozvoljavaju duplikate
 - svaki element ima redni broj (indeks) pomoću kojeg ga referenciramo

Liste se kreiraju koristeći uglate zagrade (kao nizovi u drugim programskim jezicima). A pojedinom elementu pristupamo putem indeksa.

```Python3
lista = [1, 2, "Ante", [1,2, "Zdravko"]]
print(lista[2]) # "Ante"
```

Osnovne operacije definirane definirane nad listama su:
 - indeksiranje
 - zbrajanje
 - množenje

Indeksiranje smo već spomenuli. Zbrajanje nam omogućava ujedinjavanje vrijednosti dvaju lista u jednu listu.

```Python
niz1 = [3, 6, 5]
niz2 = ["Je", "Prošlo", "Dana"]

niz3 = niz1 + niz2
print(niz3) # [3, 6, 5, "Je", "Prošlo", "Dana"]
```

Množenje funkcionira jednako kao i kod stringova, moguće je samo između liste i cijelog broja i to rezultira uzastopnim zbrajanjem liste samom sa sobom.

```Python
niz1 = ["pss"] * 3
print(niz1) # ["pss", "pss", "pss"]
```

Metode implementirane nad listama su:
 - `lista.append(value)` -> dodaje value na kraj liste
 - `lista.clear()` -> briše sve elemente iz liste
 - `lista.copy()` -> vraća kopiju liste
 - `lista.index(value)` -> vraća indeks prvog elementa čija je vrijednost jednaka value, baca grešku ukoliko traženi element ne postoji
 - `lista.count(value)` -> vraća broj ponavljanja vrijednosti value unutar liste
 - `lista.insert(position, value)` -> dodaje value na poziciju s indeksom position
 - `lista.pop(position=-1)` -> izbacuje element sa pozicije position, ukoliko pozicija nije proslijeđena izbacuje zadnji element
 - `lista.remove(value)` -> izbacuje prvi element vrijednosti value
 - `lista.reverese()` -> preokreće redoslijed elemenata
 - `lista.sort(reverse, key)` -> sortira listu uzlazno ili izlazno, ovisno o bool parametru reverse. Ako želimo definirati proizvoljni kriterij sortiranja možemo proslijediti funkciju u argument key pomoću koje opisujemo to pravilo

Ostali iterabilini elementi gotovo su identični listama tako da se nećemo pretjerano zadržavati na njihovim svojstvima.


#### Tuple

Tuple je tip podatka sličan listi s iznimkom da ne možemo promijeniti pojedini element tuplea.

Tupleovi se kreiraju koristeći okrugle zagrade umjesto uglatih. Kao i stringove, možemo ih indeksirati ali ne možemo mijenjati vrijednost na pojedinom indeksu.

```Python
tapl = ("Mate", "Mišo", "Kovač")
tapl[0] = "Ante"
# TypeError: 'tuple' object does not support item assignment
```

Jedini naćin da dodamo novi element u tuple je da stvorimo novi tuple sa elementima početnog tuplea i novim podatcima koje želimo ubaciti u njega. Zbog toga tupleovi ne podržavaju metodu `append()` ali podržavaju zbrajanje tupleova.

Metode definirane nad tupleovima su:
 - `tuple.count(value)` -> vraća broj ponavljanja vrijednosti value unutar tuplea
 - `tuple.index(value)` -> vraća poziciju prve pojave tražene vrijednosti value unutar tuplea, ako vrijednost nije pronađena baca grešku


#### Set

Set predstavlja matematički skup podataka. Za razliku od ostalih iterabilnih vrsta podataka on ne podržava duplikate. Za bilo koja dva elementa za koja vrijedi operacija jednakosti `==`, set će automatski pohraniti samo jednu od njih.

Definira se vitićastim zagradama umjesto uglatim. Dopušta nam indeksiranje elemenata, ali kao i kod tupleova, ne možemo mijenjati vrijednost na pojedinom indeksu.

```Python
skup = {1, 2, 3, 4, 5, 5, 2, 1, 2}
print(skup) # {1, 2, 3, 4, 5}
skup[0] = 2
```

Zanimljiva stvar je ta što kod dvaju setova njihva jednakost ne ovisi o rasporedu elemenata, dok kod ostalih iterabilnih tipova podataka ovisi.

```Python
skup1 = {"Mate", "Mišo", "Kovač"}
skup2 =  {"Kovač", "Mišo", "Mate"}
print(skup1 == skup2) # True

tupl1 = ("Marko", "Perković", "Thompson")
tupl2 = ("Thompson", "Marko", "Perković")
print(tupl1 == tupl2) # False
```

Setovi se koriste za dedupliciranje podataka.

Za razliku od tupleova i lista, setove ne možemo zbrajati i množiti.

Metode nad setovima bazirane su većinom na matematičkim operacijama nad skupovima (nabrojit ćemo samo neke od njih):
 - `set.add(value)` -> dodaje element vrijednosti value u set
 - `set.clear()` -> briše sve elemente iz seta
 - `set.copy()` -> vraća kopiju seta
 - `set.difference(drugi_set)` -> razlika dvaju setova
 - `set.difference_update(drugi_set)` -> iz izvornog seta briše elemente koji se nalaze u njemu i u setu drugi_set
 - `set.discard(value)` —> briše element određene vrijednosti value
 - `set.remove(value)` -> briše element određene vrijednosti value, i baca grešku ukoliko ta vrijednost ne postoji
 - `set.pop(position=-1)` -> izbacuje element sa pozicije position, ukoliko pozicija nije proslijeđene izbacuje zadnji element

#### Dict

Ako prevedemo ime ove strukture podataka (dictionary) na hrvatski, dobijemo riječ koja savršeno opisuje naćin na koji ona radi, rječnik. Za razliku od prethodnih složenih tipova podataka koje smo obradili, koji neku informaciju povezuju sa rednim brojem i omogućavaju nam pristup podatku pomoću tog rednog broja kojeg nazivamo indeks, dictovi vežu informaciju uz bilo kakav objekt kojeg je moguće hashirati (točnije mora biti immutable, zbog toga ne možemo koristiti listu kao key, ali tuple možemo) po sistemu key-value pair.

Definiraju se korištenjem vitićastih zagrada. Sintaksa je vrlo slična JSON formatu. Podatke možemo dohvatiti indeksiranjem traženog ključa.

```Python
rjecnik = {
	"Ključ": "Vrijednost",
	"rječnik": ["dictionaries", "glossary", "lexicon", "thesaurus"],
	("Marko", "Perković", "Thompson"): ["Su", "De", "Mi"]
}

rjecnik["Ključ"] = "Neka druga vrijednost"
print(rjecnik["Ključ"]) # "Vrijednost"
```

Metode definirane nad dictovima su:
 - `dict.clear()` -> briše sve elemente iz dicta
 - `dict.copy()` -> vraća kopiju dicta
 - `dict.fromkeys(keys, default_value)` -> vraća dict sa određenim keyevima i defaultnom vrijednošću
 - `dict.get(key, fallback_value)` -> dohvaća vrijednost specificirano ključa key, ako key ne postoji vraća fallback_value
 - `dict.items()` -> vraća objekt tipa dict_items što je iterabilni tip koji sadrži tupleove gdje je prvi element u tupleu pojedini key, a drugi element value vezan uz taj key
 - `dict.keys()` -> vraća objekt tipa dict_keys što je iterabilni tip koji sadrži sve keyove dicta
 - `dict.pop(key)` -> izbacuje vrijednost pod ključem key 
 - `dict.popitem()` -> izbacuje zadnji ubaćeni key-value par
 - `dict.setdefault(key, value)` -> vraća vrijednost vezanu uz ključ key, ako ključ ne postoji dodaje ga i uz njege veže vrijednost valu 
 - `dict.update(dict2)` -> updatea dict pomoću drugog dicta
 - `dict.values()` -> vraća objekt tipa dict_values što je iterabilni tip koji sadrži sve valuove dicta


#### Bool

Booleova varijabla, vrijednost `True` ili `False`. Što još reći.

Zanimljivo je zamjetiti da, s obzirom da vrijednosti `True` i `False` predstavljaju nulu i jedinicu, možemo vršiti matematičke operacije pomoću njih.

```Python
print(True + 3.5) # 4.5
```

Isto tako možemo i usporediti brojevne vrijednosti sa booleovima.

```Python3
print(False == 0) # True
print(True == 1) # True
print*(True == 2) # False
```

Ali ako ih usporedimo sa stvarima kao što su prazna lista i prazan string (koji su nešto što nazivamo falsy vrijednostima, tj. oni se unutar grananja tretiraju kao `False`) vidjet ćemo da usporedba uvijek rezultira vrijednosti `False`.


```Python
print([] == True) # False
print([] == False) # False
```

Iako bi gledajući ovaj kod došli do drukčijeg zaključka:

```Python
if []:
	print("Ovo je istina")
else:
	print("Ovo je neistina")

# "Ovo je neistina"
```

To nas vodi do zaključka da booleovi u Pythonu nisu ništa drugo nego undercover intovi.

![piderman meme](./images/piderman-meme.jpg)


#### Tips and tricks (stvari koje bi trebalo reći a neznan gdje ih svrstati)

Tokom navođenja tipova podataka siguran sam da su negdje spomenuti iterabilni tipovi. Za sada vam je dovoljno znati da pod iterabilnim tipovima možemo smatrati sve kroz što teoretski možemo prolaziti `for` petljom.

Pod iterabilne elemente spadaju: string, lista, tuple, set, dict_values, dict_keys, dict_items, ali možemo definirati i custom iterabilne elemente sa posebnim svojstvima. Činjenica da svi elementi koji predstavljaju skup nekakvih vrijednosti potječu iz istog tipa podatka omogućava pythonu definiranje funkcija koje su primjenjive nad velikim brojem različitih tipova podataka.

Kroz ova predavanja upoznat ćemo se sa velikim brojem built in custom iterabilnih elemenata kao što su `range` i `enumerate`.

Neke metode koje možemo primijeniti nad iterabilnim elementima su:
 - `any(iterable)` -> vraća `True` ako postoji barem jedan ne falsy element unutar iterabila
 - `all(iterable)` —> vraća `True` ako ne postoji nijedan falsy element unutar iterabila
 - `map(callback, iterable)` -> pokreće funkciju callback nad svakim elementom iterabila i vraća nam iterabil koji se sastoji od vraćenih vrijednosti funkcije callback
 - `filter(callback, iterable)` -> pokreće funkciju callback nad svakim elementom iterabila i vraća nam iterabil koji se sastoji od svih elemenata početnog iterabila za koje callback funkcija vraća vrijednost `True`
 - `len(iterable)` -> vraća duljinu iterabila
 - `sorted(iterable, key)` -> Sortira iterabil uzlazno ili prema proizvoljnom kriteriju opisanom funkcijom key ako je definirana
 

Postoji i jedan kul patern koji se zove raspakiravanje iterabila (unpacking) koji je poprilično self explanatory:

```Python
lista = ["Mate", "Mišo", "Kovač"]
ime1, ime2, prezime = lista

print(ime1) # "Mate"
print(ime2) # "Mišo"
print(prezime) # "Kovač"
```

S obzirom da su iterabilni tipovi svi međusobno jako slični možemo vrlo lako vršiti pretvorbu među njima.

U pythonu se pretvorba iz jednog tipa podatka u drugi vrši prosljeđivanjem podatka kojeg želimo pretvorit konstruktoru klase podatka u koji ga želimo pretvorit. Komplicirana rečenica koju je lakše shvatiti na primjeru. Pokušajmo za "proizvoljan broj" izdvojiti sve duplikate znamenki koristeći samo različite iterabilne tipove.


```Python
proizvoljan_broj = 112233
string_proizvoljnog_broja = str(proizvoljan_broj) # "112233"

# Sada taj string možemo rastaviti na pojedinačne znamenke tj. characterove
lista_znamenki = list(string_proizvoljnog_broja) # ["1", "1", "2", "2", "3", "3"]

# Sada tu listu pretvorimo u set da se riješimo duplikata 
# (mogli smo odma i string pretvoriti u set i dobili bi isti rezultat ali ovako imamo jednu pretvorbu više, a to je cilj primjera kao...)
set_znamenki = set(lista_znamenki)

# sada sve znamenke ponovno spojimo u string pa pretvorimo u broj
string_novog_broja = "".join(set_znamenki)
novi_broj = int(string_novog_broja)

# Postoji puno efikasniji naćin za napravit ovo
# Molim vas nemojte ovo pisat negdje gdje će netko gledat vaš kod
# Ako budete nemojte nikom govoriti da sam vas ja to naučio
```

## Grananja

Grananja u Pythonu započinjemo ključnom riječi `if`, nakon toga.

