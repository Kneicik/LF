# Program do sterowania wieloma robotami typu line follower

## Założenia
Aplikacja napisana w Pythonie, która umożliwia komunikację z robotem typu "line follower" poprzez protokół UDP. Użytkownik może kontrolować robota i wysyłać do niego różne parametry za pomocą interfejsu graficznego stworzonego przy użyciu biblioteki Tkinter.

## Działanie

#### Tworzenie globalnego socketu UDP

Program tworzy globalne gniazdo UDP, które będzie używane do odbierania wiadomości. Gniazdo jest wiązane z adresem 0.0.0.0 (oznaczającym nasłuchiwanie na wszystkich interfejsach sieciowych) i portem 5005.

#### Sprawdzanie poprawności wpisanego adresu IP

Funkcja ta sprawdza, czy podany adres IP jest poprawny (czy składa się z czterech oktetów w zakresie 0-255).

#### Obsługa wysyłania danych

Funkcja która przyjmuje dwa argumenty: messege oraz robot_udp_ip i wysyła podaną wiadomość w ASCII przez UDP do odpowiedniego robota

#### Odbieranie pakietów UDP

Funkcja, która korzysta z globalnego socketu UDP do odbierania pakietów i filtrowania ich.

Kolejność działania:
- Sprawdzanie czy pakiet zaczyna się od aliasu, któregoś z robotów
- Jeżeli alias istnieje sprawdzane są filtry oczekujące konkretnych wiadomości
- Jeżeli istnieją przekazywane są do odpowiedniego obiektu Tkinter
- Jeżeli nie istnieją zostają pominięte

#### Wysyłanie parametrów

Jako, że program współpracuje z już wcześniej zaprojektowanym standardem komunikacji ta funkcja formatuje dane tak aby program na robocie je rozumiał i mógł modyfikować parametry

#### Interfejs Tkinter

Funkcja start_application uruchamia osobny wątek i socket dla wysyłania danych do robota oraz tworzy okno z interfejsem gdzie znajdują się przyciski do obsługi robota i okna wyświtlające dane z czujników, pozycje lini oraz prametry regulatora PID i maksymalne prędkości silników.

#### Okno wprowadziania danych identyfikacyjnych robota

Na początku program tworzy okno gdzie wprowadzany jest adres IP robota i jego alias po czym tworzy okno.

## Pomysły na przyszłość
- Automatyczne wyszukiwanie robotów w sieci bądź wpisywanie samego aliasu i szukanie adresu robota automatycznie,
- Szyfrowanie danych w celu zabezpieczenia komunikacji
- Wypełnianie okienek do wpisywania parametrów po wciśnięciu przycisku "Request parameters",
- Stworzenie standardu obsługi dowolnego robota,

## Program robota współpracujący z projektem
https://github.com/Kneicik/Line_followerV0

Należy zmienić port do wysyłania ramek w robocie na 5005 zamiast 1234:

  if(udp.listen(5005)) {
      Serial.print("UDP Listening on IP: ");
      Serial.println(WiFi.localIP());
  }