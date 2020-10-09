# Autostopistički priručnik za Python


## Predgovor

Ova skripta namijenjena je studentima i srednjoškolcima koji pohađaju PyOpen workshopove. Ovo nije knjiga koja se bavi svim značajkama ovog jezika već samo priručnik u učenju koji sadržava velik broj zanimljivosti i uputa za izradu projekata koji će se raditi na spomenutom workshopu.

Naravno ako ikoja izgubljena duša slučajno naiđe na ovu literaturu dozvoljeno joj je koristit ju u svrhu samostalne edukacije.

P.S. Unaprijed se ispričavam na svim gramatičkim i mnogim drugim pogreškama u pisanju. Ako imate prijedlog kako unaprijediti ovu skriptu ili pak *krinđujete* na moje loše poznavanje strukture rečenice u Hrvatskom jeziku više ste nego dobrodošli napraviti pull request ili objaviti issue.



## Literatura za ucenje

1. [The Hitchiker's Guide to Python.pdf](http://index-of.es/Varios-2/The%20Hitchiker%27s%20Guide%20to%20Python.pdf)

2. [Is Python interpreted or compiled](https://nedbatchelder.com/blog/201803/is_python_interpreted_or_compiled_yes.html)


## Komedija, zmija ili programski jezik

Python, nama danas poznat kao *high level, open source* programski jezik, započeo je 1980-ih godina u Nizozemskoj.

Tada mladi računalni znanstvenik pod imenom Guido van Rossum radio je na Državnom Istraživačkom Institutu za Matematiku i Računalne Znanosti u Amesterdamu. Bio je dio skupine znanstvenika koja se bavila razvijanjem Amoeba operacijskog sustava i na božić 1989 godine stvorio je Python sa svrhom da bude skriptni jezik koji bi olakšao sistem administraciju u Amoeba os-u.

Ubrzo je Python prerastao iz malog skriptnog jezika u jedan od najpopularnijih programskih jezika na svijetu a u svrhu njegovog održavanja, promoviranja i razvoja stvoren je *Python Software Foundation*.

S obzirom da je logo Pythona zmija većina ljudi misli da je ovaj programski jezik ime dobio po toj egzotičnoj, ubojitoj životinji, međutim Guido sam govori kako ga je imenovao prema BBC-evoj popularnoj humorističnoj eriji *Monty Python’s Flying Circus*



## Na što mislimo kada kažemo Python

Sama riječ Python označava skup pravila koji definiraju jedan specifični programski jezik. Ali kada od nekog čujete da programira u Pythonu ta osoba najčešće želi reći da programira u specifičnoj implementaciji tog skupa pravila koja se naziva CPython koju ćemo i mi koristiti na radionicama.

**CPython** je implementacija našeg specifičnog skupa pravila pomoću C programskog jezika. To je ona verzija Pythona koju dobijete kada skinete Python sa [python.org](https://www.python.org/downloads/) stranice i uz to je i originalna verzija Pythona koja prva implementira nove featureove. Na ovu verziju ćemo se i mi referirati kada budemo pričali o Pythonu. Pogodnost ove implementacije Pythona je ta što može pozivati kod pisan u C programskom jeziku što doprinosi brzini izvođenja programa.

Osim CPythona postoji još zanimljivih implementacija.

**Jython** je implementacija Pythona u programskom Jeziku javi. Jython kompajla Python kod u Java bytecode i omogućuje njegovo pokretanje unutar Java virtualne mašine (JVM). Uz to korištenje Jythona programeru otvara mogućnost korištenja Java biblioteka i klasa zajedno sa Python kodom.

**Skulpt** je compiler koji prevodi Python u JavaScript, može se pokretati direktno iz web preglednika i koristi se u edukacijske svrhe.

**RPython** je kompajer koji prevodi Python kod u C i nad programerom podstavlja ograničenja *strictly typed* programskih jezika. RPython ne nazivamo Python implementacijom zbog toga što sav Python kod ne možemo smatrati RPython kodom, ali sav kod koji možemo pokrenutir RPythonom, standardna implementacija PYthona može također pokrenuti. Zbog toga RPython najčešče nazivamo podskupom Python jezika.

Na ovom primjeru možemo uočiti razliku između standardnog Pythona i RPythona:


```python
#FUNCTIONS
def add(x,y):
 return x + y

#MAIN CODE
add(1, 2)
add("Mirko", "Slavko")
```

U standardnom Pythonu primjer ovakvog koda je sasvim validan. Međutim RPython koji prevodi naš python kod u *strictly typed* programski jezik mora poznavati koji tip argumenata prima funkcija `def add(x, y)`. U prvom pozivu funkcije add `add(1, 2)` RPython compiler opaža da smo proslijedili dva *integera* pa funkciju add deklarira kao funkciju koja kao argumente prima dva *integera*.
Prilikom drugog poziva funkcije `add("Mirko", "Slavko")` proslijedili smo kao argumente dva *stringa* što se protivi prethodnoj deklaraciji funkcije i zbog toga nam program javlja grešku.

```
[translation:ERROR] In <FunctionGraph of (rtest:9)main at 0x103f7dc58>:
[translation:ERROR] Happened at file rtest.py line 11
[translation:ERROR]
[translation:ERROR]       print add(1,2)
[translation:ERROR] ==>   print add('Graham','Jenson')
```


## Verzije Python interpretera

Ako posjetite službenu [download stranicu pythona](https://www.python.org/downloads/) susrest će te se sa velikim izborom aktivnih verzija Python interpretera različitih verzija.

| Version       | Maintanance status |
| ------------- | ------------------ |
| 3.9           | bugfix             |
| 3.8           | bugfix             |
| 3.7           | security           |
| 3.6           | security           |
| 3.5           | end-of-life        |
| 2.7           | end-of-life        |

S obzirom da online Python tutoriali i knjige često datiraju i do 10 godina unatrag te različite verzije nazivaju najboljim ili aktualnim, novopridošlim python developerima zna često biti težak ovaj izbor.

Pa da ukratko objasnimo. Python 2.7 tj. posljednja je verzija Pythona 2 interpretera izašla 2010. godine. Python 2 dostigao je kraj svog životnog ciklusa. To bi značilo da developeri više ne rade na podršci za njega, ne izadaju se novi paketi kompatibilni snjim, ne prima bugfixove, a i sam po sebi je u usporedbi s novom Python 3 verzijom zastarjel.

Python 3 je trenutno najkorištenija verzija Python interpretera, najkorištenije njegovo izdanje je inačica Python 3.8.5, a nedavno smo dobili priliku koristiti i verziju 3.9 koja dodaje velik broj novih featureova u Python jezik.

Bitno je zapamtiti da su sve verzije Python interpretera unutar neke serije (gdje bi serije bile Python 3 serija i Python 2 serija) kompatibilne sa prethodnim verzijama unutar te serije, ali ne i obrnuto.




## The zen of python

``` python
>>> import this                                                                  
```
```
Beautiful is better than ugly.
Explicit is better than implicit.
Simple is better than complex.
Complex is better than complicated.
Flat is better than nested.
Sparse is better than dense.
Readability counts.
Special cases aren't special enough to break the rules.
Although practicality beats purity.
Errors should never pass silently.
Unless explicitly silenced.
In the face of ambiguity, refuse the temptation to guess.
There should be one-- and preferably only one --obvious way to do it.
Although that way may not be obvious at first unless you're Dutch.
Now is better than never.
Although never is often better than *right* now.
If the implementation is hard to explain, it's a bad idea.
If the implementation is easy to explain, it may be a good idea.
Namespaces are one honking great idea -- let's do more of those!
```
