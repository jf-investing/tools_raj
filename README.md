# tools_raj — aplikacja korzystająca z Allegro REST API

To repozytorium zawiera wyłącznie opis aplikacji. Kod jest prywatny.

User-Agent: `tools_raj/<wersja> (+https://github.com/jf-investing/tools_raj)`

Właściciel: J&F Investing sp. z o.o. Kontakt: https://jfinvesting.pl

## Czym jest

System zgłoszeń działający w wewnętrznym panelu narzędzi firmy J&F Investing. Służy działowi obsługi
klienta: zbiera wiadomości od kupujących z Allegro w jednym miejscu, obok wiadomości z innych kanałów
sprzedaży.

Aplikacja działa wyłącznie na **kontach sprzedawcy należących do J&F Investing**: aromatycznyraj,
jfinvesting, gwiazdoholik i aromaholik. Nie obsługuje sprzedawców spoza firmy, nie jest udostępniana na
zewnątrz i nie loguje się do niej nikt spoza firmy.

## Jak korzysta z API Allegro

| Obszar | Do czego |
|---|---|
| Wiadomości (`/messaging/threads`, `/messaging/message-attachments`) | cykliczny odczyt nowych wątków i wiadomości, pobieranie załączników, wysyłanie odpowiedzi |
| Oferty (`/sale/product-offers`) | odczyt oferty, której dotyczy wiadomość, żeby pracownik widział kontekst |
| Konto (`/me`) | sprawdzenie, do którego konta należy token |

## Autoryzacja

Device Flow (OAuth 2.0). Dla każdego konta pracownik firmy raz potwierdza dostęp, logując się na to
konto Allegro. Tokeny są przechowywane w konfiguracji panelu narzędzi, dostępnej tylko administratorom.

## Zgodność z regulaminem REST API

- Każde zapytanie niesie nagłówek User-Agent w formacie wymaganym przez Allegro (powyżej).
- Dane kupujących służą wyłącznie do odpowiadania na ich wiadomości.
