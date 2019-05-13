Zasady przyznawania punktów bonusowych: https://github.com/piotrekiiuwr/bd2019-projekt/blob/master/README.md
Basic-writing-and-formatting-syntax: https://help.github.com/en/articles/basic-writing-and-formatting-syntax

# Projekt: System Zarządzania Partią Polityczną.

Twoim zadaniem jest zaimplementowanie zdefiniowanego poniżej API.

Ze względu na to, że interesuje nas przede wszystkim tematyka baz danych kolejne wywołania funkcji API należy wczytywać ze standardowego wejścia.

## Opis problemu

Partia prowadzi rejestr działań rządowych i samorządowych, które wspiera lub przeciw którym protestuje.

Członkowie partii mogą proponować akcje, głosować za i przeciw ich prowadzeniu, a także przesyłać materiały (nagrania, sprawozdania) z odbytych akcji.

Członkiem partii zostaje się poprzez aktywny udział w jej życiu. Po roku nieaktywności, rozumianej jako brak wywołań funkcji API autoryzowanych danymi danej osoby, traci się prawa członka partii, a takie konto jest trwale zamrażane (tzn. dany członek nie może wykonać żadnej czynności, ale wszystkie informacje na jego temat są dalej przechowywane i raportowane).

Partią zarządza zespół liderów (będących członkami partii).

## Technologie

System Linux. Język programowania dowolny – wybór wymaga zatwierdzenia przez prowadzącego pracownię - zalecany język python. Baza danych – PostgreSQL w wersji >=9.5. Testy będą przeprowadzane na komputerze z Ubuntu 18.04, PostgreSQL 10.7 .

Twój program po uruchomieniu powinien przeczytać ze standardowego wejścia ciąg wywołań funkcji API, a wyniki ich działania wypisać na standardowe wyjście.

Wszystkie dane powinny być przechowywane w bazie danych, efekt działania każdej funkcji modyfikującej bazę, dla której wypisano potwierdzenie wykonania (wartość OK) powinien być utrwalony. Program będzie uruchamiany wielokrotnie z następującymi parametrami:

- pierwsze uruchomienie - program wywołany z parametrem --init -

Wejście zawiera w pierwszym wierszu wywołanie funkcji open z następującymi danymi login: init, password: qwerty, w kolejnych wierszach wywołania funkcji leader.

Można założyć, że przed uruchomieniem z parametrem --init baza nie zawiera jakichkolwiek tabel.

- kolejne uruchomienia - wejście zawiera w pierwszym wierszu wywołanie funkcji open z następującymi danymi login: app, password: qwerty, a następnie wywołania dowolnych funkcji API za wyjątkiem funkcji open i leader.

Przy pierwszym uruchomieniu program powinien utworzyć wszystkie niezbędne elementy bazy danych (tabele, więzy, funkcje wyzwalacze, użytkownik app z odpowiednimi uprawnieniami) zgodnie z przygotowanym przez studenta modelem fizycznym. Baza nie będzie modyfikowana pomiędzy kolejnymi uruchomieniami. Program nie będzie miał praw do tworzenia i zapisywania jakichkolwiek plików. Program będzie mógł czytać pliki z bieżącego katalogu (np. dołączony do rozwiązania studenta plik sql zawierający polecenia tworzące bazę).

Baza danych oraz użytkownik init będą istnieli w momencie pierwszego uruchomienia bazy, należy utworzyć użytkownika app, nadać mu odpowiednie uprawnienia i hasło (moduł pgcrypto będzie dostępny). Hasła należy przechowywać w bezpieczny sposób.


## Format pliku wejściowego

Każda linia pliku wejściowego zawiera obiekt JSON (http://www.json.org/json-pl.html). Każdy z obiektów opisuje wywołanie jednej funkcji API wraz z argumentami.

Przykład: obiekt
```
{ "leader": { "password": "abcde", "member": 1}} 
```
oznacza wywołanie funkcji o nazwie leader z argumentem password przyjmującym wartość "abcde" oraz member – wartość 1.

W pierwszej linii wejścia znajduje się wywołanie funkcji open z argumentami umożliwiającymi nawiązanie połączenia z bazą danych.


## Format wyjścia

Dla każdego wywołania wypisz w osobnej linii obiekt JSON zawierający status wykonania funkcji OK/ERROR oraz tabelę data zawierającą wynik działania tej funkcji wg specyfikacji.

Format zwracanych danych (dla czytelności zawiera zakazane znaki nowej linii):

Obiekt z polami: status, data (tylko dla funkcji zwracających krotki), oraz ew. pole debug. Wartość status to OK/ERROR. Tabela data zawiera wszystkie krotki wynikowe. Każda krotka to tabela zawierająca wartości wszystkich jej atrybutów w kolejności podanej w specyfikacji. Dopuszczalna jest dodatkowa para o kluczu debug i wartości typu string z ew. informacją przydatną w debugowaniu (jest ona całkowicie dobrowolna i będzie ignorowana w czasie testowania, powinna mieć niewielki rozmiar).


###### Przykładowe wejście i wyjście

Pierwsze uruchomienie (z parametrem `--init`):
```
{ "open": { "database": "student", "login": "init", "password": "qwerty"}}
{ "leader": { "password": "abc", "member": 1}}
{ "leader": { "password": "asd", "member": 2}}
```

###### Oczekiwane wyjście
```
{"status": "OK"}
{"status": "OK"}
{"status": "OK"}
```

###### Kolejne uruchomienie:
```
{ "open": { "database": "student", "login": "app", "password": "qwerty"}}
{ "protest": { "timestamp": 1557475700, "password": "123", "member": 3, "action":500, "project":5000, "authority":10000}}
{ "support": { "timestamp": 1557475701, "password": "123", "member": 3, "action":600, "project":5000}}
{ "upvote": { "timestamp": 1557475702, "password": "asd", "member": 2, "action":500}}
{ "downvote": { "timestamp": 1557475703, "password": "abc", "member": 1, "action":500}}
{ "downvote": { "timestamp": 1557475704, "password": "abc", "member": 1, "action":600}}
{ "votes": { "timestamp": 1557475705, "password": "abc", "member": 1}}
{ "trolls": { }}
```

###### Oczekiwane wyjście (dla czytelności zawiera znaki nowej linii, pierwsza linia powtarza się 6 razy)
```
{"status": "OK"}
...
{"status": "OK",
  "data": [ [ 1, 0, 2],
         [ 2, 1, 0],
	          [ 3, 0, 0] 
        ]
}
{"status": "OK",
  "data": [ [ 3, 1, 2,"true"] ]
}
```
## Format opisu API
```
<function> <arg1> <arg2> … <argn> // nazwa funkcji oraz nazwy jej argumentów
```
opis działania funkcji

// opis formatu wyniku: lista atrybutów wynikowych tabeli data


## Nawiązywanie połączenia i definiowanie liderów

Każde z poniższych wywołań powinno zwrócić obiekt JSON zawierający status wykonania OK/ERROR.

###### open

```
open <database> <login> <password>
```
przekazuje dane umożliwiające podłączenie Twojego programu do bazy - nazwę bazy, login oraz hasło, wywoływane dokładnie jeden raz, w pierwszej linii wejścia

// zwraca status OK/ERROR w zależności od tego czy udało się nawiązać połączenie z bazą

###### leader

```
leader <password> <member>
```
tworzy nowego członka partii, który będzie jej liderem o unikalnym identyfikatorze `<member>` z hasłem `<password>`

// zwraca status OK/ERROR

## Wywołania API

Każde z poniższych wywołań powinno zwrócić obiekt JSON zawierający status wykonania OK/ERROR, oraz ew. tabelę data zawierającą kolejne krotki wyniku wg specyfikacji poniżej.

Jeśli zapytanie jest autoryzowane danymi członka pozbawionego praw to jest zgłaszany błąd.

Identyfikatory `<member> <action> <project> <authority>` są typu number i są globalnie unikalne (np. nie zdarzy się, że wartość `<member>` jest równa wartości `<authority>`)

Wartość `<password>` jest typu string, jej długość nie przekracza 128 znaków.

Wartość `<timestamp>` jest typu number i reprezentuje UNIX timestamp. Gwarantowane jest, że wszyskie wywołania będą podane na wejściu w kolejności rosnących timestampów.

Argumenty funkcji w nawiasach [ ] są opcjonalne (tzn. nie muszą być podane w wywołaniu funkcji).


## Lista funkcji API

###### support protest

```
support <timestamp> <member> <passwd> <action> <project> [ <authority> ]

protest <timestamp> <member> <passwd> <action> <project> [ <authority> ]
```

Dodawanie nowej akcji `<action>` wsparcia (support) lub sprzeciwu (protest) wobec działania `<project>` prowadzonego przez organ władzy `<authority>`. 
* Jeśli `<member>` jest członkiem partii to `<passwd>` musi być jego hasłem, w przeciwnym razie dodawany jest nowy członek o podanym id i haśle, jeśli id jest zajęte (pozbawienie praw) to jest zgłaszany błąd. 
* Jeśli `<project>` jest działaniem dodanym wcześniej to wartość `<authority>` jest ignorowana, wpp `<authority>` musi być podana.

// zwraca status OK/ERROR, nie zwraca atrybutu data

###### upvote downvote

```
upvote <timestamp> <member> <passwd> <action> 

downvote <timestamp> <member> <passwd> <action> 
```

Członek `<member>` głosuje za (upvote) albo przeciw (downvote) przeprowadzeniu akcji `<action>`.

Można głosować co najwyżej jeden raz w sprawie każdej akcji.

Jeśli `<member>` jest członkiem partii to `<passwd>` musi być jego hasłem, w przeciwnym razie dodawany jest nowy członek o podanym id i haśle, jeśli id jest zajęte (pozbawienie praw) to jest zgłaszany błąd.

// zwraca status OK/ERROR, nie zwraca data

###### actions
```
actions <timestamp> <member> <passwd> [ <type> ] [ <project> | <authority> ] 
```

Zwraca listę wszystkich akcji wraz z typem, id projektu, id organu władzy oraz z liczbami głosów za i przeciw akcji z następującymi zastrzeżeniami:

* jeśli podano `<type>` w postaci tekstu „support” albo „protest” należy ograniczyć się do akcji podanego typu,
* jeśli podano `<project>` należy ograniczyć się do akcji dotyczących danego <project>,
* jeśli podano `<authority>` należy ograniczyć się do akcji dotyczących działań danego <authority>.

`<passwd>` to hasło członka `<member>` będącego liderem.

Atrybuty zwracanych krotek, krotki muszą być posortowane wg `<action>` rosnąco
```
// <action> <type> <project> <authority> <upvotes> <downvotes>
```

###### projects

```
projects <timestamp> <member> <passwd> [ authority ]
```

Zwraca listę wszystkich działań wraz z id organu władzy prowadzącego dane działanie, przy czym 
* jeśli `<authority>` jest podane to zwraca wyłącznie akcje dotyczące działań danego <authority
`<passwd>` to hasło członka `<member>` będącego liderem.

Atrybuty zwracanych krotek, krotki muszą być posortowane wg `<project>` rosnąco
```
// <project> <authority> <actions>
```

###### votes

```
votes <timestamp> <member> <passwd> [ <action> | <project> ]
```

Zwraca listę wszystkich członków, którzy oddawali głosy wraz z sumarycznymi liczbami głosów za i przeciw.
* Jeśli podano `<action>` to wynik powinien ograniczyć się do głosów dotyczących akcji `<action>`
* Jeśli podano `<project>` to wynik powinien ograniczyć się do głosów dotyczących akcji związanych z projektem `<project>`

`<passwd>` to hasło członka `<member>` będącego liderem.

Atrybuty zwracanych krotek, krotki muszą być posortowane wg `<member>` rosnąco
```
// <member> <upvotes> <downvotes>
```

###### trolls

```
trolls (funkcja bez parametrów)
```

Zwraca listę wszystkich użytkowników, którzy zaproponowali akcje mające w tej chwili sumarycznie więcej downvotes niż upvotes. Z wstępnych badań wynika, że ranking trolli będzie bardzo często używaną funkcją, zaprojektuj bazę tak aby ta funkcja działała szybko.

Atrybuty zwracanych krotek, krotki muszą być posortowane wg wartości różnicy `<downvotes> - <upvotes>` malejąco, w drugiej kolejności wg `<member>` rosnąco, atrybut `<active>` to wartość "true"/"false" w zależności od tego czy dany członek zachowuje prawa członka.
```
// <member> <upvotes> <downvotes> <active>
```


