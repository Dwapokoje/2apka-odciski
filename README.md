# Odciski rejestru 2apki

To repozytorium jest publiczną „pieczęcią czasu” dla rejestru w aplikacji
2apka (Dwa Pokoje sp. z o.o.). Nie zawiera żadnych danych rodzin ani treści
— wyłącznie jeden krótki plik na dzień.

## Czym jest odcisk (skrót)

Odcisk (inaczej skrót, po angielsku „hash”) to ciąg 64 znaków wyliczony
z zawartości rejestru za jeden dzień. Działa jak odcisk palca: ta sama
zawartość zawsze daje ten sam odcisk, a zmiana choćby jednej kropki daje
zupełnie inny. Z odcisku nie da się odtworzyć żadnej treści.

Co noc aplikacja zamyka miniony dzień i wylicza jego odcisk. Odcisk każdego
dnia uwzględnia odcisk dnia poprzedniego, więc dni tworzą łańcuch: zmiana
czegokolwiek wstecz zmieniłaby odciski wszystkich następnych dni. Plik dnia
trafia tutaj, a GitHub zapisuje, kiedy to się stało. Tego zapisu nie da się
po cichu przerobić — ani u nas, ani u nikogo innego.

## Co zawiera plik dnia

Plik `odciski/RRRR/MM/RRRR-MM-DD.txt` ma cztery linie:

    data: 2026-11-04
    ogniwo: <odcisk tego dnia>
    poprzednie: <odcisk poprzedniego dnia; w pierwszym pliku: poczatek lancucha>
    liczba ogniw: <numer kolejny dnia w łańcuchu>

## Po co to jest

Jeśli raport z 2apki trafia do sądu, druga strona może zapytać, czy rejestr
nie został zmieniony po fakcie. Odcisk opublikowany tutaj zaraz po zamknięciu
dnia jest niezależnym świadectwem: pokazuje, że rejestr z tego dnia miał
wtedy taki, a nie inny stan.

## Jak to sprawdzić

**Krok 1 — czy łańcuch jest ciągły i opublikowany w terminie (może to zrobić
każdy, bez żadnych narzędzi).**

1. Otwórz plik dla dnia, który Cię interesuje, oraz plik dnia następnego.
2. Sprawdź, że linia „poprzednie” w pliku następnego dnia jest identyczna
   z linią „ogniwo” w pliku dnia wcześniejszego.
3. Sprawdź, że numery „liczba ogniw” rosną o 1, a w kolejnych dniach nie
   brakuje żadnego pliku.
4. Kliknij „History” przy pliku — GitHub pokaże, kiedy plik dodano.
   Ta data jest zapisana przez GitHub, nie przez 2apkę.

**Krok 2 — czy raport zgadza się z zapisanym odciskiem (wykonuje operator lub
biegły).** Odcisk dnia liczy się z zawartości bazy rejestru, której z
zewnątrz nie widać, dlatego nie da się go przeliczyć samemu z pliku PDF.
Na wniosek strony operator uruchamia program weryfikujący
(`scripts/sprawdz_lancuch.py`), który porównuje dzisiejszy stan rejestru z
każdym zapamiętanym odciskiem i podaje wynik: zgodne / wyjaśnione / do oceny /
niezgodne. Wynik „zgodne” dla dnia wpisu oznacza, że wpisy z tego dnia są
takie same, jak w chwili zapieczętowania. Zapytanie: pomoc@dwapokoje.app.

**Mam raport PDF z 2apki — jak go powiązać z odciskiem.**

1. W stopce każdej strony raportu stoi zdanie: „Rejestr do DD.MM.RRRR
   zabezpieczony ogniwem nr N, skrót …”. Na ostatniej stronie raportu
   („Odcisk rejestru”) jest pełny skrót (64 znaki) i nazwa pliku dnia.
2. Otwórz w tym repozytorium plik dnia z raportu:
   `odciski/RRRR/MM/RRRR-MM-DD.txt` (ta sama data, co w stopce).
3. Porównaj: linia „ogniwo” w pliku ma być identyczna z pełnym skrótem
   z ostatniej strony raportu (pierwsze 16 znaków — ze skrótem w stopce),
   a linia „liczba ogniw” — z numerem ogniwa N.
4. Kliknij „History” przy pliku: data dodania pliku pokazuje, kiedy ten
   stan rejestru został utrwalony poza 2apką.

Zgodność oznacza, że raport powołuje się na ten sam, publicznie utrwalony
stan rejestru do tego dnia. Wpisy z dni późniejszych niż data w stopce
obejmują odciski następnych dni. Gdy raport mówi „Rejestr nie był jeszcze
zabezpieczony odciskiem.”, raport powstał, zanim pierwszy odcisk trafił do
tego repozytorium — i nie ma pliku do porównania.

Sam plik tekstowy z odciskiem można też zweryfikować jako dokument, np.
poleceniem `sha256sum odciski/2026/11/2026-11-04.txt` — pozwala to
udowodnić, że kopia pliku przedstawiona w sprawie jest identyczna z tą z
repozytorium.

## Czego odcisk NIE dowodzi

- Nie dowodzi, że treść wpisu jest prawdziwa — tylko że po zapieczętowaniu
  dnia nie została zmieniona.
- Nie obejmuje czasu sprzed pierwszego pliku w tym repozytorium; pierwszy
  odcisk pieczętuje stan rejestru od tej chwili i nie działa wstecz.
- Nie obejmuje bieżącego dnia — odcisk powstaje po zamknięciu dnia (około
  dwóch godzin po północy czasu polskiego).
- Nie wskazuje, kto i o której godzinie dokonał wpisu — to pokazuje sam
  raport.
- Nie pokazuje danych żadnej rodziny; brak pliku dla dnia oznacza przerwę w
  publikacji (np. awarię), a nie brak wpisów.
