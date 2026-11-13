# HopsKids — wdrożenie SEO

Stan wyjściowy (sprawdzony 4.08.2026): strona działa poprawnie, ale **nie ma jej w indeksie Google**.
Brakuje `robots.txt` i `sitemap.xml` (oba zwracają 404), nie ma danych strukturalnych, nie ma linków
prowadzących do domeny. Google nie ma jak jej odkryć.

---

## Krok 1 — pliki na serwerze ✅ ZROBIONE

> Ten krok jest już wykonany w repozytorium. Strona wdraża się z GitHub Pages, więc pliki
> nie idą przez FTP — trafiają na serwer przy `git push`. Zawartość `head-seo.html` została
> wklejona do `<head>` w `index.html`, a stare zdublowane znaczniki `og:` usunięte.
> Poniższa tabela zostaje jako opis, co który plik robi.

Wszystkie trzy pliki trafiają do **katalogu głównego** strony (tam, gdzie leży `index.html`):

| Plik | Gdzie | Co robi |
|---|---|---|
| `robots.txt` | katalog główny | mówi robotom, że mogą wchodzić, i wskazuje sitemapę |
| `sitemap.xml` | katalog główny | lista adresów do zindeksowania + zdjęcia |
| `head-seo.html` | **nie wgrywasz** — kopiujesz zawartość do `<head>` w `index.html` | canonical, poprawione Open Graph, dane strukturalne |

**Ważne przy `head-seo.html`:** przed wklejeniem usuń ze swojego `<head>` stare znaczniki
`og:title`, `og:description`, `og:image`, `og:type`, `og:locale` — inaczej będą zdublowane.

Sprawdzenie po wgraniu — te dwa adresy muszą otwierać treść, a nie pustą stronę:

- https://hopskids.pl/robots.txt
- https://hopskids.pl/sitemap.xml

---

## Krok 2 — Google Search Console (to jest ten krok, który realnie odpala indeksowanie)

1. Wejdź na https://search.google.com/search-console
2. Dodaj zasób typu **Domena** → `hopskids.pl`
3. Potwierdź własność rekordem TXT w DNS (panel firmy, u której masz domenę)
4. Menu **Mapy witryny** → wpisz `sitemap.xml` → Prześlij
5. Pasek **Sprawdzenie adresu URL** u góry → wklej `https://hopskids.pl/` → **Poproś o zindeksowanie**

Czas do pojawienia się w wynikach: zwykle **3 dni – 2 tygodnie**. Wcześniej `site:` będzie pusty i to normalne.

**Sprawdź też od razu:** w raporcie „Indeksowanie stron" zobaczysz, czy hosting nie wysyła nagłówka
`X-Robots-Tag: noindex`. Niektóre hostingi mają to włączone domyślnie na nowych kontach i z zewnątrz
tego nie widać.

---

## Krok 3 — Wizytówka Google (dla bawialni ważniejsza niż sama strona)

https://business.google.com — rodzice z Wrocławia szukają przez Mapy, nie przez wyszukiwarkę.

Uzupełnij komplet: kategoria „Centrum zabaw dla dzieci" + dodatkowa „Kawiarnia", adres, godziny
(te same co na stronie!), telefon, **adres strony `https://hopskids.pl/`**, min. 10 zdjęć
wnętrza. Weryfikacja idzie pocztą lub filmikiem — potrafi zająć 1–2 tygodnie, więc warto zacząć teraz.

Dane kontaktowe muszą być **identyczne** na stronie, w wizytówce, na Facebooku i Instagramie
(ten sam zapis telefonu, ten sam zapis adresu). Google porównuje je między sobą.

---

## Krok 4 — linki do domeny (bez tego Google długo nie znajdzie strony)

- Instagram → bio → link do strony
- Facebook → Informacje → Witryna
- Katalogi lokalne: Panorama Firm, PKT.pl, Zumi, Baza Firm
- Portale wrocławskie (lokalne serwisy miejskie, grupy FB dla rodziców) — nawet jedna wzmianka z linkiem pomaga
- Jeśli macie znajomych z firmami we Wrocławiu — wzajemna wzmianka na stronie działa

---

## Krok 5 — co dalej, gdy strona już będzie w indeksie

Największe ograniczenie: strona jest **jednostronicowa**, wszystko na kotwicach `#`. Google
zaindeksuje ją jako **jeden adres**, więc konkuruje tylko o jedno zapytanie naraz.

Rozbicie na osobne podstrony to najmocniejsza rzecz, jaką można zrobić dla SEO tej strony:

| Podstrona | Na jakie zapytanie łapie |
|---|---|
| `/urodzinki/` | „urodziny dla dziecka Wrocław", „sala urodzinowa Wrocław" |
| `/cennik/` | „bawialnia Wrocław cennik" |
| `/wynajem-sali/` | „sala do wynajęcia Wrocław" |
| `/warsztaty/` | „zajęcia dla dzieci Wrocław" |
| `/kawiarnia/` | „kawiarnia z kącikiem dla dzieci Wrocław" |

Każda podstrona = własny `<title>`, własny opis, 300+ słów treści. Po dodaniu dopisz je do
`sitemap.xml` (na dole pliku jest przygotowany komentarz z gotowym wzorem).

Drobiazgi warte poprawy przy okazji:

- **Blog / aktualności** — nawet 1 wpis miesięcznie („Co robić z dzieckiem we Wrocławiu, gdy pada")
  daje Google powód, żeby wracać na stronę
- **Zdjęcia** — przekonwertuj `.jpg` na WebP, teraz ładują się wolniej niż mogłyby; szybkość
  to czynnik rankingowy
- **Nazwy plików zdjęć** są już dobre (`malpi-gaj.jpg`, `basen-kulek.jpg`) — tak trzymać
- **Teksty alternatywne** obrazków też są uzupełnione — to rzadkość, dobra robota

---

## Weryfikacja po wdrożeniu

| Co sprawdzić | Gdzie |
|---|---|
| Czy dane strukturalne są poprawne | https://search.google.com/test/rich-results |
| Czy schema nie ma błędów | https://validator.schema.org/ |
| Czy podgląd linku na FB działa | https://developers.facebook.com/tools/debug/ |
| Szybkość i Core Web Vitals | https://pagespeed.web.dev/ |
| Czy strona jest już w indeksie | wpisz w Google: `site:hopskids.pl` |
