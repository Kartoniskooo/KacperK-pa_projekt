# Szczegółowe przypadki użycia
## System Interaktywnego Symulatora Układu Słonecznego

### 1. Wyszukaj i wybierz ciało niebieskie
* **Aktor główny:** Użytkownik  
* **Cel:** Odnalezienie w bazie danych i zaznaczenie na mapie orbitalnej konkretnej planety lub księżyca w celu poznania szczegółów.

* **Warunki wstępne:**
    * Użytkownik uruchomił aplikację (widoczne jest okno graficzne z poruszającymi się orbitami).
    * Baza danych SQLite została pomyślnie załadowana.

* **Warunki końcowe (sukces):**
    * System graficznie wyróżnia wybraną planetę (np. biała obwódka) i ładuje jej parametry do bocznego panelu encyklopedii.

* **Główny przebieg zdarzeń:**
    1. Użytkownik przegląda mapę i klika myszką w poruszający się obiekt graficzny (planetę).
    2. System pobiera współrzędne kliknięcia myszy.
    3. System weryfikuje matematycznie odległość kursora od środków planet w celu wykrycia kolizji.
    4. System wysyła zapytanie SQL do lokalnej bazy danych o rekord powiązany z wybraną planetą.
    5. System odczytuje dane: nazwa, masa, grawitacja, ciekawostka.
    6. System renderuje pobrane dane tekstowe na bocznym panelu UI.

* **Przebiegi alternatywne:**
    * **3a.** Kliknięcie w pustą przestrzeń – system nie podejmuje akcji, dotychczas zaznaczona planeta pozostaje aktywna.
    * **5a.** Brak szczegółowych danych w bazie – system wyświetla nazwę obiektu, a w polach parametrów wpisuje komunikat „Brak danych historycznych w bazie”.

* **Przebiegi wyjątkowe:**
    * **E1.** Błąd odczytu pliku bazy SQLite – system wyświetla w panelu bocznym komunikat o błędzie krytycznym bazy danych i ładuje domyślne wartości awaryjne zapisane w kodzie.

---

### 2. Oblicz kosmiczną wagę (Kalkulator)
* **Aktor główny:** Użytkownik  
* **Cel:** Przeliczenie ziemskiej masy użytkownika na jego wagę na powierzchni wybranego ciała niebieskiego.

* **Warunki wstępne:**
    * Dowolne ciało niebieskie jest aktualnie wybrane i wyświetlane w panelu encyklopedii.
    * Pole tekstowe/przyciski wagi są aktywne.

* **Warunki końcowe (sukces):**
    * System dynamicznie oblicza i wyświetla nową wartość w kilogramach.

* **Główny przebieg zdarzeń:**
    1. Użytkownik klika przyciski `[+5]` lub `[-5]` na panelu, aby ustawić swoją masę na Ziemi.
    2. System rejestruje zmianę wartości wejściowej.
    3. System pobiera z bazy danych wartość przyspieszenia grawitacyjnego planety.
    4. System wykonuje algorytm matematyczny: Waga = Masa * (g_planety / 9.81).
    5. System wyświetla zaktualizowany wynik w dolnej sekcji panelu UI.
