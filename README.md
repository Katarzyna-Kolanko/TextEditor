Prosty edytor tekstu w OpenGL (pygame +
PyOpenGL)
1. Cel i opis projektu
Projekt to samodzielny edytor tekstu/kodu napisany w Pythonie, w którym cała warstwa graficzna (okno, tekst,
kursor, pasek narzędzi, scrollbar) jest rysowana ręcznie przy użyciu OpenGL, a pygame odpowiada za okno,
zdarzenia klawiatury/myszy oraz renderowanie tekstu do tekstur.

2. Wymagania i uruchomienie
Wymagane biblioteki:
pip install pygame PyOpenGL PyOpenGL_accelerate
Uruchomienie (opcjonalnie ze ścieżką do pliku do otwarcia):
python texteditor.py [ścieżka_do_pliku]

3. Architektura kodu
Kod jest podzielony na kilka logicznych części:
• highlight_line() i wyrażenie regularne TOKEN_REGEX – proste kolorowanie składni: słowa kluczowe,
wbudowane funkcje/nazwy, stringi, komentarze, liczby i operatory otrzymują osobne kolory.
• Funkcje pomocnicze OpenGL (surface_to_texture, draw_texture, draw_rect, point_in_rect) – konwertują
powierzchnie pygame na tekstury OpenGL i rysują proste prostokąty/tekstury na ekranie.
• Klasa Editor – centralny obiekt trzymający cały stan aplikacji: zawartość dokumentu (lista linii self.lines),
pozycję kursora, zaznaczenie, przewinięcie, czcionkę i jej rozmiar, tryb wyszukiwania oraz pamięć podręczną
tekstur (cache czcionek i wyrenderowanych linii, dla wydajności).
• render() i handle_toolbar_click() – rysują całą klatkę (pasek narzędzi, numery linii, tekst, zaznaczenie, kursor,
scrollbar, pasek wyszukiwania) i obsługują kliknięcia w przyciski paska narzędzi.
• main() – pętla główna programu: inicjalizacja okna OpenGL, odczyt zdarzeń pygame (klawiatura, mysz, kółko
myszy, zmiana rozmiaru okna) i wywoływanie odpowiednich metod klasy Editor.

4. Funkcjonalności
• Kolorowanie składni w stylu Pythona.
• Edycja tekstu: wpisywanie, Backspace/Delete, Enter, Tab.
• Zaznaczanie: myszą, klawiaturą (Shift + strzałki), Ctrl+A
• Zaznaczanie blokowe (kolumnowe) – Alt + przeciąganie myszą, przydatne np. do edycji wielu linii naraz.
• Kopiuj / wytnij / wklej – korzysta ze schowka systemowego przez tkinter, jeśli jest dostępny.
• Wyszukiwanie w tekście – Ctrl+F otwiera pasek wyszukiwania; Enter – następne dopasowanie, Shift+Enter –
poprzednie, Esc – zamknięcie.
• Przewijanie dokumentu – kółkiem myszy, klawiszami Page Up/Page Down lub przeciąganiem suwaka po
prawej stronie.
• Zmiana czcionki i jej rozmiaru z poziomu paska narzędzi na górze okna.
• Numerowanie linii po lewej stronie edytora.
• Zapis pliku (Ctrl+S lub przycisk „Zapisz”).
