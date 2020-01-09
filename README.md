Celem zadania jest stworzenie systemu do zarządzania dyżurami kelnerów w sieci restauracji.

# Widoki: 

1. lista restauracji:  tabelka - nazwa, adres, imię i nazwisko managera

2. Lista pracowników: tabelka - imię i nazwisko, telefon

3. Lista dyżurów dla wybranej restauracji:  nazwa restauracji, wybór daty, tabelka imię i nazwisko pracownika, liczba godzin

4. Dodaj nowego pracownika -> formularz do edycji danych + walidacja

5. Dodaj nową restaurację -> formularz do edycji danych + walidacja

6. Dodaj dyżur -> wybór restauracji, wybór pracownika, pola do edycji daty i liczby godzin

7. Lista płac -> podsumowanie wypłat dla każdego pracownika z wybranego miesiąca - wybór roku i miesiąca, poniżej tabelka: imię i nazwisko, wypłata (liczba przepracowanych godzin * stawka) 

## Pracownik
    Id
	Imię
	Nazwisko
	Telefon
	Data zatrudnienia
	Stanowisko - Manager/Kelner - enum 
	Stawka za godzinę
	
##### Walidacja:
	wszystkie pola wypełnione
	Imię, Nazwisko z dużej litery, dopuszczalne znaki a-z, A-Z,  myślnik, apostrof 
	Data w formacie yyyy-MM-dd
	stawka > 0

## Restauracja
    Id
    Nazwa
    Manager (Pracownik)
    Adres
    	Ulica
    	Nr domu
    	Miasto
    	Kod pocztowy
    	
    Adres w osobnej klasie, ale w tej samej tabeli w bazie

##### Walidacja
	wszystkie pola wypełnione 
	Kod w formacie XX-XXX 
		

## Dyżur:
	Pracownik
	Restauracja
	Data
	Liczba godzin
	
##### Walidacja
	wszystkie pola wypełnione 
	data w formacie yyyy-MM-dd 
	Nie można przypisać pracownika 2x na ten sam dzień 


# Etap I
1. Widoki w JSP
2. Testy jednostkowe walidatorów
3. Bean jednego z walidatorów dodany w XML, nie przez adnotacje
5. W tym etapie brak bazy danych (wszystko w pamięci aplikacji)
4. Przy starcie aplikacji trochę danych jest już uzupełnionych, np. 3 pracowników, 2 restauracje, 5 dużyrów

# Etap II - Dodanie bazy danych 
1. Dodanie konfiguracji jdbc
2. Lokalna baza postgres
3. 	podmiana repository z inMemory na hibernate

# Etap III - Dodanie Spring Security 
1.	Dodanie logowania - wystarczy inMemoryAuthentication(), 3 użytkowników: Właściciel, Manager, Pracownik 
2.	Zabezpieczenie dostępów do URLi:
-	lista restauracji - bez logowania
-	lista dyżurów, lista pracowników - zalogowany użytkownik (dowolny) 
-	dodanie nowego pracownika, dodanie dyżuru - manager, właściciel
-	dodanie nowej restauracji - właściciel
-	lista płac - właściciel 
 
# Etap IV - Liquibase
1. Dodanie biblioteki do projektu
2. Konfiguracja
3. Wykonanie jakiejś zmiany na bazie, np. dodanie pracownika, zmiana nazwy kolumny, dodanie kolumny (już bez zmian w widoku itd, sam liquibase)
 
 # Etap V - Quartz
1. Konfiguracja
1. Utworzenie zadania cyklicznego, które koniec dnia wygeneruje dla każdej restaruracji zmiany na następny dzień (np. losowo dwóch pracowników na restaurację). 
 
 
 
 
 
 
 
 
 
