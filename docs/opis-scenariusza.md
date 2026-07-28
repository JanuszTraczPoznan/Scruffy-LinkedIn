# Opis scenariusza Make

## Cel scenariusza

Scenariusz automatycznie przygotowuje krótki komiks ze Scruffym na podstawie aktualnej wiadomości, zapisuje wygenerowaną grafikę na Google Drive i publikuje gotowy post na LinkedInie.

## Przebieg automatyzacji

### 1. Rozpoczęcie scenariusza

Pierwszy moduł uruchamia cały proces. Scenariusz może działać zgodnie z harmonogramem ustawionym w Make.

### 2. Wyszukanie wiadomości i przygotowanie wpisu

Google Gemini AI wyszukuje jedną ciekawą wiadomość z ostatnich 24 godzin.

Wiadomość powinna dotyczyć technologii, biznesu albo nietypowego wydarzenia społecznego. Pomijane są wojny, morderstwa i katastrofy.

Na podstawie znalezionej wiadomości Gemini przygotowuje krótki, ironiczny tekst w języku polskim, napisany w stylu Scruffy’ego. Gotowy wpis może mieć maksymalnie trzy zdania.

Używany model:

`gemini-2.5-flash`

### 3. Przygotowanie opisu grafiki

Drugi moduł Google Gemini AI zamienia znalezioną wiadomość w szczegółowy opis pojedynczego kadru komiksowego.

Opis określa między innymi:

* sytuację przedstawioną na ilustracji,
* wygląd i zachowanie Scruffy’ego,
* humorystyczną reakcję bohatera,
* styl nowoczesnego komiksu internetowego,
* zakaz umieszczania napisów i dymków na grafice.

Używany model:

`gemini-3.1-flash-lite`

### 4. Wygenerowanie grafiki

Kolejny moduł Google Gemini AI tworzy kwadratową ilustrację na podstawie przygotowanego opisu.

Grafika ma proporcje `1:1`, komiksowy styl, wyraźne kontury i nie powinna zawierać napisów ani dymków dialogowych.

Używany model:

`gemini-3.1-flash-image`

### 5. Zapis grafiki na Google Drive

Wygenerowana grafika jest przesyłana do wskazanego folderu na Google Drive.

W publicznym blueprincie identyfikator prywatnego folderu został zastąpiony oznaczeniem:

`GOOGLE_DRIVE_FOLDER_ID`

Osoba importująca blueprint musi wskazać własny folder Google Drive i utworzyć własne połączenie z kontem Google.

### 6. Publikacja na LinkedInie

Ostatni moduł publikuje na LinkedInie:

* wygenerowaną grafikę,
* nagłówek „Co dziś na to Scruffy”,
* krótki tekst przygotowany przez Gemini.

Post jest kierowany do głównego kanału i ma ustawioną widoczność publiczną.

Osoba korzystająca z blueprintu musi podłączyć własne konto LinkedIn.

## Obsługa błędów

Przy module wyszukującym wiadomość działa mechanizm `Retry`.

Jeżeli podczas wykonania wystąpi przejściowy błąd, Make może ponowić próbę wykonania modułu zamiast natychmiast zatrzymywać cały scenariusz.

## Wymagane połączenia

Do uruchomienia scenariusza potrzebne są własne połączenia z usługami:

* Google Gemini AI,
* Google Drive,
* LinkedIn.

Oczyszczony blueprint nie zawiera aktywnych danych dostępowych ani prywatnych identyfikatorów połączeń.

## Import blueprintu

Oczyszczony plik scenariusza znajduje się w repozytorium pod ścieżką:

`Make/publikacja-komiksow-scruffy-sanitized.json`

Po zaimportowaniu pliku do Make należy:

1. utworzyć lub wybrać własne połączenie z Google Gemini AI,
2. utworzyć lub wybrać własne połączenie z Google Drive,
3. wskazać własny folder zapisu grafik,
4. utworzyć lub wybrać własne połączenie z LinkedInem,
5. sprawdzić ustawienia harmonogramu,
6. wykonać test przed włączeniem automatycznej publikacji.

## Ważna informacja

Moduł LinkedIn publikuje post publicznie. Przed pierwszym uruchomieniem należy wykonać kontrolowany test i sprawdzić wygenerowany tekst oraz grafikę.
