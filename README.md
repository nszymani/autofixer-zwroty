# autofixer-zwroty
projekt na zajęcia
# Projekt: Automatyzacja weryfikacji zwrotów B2B (Autofixer.com)

### 1. Charakterystyka firmy i opis problemu
Autofixer.com to sklep e-commerce sprzedający części samochodowe, które zamawia u zewnętrznych dostawców (hurtowni). Każdy dostawca ma inny limit czasu na przyjęcie zwrotu (np. 14 lub 30 dni). 

Obecnie pracownik magazynu, mając przed sobą paczkę zwrotną, widzi tylko numer zamówienia – na tej podstawie nie wie od razu, z jakiej hurtowni pochodzi część ani czy termin zwrotu jeszcze obowiązuje. Ręczne przeszukiwanie systemu ERP i liczenie dni w kalendarzu zajmuje czas i prowadzi do przekraczania terminów zwrotów do dostawców, co z kolei powoduje straty finansowe i odkładanie się niesprzedanego towaru na magazynie.

### 2. Plan i sposób rozwiązania problemu (MVP)
Rozwiązaniem problemu jest prosty program działający w wierszu poleceń (konsoli cmd), który działa w oparciu o dwie tabele danych i automatyzuje proces decyzyjny:
* *Tabela dostawców (suppliers.json):* baza hurtowni z przypisanymi limitami dni na zwrot.
* *Tabela zamówień (orders.json):* baza łącząca numer zamówienia z konkretnym dostawcą i datą zakupu.

*Działanie programu krok po kroku:*
1. Po uruchomieniu w konsoli program wczytuje dane i wyświetla czytelną tabelę wszystkich dostawców wraz z ich limitami dni na zwrot.
2. Pracownik wpisuje z klawiatury numer zamówienia znajdujący się na paczce (np. AF-1005).
3. Program szuka zamówienia w tabeli, przypisuje je do konkretnego dostawcy i automatycznie wylicza, ile dni upłynęło od daty zakupu do dnia dzisiejszego.
4. Następuje automatyczna decyzja systemu: 
   * *Gdy termin jest zachowany:* Program informuje, że zwrot jest możliwy, symuluje wysyłkę powiadomienia przez API dostawcy i zapisuje gotowy plik dokumentu ZWROT_DOSTAWCA_[numer].txt.
   * *Gdy termin minął:* Program informuje o przekroczeniu limitu dni i generuje dokument przyjęcia na magazyn własny PRZYJECIE_MAGAZYN_WLASNY_[numer].txt.
