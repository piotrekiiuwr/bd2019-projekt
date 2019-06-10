Specyfikacja projektu do przedmiotu BD2019 prowadzonego w Instytucie Informatyki UWr znajduje się w pliku https://github.com/piotrekiiuwr/bd2019-projekt/blob/master/projekt.md

# Testy
W katalogu `testy` umieściłem przykładowe testy (z opisu projektu). Zachęcam Was do wrzucania tam swoich własnych testów oraz wyników zwracanych przez Wasze implementacje. Będę akceptował pull-requesty bez dokladniejszej weryfikacji. Proszę o przestrzegania konwencji dotyczącej nazw - nazwa pliku z testem do uruchomienia z parametrem `--init` powinna zawierać słowo `init`, nazwa pliku z testem powinna pasować do `*.in.json`, plik z odpowiedzią na test powinien mieć tę samą nazwę co test i pasować do `*.out.json`. W przypadku gdyby ktoś wygenerował więcej testów proszę o wrzucenie ich w osobnym podkatalogu.  

# Zgłaszanie uwag do projektu zakończone

Specyfikacja projektu nie będzie już zmieniana (za wyjątkiem sytuacji, gdy taka zmiana będzie bezwzględnie konieczna).

Osoby, które pracowały nad specyfikacją projektu proszę o maila do mnie  z podaniem swojego imienia i nazwiska oraz loginu na githubie.

# Informacja o projekcie

Projekty należy przygotować indywidualnie.

Co będzie oceniane?

Model konceptualny - powinien składać się z diagramu E-R oraz komentarza zawierającego więzy pominięte w diagramie, powinien zawierać opis uprawnień użytkowników init i app. Komentarz powinien dodatkowo zawierać zwięzłą informację w jaki sposób zostaną zaimplementowane poszczególne funkcje API **(termin: 30 maja, wysłanie poprzez zadanie na skosie, ocena: waga 20%)**

Model fizyczny - powinien być plikiem sql nadającym się do czytania (i oceny) przez człowieka. Powinien zawierać definicję wszystkich tabel, więzów, indeksów, kluczy, akcji referencyjnych, funkcji, perspektyw i wyzwalaczy, a także użytkownika app z odpowiednimi uprawnieniami. Nie jest niezbędne wykorzystanie wszystkich tych udogodnień, ale tam, gdzie pasują, powinny być wykorzystywane. **(ocena łącznie z programem)**

Dokumentacja projektu - ma się składać z pojedynczego pliku pdf zawierającego ostateczny model konceptualny oraz dokładne instrukcje, jak należy aplikację uruchomić. Dokumentacja ma dotyczyć tego, co jest zaimplementowane; w szczególności, nie można oddać samej dokumentacji, bez projektu. **(ocena łącznie z programem)**

Program - oceniany będzie kod źródłowy oraz poprawność i efektywność działania. **(ocena: waga 80%, łącznie z modelem fizycznym i dokumentacją)**

Oddajemy archiwum zawierające wszystkie pliki źródłowe programu, ostateczną wersję modelu konceptualny oraz dokumentację w pliku pdf, model fizyczny w pliku sql oraz polecenie typu make (ew. skrypt run.sh, itp.) umożliwiające kompilację i uruchomienie systemu - archiwum należy przesłać poprzez polecenie w systemie skos.


# Zasady, na których do 19 maja można było zgłaszać uwagi do projektu

Ogłaszam możliwość otrzymania punktów bonusowych za zgłaszane uwagi do projektu. Uwagi zgłaszamy w postaci pull-requesta do mojego repozytorium na githubie lub jako issue jeśli problem jest bardziej skomplikowany i znalezienie rozwiązania wymaga uzgodnienia.

Za uwagi, które wg mojej subiektywnej opinii będą pomocne oferuję bonus do 10% maksa z teorii/sql/projektu (wg wyboru studenta - wybór proszę dospecyfikować w opisie pull - requesta/issue w postaci pojedynczej linii (ostatniej we wpisie) zawierającej jedną z opcji: teoria/sql/projekt).

Dokładna wysokość bonusa zależy od wagi korygowanego problemu oraz terminu zgłoszenia (im szybciej tym łatwiej będzie mi daną uwagę uwzględnić). Bonus będzie przyznawany łącznie za wszystkie uwagi zgłoszone do dnia 19 maja włącznie (limit 10% dotyczy łącznie wszystkich uwag zgłoszonych przez pojedynczego studenta, punkty może dostać  pierwsza osoba zgłaszająca dany problem i pierwsza proponująca sensowną wersję rozwiązania).

Jak używać git-a oraz github-a można nauczyć się tutaj: https://guides.github.com/
W szczególności należy zapoznać się z poradnikami: 
* https://guides.github.com/introduction/git-handbook/
* https://guides.github.com/activities/forking/
