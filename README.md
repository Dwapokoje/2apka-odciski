# Odciski rejestru 2apki

To repozytorium jest publiczną „pieczęcią czasu” dla rejestru w aplikacji
2apka (Dwa Pokoje sp. z o.o.). Nie zawiera żadnych danych rodzin ani treści
— wyłącznie jeden krótki plik na dzień.

## Czym jest odcisk

Co noc aplikacja zamyka dzień i wylicza z zapisanych w nim wpisów jeden
ciąg znaków (odcisk), podobny do cyfrowego zapisu „jak wyglądał rejestr tego
dnia”. Kolejny odcisk zawiera w sobie poprzedni, więc tworzą łańcuch: zmiana
czegokolwiek wstecz zmieniłaby wszystkie następne. Plik dnia trafia tutaj,
a GitHub zapisuje, kiedy to się stało — nie da się tego potem po cichu
przerobić ani u nas, ani u nikogo innego.

Plik `odciski/RRRR/MM/RRRR-MM-DD.txt` ma cztery linie: data, odcisk dnia,
odcisk poprzedniego dnia, numer kolejny.

## Po co to jest

Jeśli raport z 2apki trafia do sądu, druga strona może zapytać, czy rejestr
nie został zmieniony po fakcie. Odcisk opublikowany tutaj w dniu zapisu jest
na to niezależnym świadectwem: pokazuje, że dany stan rejestru istniał już
wtedy, gdy powstał ten plik.

## Jak sprawdzić raport

1. W raporcie PDF znajdź datę wpisu, który Cię interesuje.
2. Otwórz tutaj plik dla tej daty (i kilku następnych dni).
3. Porównaj: odcisk poprzedniego dnia w pliku z kolejnego dnia musi być taki sam
   jak odcisk tego dnia — łańcuch jest ciągły i nie ma w nim luk ani zmian.
4. Pełną weryfikację (zestawienie raportu z odciskiem) wykonuje na wniosek
   wnioskodawcy biegły lub operator aplikacji; w razie potrzeby napisz na
   pomoc@dwapokoje.app.

Odcisk dowodzi, że rejestr nie został zmieniony po dniu zapisu. Nie
potwierdza prawdziwości samej treści wpisów.
