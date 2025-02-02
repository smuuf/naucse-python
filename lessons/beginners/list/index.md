Encyklopedické informace z této stránky shrnuje
[Tahák na seznamy](https://github.com/pyvec/cheatsheets/blob/master/lists/lists-cs.pdf),
který si můžeš vytisknout.

# Seznamy

Dnes si ukážeme, jak pracovat se *seznamy* (angl. *lists*).

Začneme prakticky.
Vytvoř si seznam pomocí následujícího kódu:

```python
zviratka = ['pes', 'kočka', 'králík']
print(zviratka)
```

> [note]
> Nemůžeš najít hranaté závorky?
> Na české klávesnici zkus pravý <kbd>Alt</kbd> + <kbd>F</kbd> a <kbd>G</kbd>.

Seznam je hodnota, která může obsahovat spoustu dalších hodnot.
Tak jako řetězec obsahuje sekvenci znaků,
seznam obsahuje sekvenci jakýchkoli hodnot.
V našem případě obsahuje sekvenci řetězců.

A tak jako můžeš pomocí cyklu `for` procházet řetězec po znacích,
seznam můžeš procházet po jednotlivých prvcích:

```python
for zviratko in zviratka:
    print(zviratko)
```

Seznamy se v programech vyskytují často:
soubor se dá načíst jako seznam jednotlivých řádků,
matematika je plná číselných řad, e-shopy pracují se seznamy zboží,
seznam řetězců jako `'7♥'` a `'K♣'` může posloužit jako balíček karet.

Hodnoty v seznamu můžou být jakéhokoli typu:

```python
prvni_prvocisla = [2, 3, 5, 7, 11]
```

Dokonce můžeš různé typy míchat v jednom seznamu.
(S takovými namixovanými seznamy se ovšem příliš často nesetkáš.
Různé typy hodnot se používají spíš v <var>n</var>-ticích, o kterých si povíme
později):

```python
seznam = [1, 'abc', True, None, range(10), len]
print(seznam)
```

## Neměnitelné hodnoty

Důležitá vlastnost seznamů je, že se dají *měnit*.

Než vysvětlíme o co jde, připomeňme si jak fungují hodnoty, které se měnit
nedají – např. čísla, řetězce, `True`, `False`, `None`.

Vyzkoušej si následující kousek kódu. Co je na něm „špatně“?

```python
kamaradka = 'Žaneta'
print(kamaradka)
kamaradka.upper()
print(kamaradka)
```

Proměnná `kamaradka` obsahuje řetězec `'Žaneta'` (který se už nedá změnit).
Metoda `upper()` vytvoří a vrátí *nový* řetězec `'ŽANETA'`.
Výsledná hodnota se ale v našem programu nevyužije – Python ji vytvoří,
ale pak ji „zahodí“.

Oprava je snadná: výsledek si ulož do proměnné.
Často budeš chtít takový výsledek uložit zpátky do původní proměnné:

```python
kamaradka = kamaradka.upper()
```

Tímto přiřazením Python „zahodí“ původní hodnotu.
Od tohoto příkazu dál bude proměnná `kamaradka` označovat nový řetězec.

Podobně by se dala proměnná přenastavit na jakoukoli jinou hodnotu:

```python
kamaradka = 'Žaneta'
print(kamaradka)
kamaradka = 'Alexandra'
print(kamaradka)
```


## Měnění seznamů

A jak jsou na tom seznamy?
Ty se měnit dají.

Základní způsob jak změnit seznam je přidání
prvku na konec pomocí metody `append`.
Ta *nic nevrací* (resp. vrací `None`), ale „na místě” (angl. *in place*) změní
seznam, se kterým pracuje. Vyzkoušej si to:

```pycon
>>> zviratka = ['pes', 'kočka', 'králík']
>>> print(zviratka)
['pes', 'kočka', 'králík']
>>> zviratka.append('morče')
>>> print(zviratka)
['pes', 'kočka', 'králík', 'morče']
```

Všimni si, že proměnná `zviratka` se nastavuje jen na začátku.
V rámci celého běhu programu výše existuje jen jeden seznam.
Na začátku má tři prvky, pak mu jeden přibude, ale stále je to jeden a ten
samý seznam.

Takové měnění může být občas překvapující,
protože stejná hodnota může být přiřazená ve více proměnných.
Protože se mění hodnota samotná, může to vypadat,
že se „mění proměnná, aniž na ni sáhneš”:

```python
a = [1, 2, 3]   # Vytvoření seznamu
b = a           # Tady se nový seznam nevytváří!

# seznam vytvořený v prvním řádku má teď dvě jména: "a" a "b",
# ale stále pracuješ jenom s jedním seznamem

print(b)
a.append(4)
print(b)
```


## Další způsoby, jak měnit seznamy

Kromě metody `append`, která přidává jediný prvek na konec, existuje
spousta dalších metod, které seznamy mění.
Všechny udělají změny přímo v daném seznamu a (kromě `pop`) vrací `None`:

* `extend()` přidá více prvků najednou,
* `pop()` odebere poslední prvek a *vrátí ho* (jako návratovou hodnotu),
* `insert()` přidá prvek na danou pozici,
* `remove()` odstraní první výskyt daného prvku,
* `sort()` seznam seřadí (řetězce „podle abecedy”, čísla vzestupně),
* `clear()` odstraní všechny prvky.
* `reverse()` obrátí pořadí prvků,

{{ figure(img=static('methods.svg'), alt="Tahák") }}

Například:

```python
zviratka = ['pes', 'kočka', 'králík']
zviratka.append('morče')      # ['pes', 'kočka', 'králík', 'morče']
zviratka.insert(2, 'had')     # ['pes', 'kočka', 'had', 'králík', 'morče']
zviratka.pop()                # ['pes', 'kočka', 'had', 'králík'], vrátí 'morče'
zviratka.remove('had')        # ['pes', 'kočka', 'králík']
zviratka.sort()               # ['kočka', 'králík', 'pes']
zviratka.reverse()            # ['pes', 'králík', 'kočka']
zviratka.clear()              # []
```

## Vybírání ze seznamů

Často budeš ze seznamu chtít vybrat prvek na určité pozici.
To funguje jako u řetězců: do hranatých závorek dáš číslo prvku.
Stejně jako u řetězců se čísluje od nuly a záporná čísla číslují od konce.

```python
zviratka = ['pes', 'kočka', 'králík']
print(zviratka[2])
```

Hranatými závorkami můžeš získat i podseznam.
[Diagram z materiálů k řetězcům]({{ lesson_url('beginners/str-index-slice')}}#slicing-diagram)
ukazuje, jak u takového „sekání” číslovat:
funguje to stejně, jen místo menšího řetězce dostaneš menší seznam.

```python
zviratka = ['pes', 'kočka', 'králík', 'had', 'andulka']
print(zviratka[1:-2])
```

„Sekáním“ vzniká nový seznam – když pak původní seznam změníš, v novém menším seznamu se
to neprojeví.


### Měnění prvků

Na rozdíl od řetězců (které se měnit nedají) můžeš u existujících seznamů
nastavovat konkrétní prvky – a to tak, že do prvku přiřadíš jako by to byla
proměnná:

```python
zviratka = ['pes', 'kočka', 'králík']
zviratka[1] = 'koťátko'
print(zviratka)
```

Přiřazovat se dá i do podseznamu – v tomto případě
se podseznam nahradí jednotlivými prvky z toho,
co přiřadíš.

```python
zviratka = ['pes', 'kočka', 'králík', 'had', 'andulka']
print(zviratka[1:-2])
zviratka[1:-2] = ['koťátko', 'králíček']
print(zviratka)
```

### Mazání prvků

Přiřazením do podseznamu můžeš i změnit délku
seznamu nebo některé prvky úplně odstranit:

```python
zviratka = ['pes', 'kočka', 'králík']
zviratka[1:-1] = ['had', 'ještěrka', 'drak']
print(zviratka)
zviratka[1:-1] = []
print(zviratka)
```

Tenhle zápis pro mazání prvků je ale docela nepřehledný.
Proto na to existuje zvláštní příkaz jménem `del`.
Jak už jeho název (z angl. *delete*, smazat)
napovídá, smaže, co mu přijde pod ruku – jednotlivé
prvky seznamů, podseznamy, … a dokonce i proměnné!
Zkus si:

```python
zviratka = ['pes', 'kočka', 'králík', 'had', 'ještěrka', 'andulka']

# Smazání prvku seznamu
print(zviratka[-1])
del zviratka[-1]
print(zviratka)

# Smazání podseznamu
print(zviratka[1:-1])
del zviratka[1:-1]
print(zviratka)
```

> [note]
> Příkaz `del` umí mazat i proměnné.
> Po takovém smazání se proměnná chová jako kdyby do ní nikdo nikdy nic
> nepřiřadil:
>
> ```python
> del zviratka
> print(zviratka)
> ```
>
> V praxi se ale `del` na proměnné příliš často nepoužívá.


Na mazání prvků můžeš použít i metody zmíněné výše:
* `pop` odstraní poslední prvek v seznamu a *vrátí* ho,
* `remove` najde v seznamu první výskyt daného prvku a odstraní ho,
* `clear` vyprázdní celý seznam.

```python
balicek = ['eso', 'sedma', 'svršek', 'sedma', 'král']
liznuta_karta = balicek.pop()
print(liznuta_karta)
print(balicek)

balicek.remove('sedma')
print(balicek)

balicek.clear()
print(balicek)
```

## Řazení

Metoda `sort` seřadí prvky seznamu.

```python
seznam = [4, 7, 8, 3, 5, 2, 4, 8, 5]
seznam.sort()
print(seznam)
```

Aby se daly seřadit, musí být prvky seznamu vzájemně
*porovnatelné* – konktrétně na ně musí fungovat operátor `<`.
Seznam s mixem čísel a řetězců tedy seřadit nepůjde.
Operátor `<` definuje i jak přesně `sort` řadí: čísla vzestupně podle
velikosti; řetězce podle speciální „abecedy” která řadí
malá písmena za velká, česká až za anglická, atd.

Metoda `sort` zná pojmenovaný argument `reverse`.
Pokud ho nastavíš na *True*, řadí se naopak – od největšího prvku po nejmenší.

```python
seznam = [4, 7, 8, 3, 5, 2, 4, 8, 5]
seznam.sort(reverse=True)
print(seznam)
```

## Známé operace se seznamy

Spousta toho, co můžeš dělat s řetězci, má stejný účinek i u seznamů.
Třeba sečítání a násobení číslem:

```python
melodie = ['C', 'E', 'G'] * 2 + ['E', 'E', 'D', 'E', 'F', 'D'] * 2 + ['E', 'D', 'C']
print(melodie)
```

Stejně jako u řetězců jde se seznamem sečíst jen další seznam.
Nemůžeš sečítat třeba seznam s řetězcem.

Další staří známí jsou funkce `len`,
metody `count` a `index`, a operátor `in`.

```python
print(len(melodie))         # Délka seznamu
print(melodie.count('D'))   # Počet 'D' v seznamu
print(melodie.index('D'))   # Číslo prvního 'D'
print('D' in melodie)       # Je 'D' v seznamu?
```

Poslední tři se ale přece jen chovají kapku jinak:
u řetězců pracují s *podřetězci*,
u seznamů jen s *jednotlivými* prvky.
Takže ačkoliv melodie výše obsahuje prvky
`'D'` a `'E'` vedle sebe, `'DE'` ani `['D', 'E']` v seznamu není:

```python
print('DE' in melodie)
print(melodie.count('DE'))
print(melodie.index('DE'))
```

## Seznam jako podmínka

Seznam můžeš použít v příkazu `if` (nebo `while`) jako podmínku,
která platí, když v tom seznamu něco je.
Jinými slovy, `seznam` je tu „zkratka“ pro `len(seznam) > 0`.

```python
if seznam:
    print('V seznamu něco je!')
else:
    print('Seznam je prázdný!')
```

Podobně můžeš v podmínce použít i řetězce.
A dokonce i čísla – ta jako podmínka platí, pokud jsou nenulová.

## Tvoření seznamů

Tak jako funkce `int` převádí na
celá čísla a `str` na řetězce,
funkce `list` převádí na seznam.
Jako argument jí můžeš předat jakoukoli hodnotu,
kterou umí zpracovat příkaz `for`.
Z řetězce udělá seznam znaků, z `range` udělá seznam čísel.

```python
abeceda = list('abcdefghijklmnopqrstuvwxyz')
cisla = list(range(100))
print(abeceda)
print(cisla)
```

I ze seznamu udělá funkce `list` seznam.
To může znít zbytečně, ale není – vytvoří se totiž *nový* seznam.
Bude mít sice stejné prvky ve stejném pořadí,
ale nebude to ten samý seznam:
měnit se bude nezávisle na tom starém.

```python
a = [1, 2, 3]
b = list(a)

print(b)
a.append(4)
print(b)
print(a)
```

Další způsob, jak tvořit seznamy
(zvláště složitější), je nejdřív udělat prázdný
seznam a pak ho postupně naplnit pomocí funkce `append`.
Třeba pokud z nějakého důvodu chceš seznam
mocnin dvou, projdi čísla, kterými chceš mocnit,
cyklem `for` a pro každé z nich
do seznamu přidej příslušnou mocninu:

```python
mocniny_dvou = []
for cislo in range(10):
    mocniny_dvou.append(2 ** cislo)
print(mocniny_dvou)
```

Podobným způsobem získáš seznam seznam `matka`, `babička`, `prababička`,
`praprababička`, atd.:

```python
predkove = ['matka']
for pocet_pra in range(10):
    predkove.append(('pra' * pocet_pra) + 'babička')
print(predkove)
```

Chceš-li seznam, který reprezentuje balíček karet,
zavolej `append` pro všechny kombinace barev a hodnot.
Neboli česky:

* Začni s prázdným **balíčkem**.
* Pro každou ze čtyř **barev** (*přidáme 13 karet té barvy, a to následovně*):
  * Pro každou ze 13 **hodnot**, 2-10 a 4 karty s obrázkem:
    * Přidej do **balíčku** kartu s danou **barvou** a **hodnotou**.
* **Balíček** je hotový, vypiš ho.

Takový program může být trochu složitější vymyslet.
Začít můžeš programem, který všechny karty jen vypíše:

```python
for barva in '♠', '♥', '♦', '♣':
    for hodnota in ['2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K', 'A']:
        print(hodnota, barva)
```

A pak program změň tak, aby každou kartu místo vypsání přidal do seznamu:

```python
balicek = []
for barva in '♠', '♥', '♦', '♣':
    for hodnota in ['2', '3', '4', '5', '6', '7', '8', '9', '10', 'J', 'Q', 'K', 'A']:
        balicek.append(hodnota + barva)
print(balicek)
```

Výsledný program porovnej s českým „překladem“ výše.


> [note] Jde to líp?
> Psát do programu výčet po sobě jdoucích čísel,
> `'2', '3', '4', '5', '6', '7', '8', '9', '10'`,
> není ideální – na takovou otročinu přece máme počítače!
> Zkus čísla dostat pomocí `range`.
> Ale pozor, není to úplně přímočaré:
>
> * Jaké argumenty dáš funkci `range`, abys dostal{{a}} čísla od 2 do 10?
> * Funkce `range` vrací sekvenci, která ale není seznam.
>   Abys ji mohl{{a}} spojit se seznamem `['J', 'Q', 'K', 'A']`, budeš ji muset
>   na seznam převést: `list(range(...))`
> * Abys mohl{{a}} čísla z `range` připojit k řetězci jako `♠`, budeš muset
>   každou hodnotu před použitím převést na řetězec: `str(hodnota)`.
>
> Bonus: Jaký je nejkratší zápis, kterým můžeš zadat seznam
> `['J', 'Q', 'K', 'A']`?
>
> Řešení najdeš v textu o kousek níže.


## Seznamy a řetězce

Seznamy a řetězce jsou druhy *sekvencí*.
Můžeš různě převádět z jednoho typu na druhý.

Funkce `list` vytvoří z řetězce seznam znaků.
Když chceš dostat seznam slov, použij
na řetězci metodu `split` (angl. *rozdělit*):

```python
slova = 'Tato věta je složitá, rozdělme ji na slova!'.split()
print(slova)
```

Metoda `split` umí brát i argument.
Pokud ho předáš, řetězec „rozseká” podle daného oddělovače
(místo mezer a nových řádků).
Takže když máš nějaká data oddělená čárkami,
použij `split` s čárkou:

```python
zaznamy = '3A,8B,2E,9D'.split(',')
print(zaznamy)
```

Chceš-li spojit seznam řetězců zase dohromady
do jediného řetězce, použij metodu `join` (angl. *spojit*).
Pozor, tahle metoda se volá na *oddělovači*,
tedy na řetězci, kterým se jednotlivé kousky „slepí” dohromady.
Seznam jednotlivých řetězců bere jako argument.

```python
veta = ' '.join(slova)
print(veta)
```

## Úkol

Představ si, že ti uživatelé zadávají jména a příjmení a ty si je ukládáš do
seznamu pro další použití např. v evidenci studentů. Ne všichni jsou ale pořádní,
a tak se v seznamu sem tam objeví i jméno s nesprávně zadanými velkými písmeny.
Například:

```python
zaznamy = ['pepa novák', 'Jiří Sládek', 'Ivo navrátil', 'jan Poledník']
```

Úkolem je:

* Napsat program, který vybere jen ty správně zadané záznamy, které mají správně
jméno i příjmení s velkým počátečním písmenem.
* Napsat program, který vybere naopak jen ty nesprávně zadané záznamy.
* *(Nepovinný)* – Napsat program, který opraví špatné záznamy.

Výsledný kód by měl fungovat takto:

```python
zaznamy = ['pepa novák', 'Jiří Sládek', 'Ivo navrátil', 'jan Poledník']

print(chybne_zaznamy) # → ['pepa novák', 'Ivo navrátil', 'jan Poledník']

print(spravne_zaznamy) # → ['Jiří Sládek']

print(opravene_zaznamy) # → ['Pepa Novák', 'Jiří Sládek', 'Ivo Navrátil', 'Jan Poledník']
```

> [note]
> Snadný způsob jak zjistit, zda je řetězec složen jen z malých písmen,
> je metoda `islower()`, která vrací True, pokud řetězec obsahuje jen malá
> písmena, jinak vrací False. Například `'abc'.islower() == True` ale
> `'aBc'.islower() == False`.
>
> Snadný způsob jak převést první písmenko na velké je metoda `capitalize()`:
> např. `'abc'.capitalize() == 'Abc'`

{% filter solution %}
```python
chybne_zaznamy = []
for zaznam in zaznamy:
    jmeno_a_prijmeni = zaznam.split(' ')
    jmeno = jmeno_a_prijmeni[0]
    prijmeni = jmeno_a_prijmeni[1]
    if jmeno[0].islower() or prijmeni[0].islower():
        chybne_zaznamy.append(zaznam)

spravne_zaznamy = []
for zaznam in zaznamy:
    jmeno_a_prijmeni = zaznam.split(' ')
    jmeno = jmeno_a_prijmeni[0]
    prijmeni = jmeno_a_prijmeni[1]
    if not jmeno[0].islower() and not prijmeni[0].islower():
        spravne_zaznamy.append(zaznam)

opravene_zaznamy = []
for zaznam in zaznamy:
    jmeno_a_prijmeni = zaznam.split(' ')
    jmeno = jmeno_a_prijmeni[0]
    prijmeni = jmeno_a_prijmeni[1]
    opravene_zaznamy.append(jmeno.capitalize() + ' ' + prijmeni.capitalize())
```
{% endfilter %}

## Seznamy a náhoda

Modul `random` obsahuje funkce, které mají něco společného s náhodou:
třeba nám už známou `random.randrange`.
Podívejme se na dvě další, které se hodí k seznamům.

Funkce `shuffle` seznam „zamíchá” – všechny prvky náhodně popřehází.
Seznam změní „na místě“ a nic nevrací, podobně jako metoda `sort`.

```python
import random

ciselne_hodnoty = list(range(2, 11))
pismenne_hodnoty = list('JQKA')

balicek = []
for barva in '♠', '♥', '♦', '♣':
    for hodnota in ciselne_hodnoty + pismenne_hodnoty:
        balicek.append(str(hodnota) + barva)
print(balicek)

random.shuffle(balicek)
print(balicek)
```

A funkce `choice` ze seznamu vybere jeden náhodný prvek.
S použitím seznamu tak můžeš třeba jednoduše vybrat tah pro hru
kámen/nůžky/papír:

```python
import random
mozne_tahy = ['kámen', 'nůžky', 'papír']
tah_pocitace = random.choice(mozne_tahy)
print(tah_pocitace)
```

## Vnořené seznamy

A perlička na konec!
Na začátku tohoto textu je napsáno, že seznam
může obsahovat jakýkoli typ hodnot.
Může třeba obsahovat i další seznamy:

```python
seznam_seznamu = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
```

Takový seznam se chová docela normálně – jdou
z něj třeba brát jednotlivé prvky
(které jsou ovšem taky seznamy):

```python
prvni_seznam = seznam_seznamu[0]
print(prvni_seznam)
```

A protože jsou prvky samy seznamy,
můžeme mluvit o věcech jako „první prvek druhého seznamu”:

```python
druhy_seznam = seznam_seznamu[1]
prvni_prvek_druheho_seznamu = druhy_seznam[0]
print(prvni_prvek_druheho_seznamu)
```

A protože výraz `seznam_seznamu[1]`
označuje seznam, můžeme brát prvky přímo z něj:

```python
prvni_prvek_druheho_seznamu = (seznam_seznamu[1])[0]
```

Neboli:

```python
prvni_prvek_druheho_seznamu = seznam_seznamu[1][0]
```

A má tahle věc nějaké použití, ptáš se?
Stejně jako vnořené cykly `for`
nám umožnily vypsat tabulku, vnořené seznamy
nám umožní si tabulku „zapamatovat”.

```python
velikost = 11
nasobilka = []
for a in range(velikost):
    radek = []
    for b in range(velikost):
        radek.append(a * b)
    nasobilka.append(radek)

print(nasobilka[2][3])  # dva krát tři
print(nasobilka[5][2])  # pět krát dva
print(nasobilka[8][7])  # osm krát sedm

# Vypsání celé tabulky
for radek in nasobilka:
    for cislo in radek:
        print(cislo, end=' ')
    print()
```

Co s takovou „zapamatovanou” tabulkou?
Můžeš si do ní uložit třeba pozice
figurek na šachovnici nebo křížků a koleček
ve *2D* piškvorkách.
