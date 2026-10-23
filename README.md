# PythonProject
# Password Security Analyzer

**Nástroj pro analýzu bezpečnosti a síly hesel v jazyce Python**

![Python](https://img.shields.io/badge/Python-3.12-blue?logo=python&logoColor=white)
![Oblast](https://img.shields.io/badge/Oblast-Kybernetická%20bezpečnost-red)
![Testování](https://img.shields.io/badge/Testování-unittest-success)
![Typ projektu](https://img.shields.io/badge/Typ-Akademický%20projekt-orange)

---

## Obsah

1. [O projektu](#1-o-projektu)
2. [Motivace](#2-motivace)
3. [Cíle projektu](#3-cíle-projektu)
4. [Hlavní funkce](#4-hlavní-funkce)
5. [Použité technologie](#5-použité-technologie)
6. [Struktura projektu](#6-struktura-projektu)
7. [Požadavky](#7-požadavky)
8. [Instalace](#8-instalace)
9. [Spuštění aplikace](#9-spuštění-aplikace)
10. [Princip fungování analýzy](#10-princip-fungování-analýzy)
11. [Hodnocení síly hesla](#11-hodnocení-síly-hesla)
12. [Odhad entropie hesla](#12-odhad-entropie-hesla)
13. [Detekce běžných hesel a sekvencí](#13-detekce-běžných-hesel-a-sekvencí)
14. [Automatizované testování](#14-automatizované-testování)
15. [Ukázky analýzy](#15-ukázky-analýzy)
16. [Bezpečnostní aspekty](#16-bezpečnostní-aspekty)
17. [Současná omezení](#17-současná-omezení)
18. [Možnosti budoucího rozšíření](#18-možnosti-budoucího-rozšíření)
19. [Vzdělávací přínos projektu](#19-vzdělávací-přínos-projektu)
20. [Licence](#20-licence)

---

## 1. O projektu

**Password Security Analyzer** je aplikace vytvořená v jazyce Python, jejímž hlavním účelem je analyzovat bezpečnost a sílu uživatelských hesel.

Projekt vznikl v rámci vysokoškolského studia se zaměřením na kybernetickou bezpečnost. Zaměřuje se na problematiku tvorby bezpečných hesel, rozpoznávání snadno odhadnutelných vzorů a základních principů hodnocení odolnosti hesel proti útokům založeným na jejich hádání.

Aplikace nehodnotí heslo pouze podle jeho délky nebo podle toho, zda obsahuje malá a velká písmena, číslice a speciální znaky. Zohledňuje také další vlastnosti, například výskyt běžných hesel, opakování stejného znaku a předvídatelné posloupnosti znaků.

Součástí analýzy je rovněž odhad entropie založený na knihovně `zxcvbn`, která slouží k posuzování odhadnutelnosti hesel.

Projekt je rozdělen do samostatných modulů, obsahuje datové soubory s běžnými hesly a znakovými sekvencemi a využívá automatizované testy pro ověřování správnosti implementovaných funkcí.

Hlavním cílem není pouze vytvořit funkční program, ale také prakticky demonstrovat vybrané principy zabezpečení autentizačních údajů a ukázat, jak lze jednotlivé analytické metody spojit do jednoho nástroje.

### Základní vlastnosti

- Analýza délky hesla.
- Kontrola zastoupení jednotlivých kategorií znaků.
- Detekce běžných a snadno odhadnutelných hesel.
- Rozpoznávání opakujících se znaků a sekvenčních vzorů.
- Výpočet bodového skóre.
- Klasifikace hesla podle jeho síly.
- Odhad entropie prostřednictvím knihovny `zxcvbn`.
- Podpora znaků Unicode.
- Oddělení analytické logiky od testovacího kódu.
- Automatizované testování pomocí modulu `unittest`.

## 2. Motivace

Hesla představují jeden z nejrozšířenějších způsobů ověřování identity uživatelů. Přesto bývají často volena tak, aby se snadno pamatovala, nikoliv tak, aby byla odolná proti útokům.

Mezi typické problémy patří:

- Používání krátkých hesel.
- Opakované používání stejného hesla na více službách.
- Volba často používaných hesel.
- Používání jednoduchých číselných nebo abecedních posloupností.
- Opakování jednoho znaku.
- Vytváření předvídatelných hesel založených na běžných slovech.
- Přehnaná důvěra v přítomnost speciálních znaků.

Heslo obsahující velké písmeno, číslici a speciální znak nemusí být automaticky bezpečné. Pokud je jeho struktura předvídatelná, může být pro útočníka výrazně jednodušší jej odhadnout.

Například přidání číslice na konec běžného slova nemusí přinést takovou úroveň zabezpečení, jakou by uživatel očekával.

Z tohoto důvodu projekt kombinuje více kontrol, které společně poskytují podrobnější pohled na vlastnosti analyzovaného hesla.

Důležitým principem projektu je rozlišování mezi formální složitostí hesla a jeho skutečnou odhadnutelností.

## 3. Cíle projektu

Hlavní cíle projektu jsou následující:

1. **Analyzovat vlastnosti hesla** – zjistit jeho délku a zastoupení jednotlivých kategorií znaků.
2. **Rozpoznávat běžná hesla** – porovnávat heslo s lokálně uloženým seznamem často používaných hesel.
3. **Detekovat předvídatelné vzory** – identifikovat opakování stejného znaku a jednoduché znakové posloupnosti.
4. **Vyhodnocovat sílu hesla** – spojit výsledky jednotlivých kontrol do bodového skóre a slovního hodnocení.
5. **Odhadovat entropii** – využívat knihovnu `zxcvbn` k získání odhadu založeného na modelu hádání hesel.
6. **Podporovat bezpečné návyky** – ukázat význam délky, jedinečnosti a nepředvídatelnosti hesla.
7. **Procvičit návrh softwaru** – rozdělit program do modulů a ověřovat jeho funkčnost automatizovanými testy.
8. **Vytvořit základ pro další rozvoj** – umožnit doplňování nových analytických funkcí bez nutnosti zásadně měnit strukturu projektu.

## 4. Hlavní funkce

### 4.1 Analýza délky hesla

Aplikace zjišťuje počet znaků zadaného hesla.

Délka představuje důležitý faktor bezpečnosti, protože delší heslo může výrazně zvětšit prostor možných kombinací. Samotná délka však nezaručuje vysokou bezpečnost, pokud heslo obsahuje předvídatelné vzory.

Implementace využívá stanovené délkové hranice při výpočtu bodového skóre.

### 4.2 Kontrola kategorií znaků

Program kontroluje přítomnost následujících kategorií znaků:

- Malá písmena.
- Velká písmena.
- Číslice.
- Speciální znaky.

Výsledky jednotlivých kontrol jsou uchovávány samostatně. Díky tomu lze získat podrobnější informace o složení hesla, místo aby aplikace vracela pouze jedno výsledné hodnocení.

### 4.3 Detekce běžných hesel

Aplikace využívá lokální datový soubor `data/common_passwords.txt`.

Analyzované heslo se kontroluje vůči seznamu běžných hesel. Tato funkce pomáhá identifikovat hesla, která mohou být snadno odhadnutelná prostřednictvím slovníkových útoků.

Pokud je heslo vyhodnoceno jako běžné, aktuální pravidla jej klasifikují jako slabé.

Účinnost této kontroly závisí na kvalitě a rozsahu použitého seznamu.

### 4.4 Detekce opakujících se znaků

Program kontroluje, zda heslo neobsahuje pouze jeden opakující se znak.

Příklady:

- `aaaaaaaa`
- `11111111`
- `!!!!!!!!`

Taková hesla mají velmi předvídatelnou strukturu a jejich délka sama o sobě nepředstavuje dostatečnou ochranu.

Výsledek této kontroly je dostupný prostřednictvím vlastnosti `all_same`.

### 4.5 Detekce sekvenčních znaků

Další kontrola se zaměřuje na jednoduché posloupnosti znaků.

Příklady:

- `abcd`
- `1234`
- `9876`

Implementace používá minimální délku sekvence čtyř znaků.

Výsledky souvisejících kontrol jsou reprezentovány vlastnostmi `is_sequence` a `has_sequential_chars`.

Rozpoznávání sekvencí pomáhá identifikovat předvídatelné části hesla, které mohou snížit náročnost jeho uhádnutí.

### 4.6 Bodové hodnocení

Program vypočítává bodové skóre založené na vybraných vlastnostech hesla.

Aktuální implementace používá rozsah od 0 do 6 bodů. Zohledňuje délku hesla a přítomnost jednotlivých kategorií znaků.

Další bezpečnostní kontroly, například detekce běžného hesla nebo sekvenčních vzorů, ovlivňují jeho výslednou klasifikaci podle implementovaných pravidel.

Skóre slouží jako pomocný ukazatel a nelze jej považovat za univerzální bezpečnostní standard.

### 4.7 Slovní klasifikace síly hesla

Na základě výsledků analýzy program přiřazuje heslu slovní hodnocení.

Aktuální implementace rozlišuje následující kategorie:

| Kategorie | Význam |
|---|---|
| Weak – slabé | Heslo obsahuje vlastnosti, které usnadňují jeho uhádnutí. |
| Moderate – střední | Heslo splňuje některé požadavky, ale stále může mít bezpečnostní nedostatky. |
| Strong – silné | Heslo dosahuje dobrých výsledků podle implementovaných pravidel. |

Konkrétní výsledek závisí na pravidlech definovaných v analytickém modulu.

Ani hodnocení „Strong“ nezaručuje absolutní bezpečnost hesla proti všem možným způsobům útoku.

### 4.8 Odhad entropie

Pro další posouzení hesla aplikace využívá knihovnu `zxcvbn`.

Ta poskytuje odhad založený na modelu hádání hesel. Projekt následně převádí hodnotu `guesses_log10` na bitovou stupnici:

`entropie = guesses_log10 × log2(10)`

Výsledkem je číselná hodnota vyjádřená v bitech.

Tento ukazatel doplňuje pravidlové hodnocení a pomáhá lépe pochopit rozdíl mezi formálními vlastnostmi hesla a jeho odhadnutelností.

### 4.9 Podpora Unicode

Aplikace je určena také pro hesla obsahující znaky Unicode, tedy například písmena s diakritikou a další neanglické znaky.

Příkladem je heslo obsahující české znaky, například `Žluťoučký123!`.

Podpora Unicode je důležitá, protože skutečná hesla nemusí být omezena pouze na základní anglickou abecedu.

### 4.10 Automatizované testování

Součástí projektu jsou automatizované testy, které ověřují chování analytických funkcí.

Testy pokrývají reprezentativní případy, jako jsou slabá hesla, silnější hesla, opakující se znaky, sekvenční vzory, prázdný vstup a hesla obsahující Unicode.

Díky testům lze lépe odhalovat chyby a kontrolovat, zda pozdější změny neovlivnily již implementovanou funkcionalitu.

## 5. Použité technologie

| Technologie | Využití |
|---|---|
| Python 3.12 | Hlavní programovací jazyk |
| `zxcvbn` | Odhad odhadnutelnosti hesla |
| `unittest` | Automatizované testování |
| Textové soubory | Ukládání lokálních seznamů hesel a sekvencí |
| Git | Správa verzí, pokud je v projektu nakonfigurována |

### Python

Python tvoří základ celé aplikace. Zajišťuje zpracování vstupu, analýzu jednotlivých vlastností hesla, výpočet výsledků a organizaci programu do samostatných modulů.

### zxcvbn

Knihovna `zxcvbn` odhaduje náročnost hádání hesla s ohledem na jeho strukturu a předvídatelné vzory.

Projekt používá její výstup `guesses_log10` pro výpočet odhadu entropie v bitech.

Tato hodnota je odhadem založeným na konkrétním modelu, nikoliv přímým měřením skutečné náhodnosti hesla.

### unittest

Modul `unittest` je součástí standardní knihovny Pythonu a umožňuje vytvářet a spouštět automatizované testy.

Pro jeho použití není nutné instalovat samostatný externí balíček.

## 6. Struktura projektu

Projekt je rozdělen do několika částí, které oddělují hlavní aplikaci, analytickou logiku, testy a datové soubory.

```text
password-security-analyzer/
│
├── main.py
│
├── analyzer/
│   └── password_analyzer.py
│
├── tests/
│   ├── test_analyzer.py
│   └── test_entropy.py
│
├── data/
│   ├── common_passwords.txt
│   └── common_sequences.txt
│
├── .venv/
│
└── README.md
```

### `main.py`

Vstupní bod aplikace.

Slouží ke spuštění programu a propojuje uživatelský vstup s funkcemi určenými k analýze hesel.

### `analyzer/password_analyzer.py`

Obsahuje hlavní implementaci analýzy hesel.

Zpracovává délku, kategorie znaků, běžná hesla, opakující se znaky, sekvenční vzory a odhad entropie.

Součástí modulu je také logika potřebná k výpočtu skóre a výsledné klasifikace.

### `tests/test_analyzer.py`

Obsahuje testy hlavních funkcí analyzátoru.

Jeho účelem je ověřovat, zda program vrací očekávané výsledky pro různé typy hesel.

### `tests/test_entropy.py`

Obsahuje testy zaměřené na výpočet entropie.

Oddělení těchto testů umožňuje ověřovat numerické výsledky samostatně od ostatních kontrol.

### `data/common_passwords.txt`

Obsahuje lokální seznam běžných hesel používaný při analýze.

### `data/common_sequences.txt`

Obsahuje datový seznam znakových sekvencí používaných pro rozpoznávání předvídatelných vzorů.

### `.venv/`

Adresář obsahující virtuální prostředí Pythonu.

Virtuální prostředí umožňuje izolovat závislosti projektu od ostatních Python aplikací v systému.

Tento adresář je zpravidla vhodné vyloučit ze správy verzí, protože obsahuje prostředí specifické pro konkrétní počítač.

## 7. Požadavky

Pro spuštění projektu jsou potřeba následující komponenty:

- Python 3.12 nebo kompatibilní verze.
- Terminál či příkazový řádek.
- Zdrojové soubory projektu.
- Datové soubory používané při analýze.
- Nainstalovaná knihovna `zxcvbn`.
- Funkční virtuální prostředí Pythonu.

Projekt byl vyvíjen v prostředí Python 3.12.

Příkazy pro vytvoření virtuálního prostředí a spuštění programu se mohou mírně lišit podle operačního systému a použité distribuce Pythonu.

## 8. Instalace

Následující postup popisuje přípravu projektu v lokálním vývojovém prostředí.

### 8.1 Otevření adresáře projektu

Nejprve otevři terminál a přejdi do složky projektu.

Příklad pro Windows:

```powershell
cd C:\Users\Capta\Desktop\password-security-analyzer
```

### 8.2 Vytvoření virtuálního prostředí

Pokud virtuální prostředí ještě neexistuje, vytvoř jej příkazem:

```powershell
python -m venv .venv
```

Virtuální prostředí umožňuje instalovat potřebné knihovny nezávisle na ostatních projektech.

Pokud již prostředí `.venv` existuje, není potřeba jej vytvářet znovu.

### 8.3 Aktivace virtuálního prostředí

V prostředí Windows PowerShell lze použít:

```powershell
.\.venv\Scripts\Activate.ps1
```

V klasickém příkazovém řádku Windows:

```cmd
.venv\Scripts\activate.bat
```

**Poznámka:** Pokud používáš prostředí MSYS2 nebo máš virtuální prostředí vytvořené s jinou distribucí Pythonu, může mít odlišnou strukturu adresářů. V takovém případě používej přímo spustitelný soubor Pythonu uvnitř svého existujícího prostředí.

### 8.4 Instalace závislosti

Aplikace využívá knihovnu `zxcvbn`.

Po aktivaci prostředí ji nainstaluj příkazem:

```bash
python -m pip install zxcvbn
```

Pokud používáš existující prostředí, ve kterém je Python dostupný například prostřednictvím `.venv/bin/python.exe`, můžeš použít:

```powershell
.\.venv\bin\python.exe -m pip install zxcvbn
```

Konkrétní cesta závisí na tom, jak bylo virtuální prostředí vytvořeno.

### 8.5 Ověření instalace

Instalaci knihovny lze ověřit následujícím příkazem:

```bash
python -c "import zxcvbn; print('Knihovna zxcvbn je dostupná.')"
```

Pokud příkaz proběhne bez chyby, Python dokáže knihovnu importovat.

## 9. Spuštění aplikace

Po přípravě prostředí lze aplikaci spustit z kořenového adresáře projektu.

Standardní způsob spuštění:

```bash
python main.py
```

Pokud používáš své existující prostředí MSYS2, můžeš použít také přímou cestu:

```powershell
.\.venv\bin\python.exe main.py
```

Program následně provede operace definované ve vstupním souboru `main.py`.

Přesný způsob zadávání hesla a formát výstupu závisí na aktuální implementaci tohoto souboru.

## 10. Princip fungování analýzy

Analýza hesla je založena na kombinaci několika kontrol.

Zjednodušený průběh lze znázornit následujícím způsobem:

```text
             Zadání hesla
                   |
                   v
        Zjištění základních vlastností
                   |
                   v
       +-----------+-----------+
       |           |           |
       v           v           v
     Délka     Kategorie    Vzory znaků
                  znaků
       |           |           |
       +-----------+-----------+
                   |
                   v
         Kontrola běžných hesel
                   |
                   v
          Odhad pomocí zxcvbn
                   |
                   v
          Výpočet bodového skóre
                   |
                   v
        Výsledná klasifikace hesla
```

Tento diagram představuje koncepční přehled analytického procesu. Skutečné pořadí operací odpovídá implementaci v souboru `analyzer/password_analyzer.py`.

### 10.1 Základní vlastnosti hesla

Program nejprve zjišťuje délku hesla a přítomnost jednotlivých kategorií znaků.

Tyto informace slouží jako vstupní charakteristiky pro další vyhodnocení.

### 10.2 Kontrola předvídatelných vzorů

Následně se vyhodnocují vlastnosti, které mohou naznačovat snadnou odhadnutelnost hesla.

Patří sem například opakování jednoho znaku nebo jednoduchá posloupnost.

### 10.3 Kontrola běžných hesel

Heslo se porovnává s lokálním seznamem běžných hesel.

Tím lze zachytit některá hesla, která by samotná kontrola délky a kategorií znaků nemusela správně vyhodnotit.

### 10.4 Odhad entropie

Pomocí knihovny `zxcvbn` aplikace získává další ukazatel související s odhadnutelností hesla.

### 10.5 Výsledné hodnocení

Jednotlivé výsledky se využívají při výpočtu skóre a klasifikaci hesla.

Výsledné hodnocení je třeba chápat jako orientační posouzení podle pravidel implementovaných v projektu.

## 11. Hodnocení síly hesla

Síla hesla závisí na více faktorech. Projekt proto používá bodový systém doplněný o samostatné bezpečnostní kontroly.

Aktuální bodové skóre má rozsah od 0 do 6.

Mezi hodnocené vlastnosti patří:

- Délka hesla.
- Přítomnost malých písmen.
- Přítomnost velkých písmen.
- Přítomnost číslic.
- Přítomnost speciálních znaků.

Implementace rozlišuje dvě délkové hranice, osm a dvanáct znaků. Jejich konkrétní bodové ohodnocení vychází z pravidel v analytickém modulu.

Samotné skóre však nepředstavuje úplný model bezpečnosti hesla.

Například dlouhé heslo tvořené jedním opakujícím se znakem může mít příznivou délku, ale zároveň zjevnou strukturální slabinu.

Z tohoto důvodu aplikace zohledňuje také běžná hesla a sekvenční vzory.

### Důležité rozlišení

Je vhodné rozlišovat tři pojmy:

- **Délka hesla** – počet znaků, ze kterých se heslo skládá.
- **Složitost hesla** – vlastnosti jeho znakového složení.
- **Odhadnutelnost hesla** – míra, do jaké lze heslo odhadnout pomocí realistických strategií hádání.

Tyto vlastnosti spolu souvisejí, ale nejsou totožné.

## 12. Odhad entropie hesla

Entropie je jedním z pojmů používaných při hodnocení nejistoty a bezpečnosti hesel.

V kontextu hesel je však nutné rozlišovat mezi teoretickou entropií náhodně vytvořeného hesla a odhadem založeným na modelu hádání.

Projekt používá knihovnu `zxcvbn`, která vrací hodnotu `guesses_log10`.

Tato hodnota odpovídá logaritmu o základu 10 odhadovaného počtu pokusů potřebných k uhádnutí hesla podle modelu knihovny.

Převod na bitovou stupnici lze zapsat jako:

\[
H = \log_{2}(G)
\]

kde \(G\) představuje odhadovaný počet pokusů.

Protože knihovna poskytuje jeho logaritmus o základu 10, lze vztah upravit:

\[
H = \log_{10}(G)\cdot\log_{2}(10)
\]

V implementaci projektu se používá odpovídající výpočet:

```python
entropy = zxcvbn(password)["guesses_log10"] * math.log2(10)
```

Pro prázdné heslo implementace vrací hodnotu `0.0`.

### Interpretace výsledku

Vyšší hodnota znamená vyšší odhadovanou náročnost hádání v rámci použitého modelu.

Výsledek však nelze interpretovat jako přesnou fyzikální nebo matematickou míru skutečné náhodnosti libovolného hesla. Jde o odhad založený na modelu `zxcvbn`.

Odhad také automaticky neznamená konkrétní dobu potřebnou k prolomení hesla. Ta závisí mimo jiné na dostupném výpočetním výkonu, způsobu útoku, omezeních pokusů a dalších okolnostech.

## 13. Detekce běžných hesel a sekvencí

### 13.1 Běžná hesla

Běžná hesla jsou hesla, která se často používají nebo se dají snadno předvídat.

Útočníci mohou při pokusech o získání přístupu využívat seznamy známých hesel a jejich variant.

Lokální seznam v souboru `data/common_passwords.txt` umožňuje aplikaci některá taková hesla rozpoznat.

Rozsah této ochrany závisí na velikosti a aktuálnosti datového souboru.

### 13.2 Sekvenční vzory

Sekvenční vzory jsou posloupnosti znaků, jejichž pořadí je snadno předvídatelné.

Příklady zahrnují:

- Vzestupné číselné posloupnosti.
- Sestupné číselné posloupnosti.
- Posloupnosti sousedních písmen.
- Jiné jednoduché znakové vzory.

Projekt používá kontrolu sekvencí s minimální délkou čtyř znaků.

Nejde o univerzální detektor všech možných vzorů. Jeho přesné možnosti jsou omezeny implementací a použitými daty.

### 13.3 Opakování znaků

Hesla složená z jediného opakovaného znaku jsou příkladem extrémně předvídatelného vstupu.

Kontrola této vlastnosti doplňuje ostatní analytické metody a pomáhá zabránit tomu, aby byla podobná hesla hodnocena pouze na základě délky.

## 14. Automatizované testování

Testování je důležitou součástí vývoje, protože umožňuje ověřovat správnost funkcí a zachovat jejich očekávané chování při dalších úpravách.

Projekt využívá standardní modul `unittest`.

### 14.1 Struktura testů

Testy jsou rozděleny do dvou souborů:

- `tests/test_analyzer.py` – testování vlastností hesla a výsledné analýzy.
- `tests/test_entropy.py` – testování výpočtu entropie.

Toto rozdělení usnadňuje kontrolu jednotlivých částí aplikace.

### 14.2 Spuštění testů

Z kořenového adresáře projektu spusť:

```bash
python -m unittest discover -s tests -v
```

Pokud používáš existující virtuální prostředí, můžeš spustit testy přímo jeho interpretem:

```powershell
.\.venv\bin\python.exe -m unittest discover -s tests -v
```

Parametr `discover` automaticky vyhledává testy v určeném adresáři.

Parametr `-s tests` nastavuje adresář, ve kterém se testy hledají.

Parametr `-v` zapíná podrobnější výpis výsledků.

### 14.3 Co testovat

Mezi důležité testovací případy patří:

| Testovací případ | Očekávaný účel |
|---|---|
| Prázdné heslo | Ověřit správné zpracování prázdného vstupu. |
| Běžné heslo | Ověřit detekci známých slabých hesel. |
| Dlouhé heslo | Prověřit hodnocení délky. |
| Heslo s různými kategoriemi znaků | Ověřit jednotlivé kontroly znaků. |
| Heslo tvořené stejným znakem | Ověřit detekci opakování. |
| Heslo obsahující sekvenci | Ověřit detekci předvídatelných vzorů. |
| Heslo s Unicode znaky | Prověřit zpracování neanglických znaků. |
| Výpočet entropie | Ověřit číselný výsledek a chování při prázdném vstupu. |

Tabulka popisuje doporučené oblasti testování, nikoliv tvrzení, že každá varianta je již samostatně pokryta konkrétním testem.

### 14.4 Význam automatizovaných testů

Automatizované testování umožňuje:

- Rychle odhalovat chyby.
- Ověřovat výsledky po změnách kódu.
- Zajišťovat konzistentní chování analytických funkcí.
- Ověřovat hraniční případy.
- Zjednodušit další rozšiřování projektu.

## 15. Ukázky analýzy

Následující příklady ilustrují principy, na které se aplikace zaměřuje. Nejde o skutečný výpis programu ani o garantované výsledky jeho konkrétní implementace.

### Příklad 1: Běžné heslo

```text
Heslo: password
```

Možné nedostatky:

- Heslo patří mezi známé a často používané výrazy.
- Jeho struktura je snadno předvídatelná.
- Přítomnost osmi znaků sama o sobě nezaručuje bezpečnost.

Takové heslo by mělo být nahrazeno jedinečným a obtížněji odhadnutelným heslem.

### Příklad 2: Opakování znaků

```text
Heslo: aaaaaaaa
```

Možné nedostatky:

- Všechny znaky jsou stejné.
- Heslo obsahuje velmi jednoduchý vzor.
- Jeho délka neodpovídá skutečné náročnosti hádání.

Tento příklad demonstruje význam detekce opakujících se znaků.

### Příklad 3: Jednoduchá sekvence

```text
Heslo: abcd1234
```

Možné nedostatky:

- Obsahuje snadno rozpoznatelné posloupnosti.
- Kombinuje dva předvídatelné vzory.
- Samotná přítomnost písmen a číslic nezaručuje vysokou bezpečnost.

### Příklad 4: Heslo s více kategoriemi znaků

```text
Heslo: vR7!qP2#xL9@mK4
```

Tento příklad obsahuje malá a velká písmena, číslice i speciální znaky a je delší než dvanáct znaků.

Takové vlastnosti mohou přispět k dobrému výsledku analýzy. Skutečná odolnost však závisí také na tom, zda bylo heslo vytvořeno nepředvídatelným způsobem a zda není odvozeno ze známého vzoru.

### Příklad 5: Heslo s českými znaky

```text
Heslo: Žluťoučký123!
```

Tento příklad ilustruje podporu znaků Unicode.

Je však důležité rozlišovat podporu českých znaků od bezpečnosti samotného hesla. Slovo ze slovníku doplněné číslicemi a speciálním znakem nemusí být dostatečně odolné.

**Doporučení:** Pro reálné účty používej dlouhá, jedinečná hesla generovaná správcem hesel. Příklady v této dokumentaci nepoužívej jako skutečná přihlašovací hesla.

## 16. Bezpečnostní aspekty

Projekt je vzdělávací nástroj zaměřený na vybrané aspekty bezpečnosti hesel. Při jeho používání je důležité vzít v úvahu následující skutečnosti.

### 16.1 Hodnocení není zárukou bezpečnosti

Žádné jednoduché skóre nedokáže zaručit, že heslo nelze prolomit.

Výsledky představují orientační hodnocení na základě implementovaných pravidel a použitého modelu.

### 16.2 Význam délky a jedinečnosti

Dlouhá a náhodně vygenerovaná hesla mohou poskytovat výrazně lepší ochranu než krátká nebo předvídatelná hesla.

Každý účet by měl používat vlastní jedinečné heslo, aby kompromitace jednoho účtu automaticky neohrozila ostatní.

### 16.3 Ochrana vstupních údajů

Při analýze skutečných hesel je nutné dbát na jejich důvěrnost.

Hesla by neměla být zapisována do logů, veřejných výpisů nebo jiných trvale uchovávaných záznamů bez odpovídajícího důvodu a zabezpečení.

Při rozšiřování aplikace o další funkce je vhodné zachovat princip minimalizace zpracovávaných citlivých údajů.

### 16.4 Lokální zpracování

Projekt využívá lokální datové soubory pro kontrolu běžných hesel a sekvencí.

Samotná přítomnost lokálních souborů však není zárukou, že se heslo nikdy neodesílá jinam. To závisí na celém programu a jeho závislostech.

Před použitím aplikace pro citlivé vstupy je proto vhodné ověřit skutečné chování implementace.

### 16.5 Omezení datových seznamů

Seznam běžných hesel nemůže obsahovat všechny existující nebo potenciálně slabé varianty.

Nepřítomnost hesla v seznamu proto neznamená, že je heslo bezpečné.

### 16.6 Rozdíl mezi analýzou a autentizací

Aplikace slouží k analýze hesel. Sama o sobě nepředstavuje kompletní autentizační systém a nenahrazuje zabezpečené ukládání hesel, vícefaktorové ověřování ani další ochranné mechanismy.

## 17. Současná omezení

Aktuální verze projektu má několik omezení, která je vhodné zohlednit při interpretaci výsledků.

- **Pravidlové hodnocení:** Bodové skóre vychází z předem stanovených pravidel a nemusí zachytit všechny způsoby, jak lze heslo odhadnout.
- **Omezený seznam běžných hesel:** Účinnost detekce závisí na obsahu lokálního datového souboru.
- **Omezená detekce vzorů:** Kontrola sekvencí se zaměřuje na implementované vzory a nemusí rozpoznat všechny předvídatelné konstrukce.
- **Odhad entropie:** Výsledek knihovny `zxcvbn` je modelový odhad, nikoliv záruka konkrétní odolnosti.
- **Závislost na konfiguraci:** Chování aplikace závisí na správném nastavení Pythonu, dostupnosti knihovny a cest k datovým souborům.
- **Nejde o kompletní bezpečnostní audit:** Projekt se zaměřuje na vlastnosti hesel a nehodnotí celý proces autentizace ani zabezpečení konkrétního systému.

Tato omezení představují také příležitosti pro budoucí rozšíření projektu.

## 18. Možnosti budoucího rozšíření

Projekt lze dále rozvíjet v několika směrech.

### 18.1 Rozšíření analytických metod

Možná vylepšení zahrnují:

- Pokročilejší rozpoznávání sekvencí a opakujících se vzorů.
- Detekci jednoduchých obměn běžných hesel.
- Podrobnější vysvětlení jednotlivých důvodů výsledné klasifikace.
- Lepší práci s hraničními případy.

### 18.2 Vylepšení hodnocení

Další vývoj by mohl zahrnovat:

- Samostatné zobrazení všech dílčích výsledků.
- Podrobnější odůvodnění výsledného hodnocení.
- Jasné oddělení pravidlového skóre a odhadu `zxcvbn`.
- Přesnější dokumentaci jednotlivých hranic a pravidel.

### 18.3 Uživatelské rozhraní

Do budoucna lze uvažovat o:

- Grafickém uživatelském rozhraní.
- Přehlednějším výpisu výsledků.
- Vizualizaci jednotlivých vlastností hesla.
- Interaktivním vysvětlování bezpečnostních nedostatků.

### 18.4 Rozšíření testovací sady

Další testy by mohly pokrýt:

- Různé délky hesel.
- Další varianty Unicode.
- Hraniční případy sekvenčních vzorů.
- Neočekávané vstupy.
- Chybějící nebo nesprávně načtené datové soubory.
- Chování programu při změně konfigurace.

### 18.5 Dokumentace a správa projektu

Mezi další možné kroky patří:

- Doplnění souboru `requirements.txt`.
- Přidání automatické kontroly kvality kódu.
- Zavedení kontinuální integrace.
- Vytvoření dokumentace veřejných funkcí.
- Přidání licenčních informací a pravidel pro příspěvky.
- Rozšíření návodu pro instalaci v různých operačních systémech.

Uvedené body představují návrhy pro budoucí vývoj, nikoliv funkce, které by již byly součástí aktuální implementace.

## 19. Vzdělávací přínos projektu

Projekt propojuje několik oblastí programování a kybernetické bezpečnosti.

### Programování v Pythonu

Práce na projektu zahrnuje návrh funkcí, práci s řetězci, podmínkami, datovými soubory a externími knihovnami.

### Návrh modulární aplikace

Rozdělení aplikace na hlavní vstupní soubor, analytický modul, testy a datové soubory usnadňuje orientaci v kódu a jeho další rozšiřování.

### Základy kybernetické bezpečnosti

Projekt demonstruje význam nepředvídatelnosti hesel, rozpoznávání běžných vzorů a omezení jednoduchých pravidel pro hodnocení bezpečnosti.

### Testování softwaru

Použití `unittest` ukazuje, jak automatizovaně ověřovat funkčnost aplikace a snižovat riziko regresních chyb.

### Práce s externí knihovnou

Integrace `zxcvbn` představuje příklad využití existující knihovny k doplnění vlastní analytické logiky.

### Kritické vyhodnocování výsledků

Důležitou součástí projektu je také pochopení toho, že výsledek bezpečnostního nástroje závisí na použitých metodách, datech a předpokladech.

## 20. Licence

Licence projektu zatím není v této dokumentaci určena.

Pokud bude projekt zveřejněn nebo dále distribuován, je vhodné zvolit odpovídající licenci a ověřit licenční podmínky použitých knihoven a datových souborů.

---

**Password Security Analyzer** je vzdělávací projekt zaměřený na praktickou analýzu síly hesel, detekci vybraných bezpečnostních nedostatků a demonstraci základních principů kybernetické bezpečnosti.
