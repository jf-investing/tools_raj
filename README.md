# tools_raj — aplikacja korzystająca z Allegro REST API

To repozytorium zawiera wyłącznie opis aplikacji. Kod jest prywatny.

User-Agent: `tools_raj/<wersja> (+https://github.com/jf-investing/tools_raj)`

Właściciel: J&F Investing sp. z o.o. Kontakt: https://jfinvesting.pl

## Czym jest

Aplikacja obsługuje dwa moduły wewnętrznego panelu narzędzi firmy J&F Investing:

- **System zgłoszeń** — dla działu obsługi klienta: zbiera wiadomości od kupujących z Allegro w jednym
  miejscu, obok wiadomości z innych kanałów sprzedaży.
- **Scraper** — monitoring ocen: regularnie zbiera oceny naszych ofert i oceny naszego konta
  sprzedawcy, żeby zespół szybko widział negatywne opinie. Wyłącznie odczyt.

Aplikacja działa wyłącznie na **kontach sprzedawcy należących do J&F Investing**: aromatycznyraj,
jfinvesting, gwiazdoholik i aromaholik. Nie obsługuje sprzedawców spoza firmy, nie jest udostępniana na
zewnątrz i nie loguje się do niej nikt spoza firmy.

## Jak korzysta z API Allegro

System zgłoszeń:

| Obszar | Do czego |
|---|---|
| Wiadomości (`/messaging/threads`, `/messaging/message-attachments`) | cykliczny odczyt nowych wątków i wiadomości, pobieranie załączników, wysyłanie odpowiedzi |
| Oferty (`/sale/product-offers`) | odczyt oferty, której dotyczy wiadomość, żeby pracownik widział kontekst |
| Konto (`/me`) | sprawdzenie, do którego konta należy token |

Scraper (wyłącznie odczyt):

| Obszar | Do czego |
|---|---|
| Oferty (`/sale/offers`, `/sale/product-offers`, `/sale/products`) | lista naszych ofert i produktów, do których należą |
| Oceny ofert (`/sale/offers/{offerId}/rating`) | średnia i liczba ocen każdej oferty |
| Oceny konta (`/sale/user-ratings`) | oceny wystawione naszemu kontu przez kupujących |
| Konto (`/me`) | login konta, do linku do jego publicznej strony ocen |

## Autoryzacja

Device Flow (OAuth 2.0). Dla każdego konta pracownik firmy raz potwierdza dostęp, logując się na to
konto Allegro. Tokeny są przechowywane w konfiguracji panelu narzędzi, dostępnej tylko administratorom.

## Zgodność z regulaminem REST API

- Każde zapytanie niesie nagłówek User-Agent w formacie wymaganym przez Allegro (powyżej).
- Dane kupujących służą wyłącznie do odpowiadania na ich wiadomości i do przeglądu ocen naszych ofert
  i konta. Nie są przekazywane poza firmę.
