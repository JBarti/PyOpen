# Autostopistički priručnik za Python

## Preface

Ova skripta namjenjena je studentima i srednjoškolcima koji pohađaju PyOpen workshopove. Ovo nije knjiga koja se bavi svim značajkama ovog jezika već samo priručnik u učenju koji sadržava velik broj zanimljivosti i uputa za izradu projekata koji će se raditi na spomenutom workshopu.

Naravno ako ikoja izgubljena duša slučajno naiđe na ovu literaturu dozvoljeno joj je koristit ju u svrhu samostalne edukacije.

P.S. Unaprijed se ispričavam na svim gramatičkim i mnogom drugim pogreškama u pisanju. Ako imate prijedlog kako unaprijediti ovu skriptu ili želite popraviti loše navike koje sam stekao prilikom pisanja na Hrvatskom više ste nego dobrodošli napraviti pull request ili objaviti issue.


## Literatura za ucenje

[The Hitchiker's Guide to Python.pdf](http://index-of.es/Varios-2/The%20Hitchiker%27s%20Guide%20to%20Python.pdf)


## Na što mislimo kada kažemo Python ?



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

