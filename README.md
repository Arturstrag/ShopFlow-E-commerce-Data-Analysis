# ShopFlow – E-commerce Data Analysis

## 🎯 Cel projektu

Celem projektu była analiza danych sprzedażowych sklepu internetowego **ShopFlow** oraz przygotowanie danych do wiarygodnej analizy biznesowej.

Projekt obejmował:
- identyfikację i naprawę problemów jakości danych,
- analizę sprzedaży,
- analizę klientów i produktów,
- analizę sezonowości,
- analizę stanów magazynowych.

---

## 🗂️ Dane

- **Źródło:** symulowane dane sklepu internetowego ShopFlow
- **Liczba rekordów:** ok. 85 000
- **Liczba tabel:** 5
- **Zakres czasowy:** 24 miesiące
- **Format:** relacyjna baza danych PostgreSQL

### Główne obszary danych:
- klienci,
- produkty,
- zamówienia,
- pozycje zamówień,
- stany magazynowe.

---

## 🔧 Narzędzia i technologie

- **PostgreSQL** – czyszczenie, transformacja i analiza danych
- **SQL** – tworzenie zapytań analitycznych
- **DBeaver** – praca z bazą danych
- **Microsoft Excel** – analiza i prezentacja wyników
- **Copilot** – wsparcie przy tworzeniu i optymalizacji zapytań

---

## Kontekst biznesowy
Kontekst biznesowy
ShopFlow Sp. z o.o.- sklep internetowy działający na polskim rynku e-commerce od 2021 roku.
- ~40 tys.
zarejestrowanych klientów
- 2 000
produktów w katalogu
- 20 000
zamówień (12 mies., próbka)
- 187 zł
średnia wartość koszyka (AOV)

| Parametr | Wartość |
|-----------|----------|
| Branża | E-commerce – moda, dom i wnętrza, elektronika użytkowa, uroda |
| Rynek | Polska (dostawy krajowe, brak jeszcze ekspansji zagranicznej) |
| Model biznesowy | B2C, sprzedaż wyłącznie online (własny sklep + integracja z Allegro) |
| Liczba klientów w bazie | ok. 5 000 aktywnych kont (dane do warsztatu – w rzeczywistości ShopFlow ma ok. 38 000 zarejestrowanych klientów, warsztat pracuje na próbce) |
| Liczba zamówień | ok. 20 000 (12 miesięcy wstecz, próbka reprezentatywna) |
| Liczba produktów w katalogu | ok. 2 000 SKU w 8 kategoriach |
| Średnia wartość koszyka (AOV) | 187 zł |
| Zespół | 34 osoby: e-commerce, marketing, logistyka, obsługa klienta, 1-osobowy zespół analityczny (do niedawna 0-osobowy) |
| Siedziba i magazyn | Poznań |

## 🚨 Główne wyzwania biznesowe

ShopFlow zmaga się z kilkoma kluczowymi problemami biznesowymi, które ograniczają dalszy wzrost firmy:

1. Rosnący koszt pozyskania klienta. Koszt pozyskania klienta (CAC) wzrósł o **34% rok do roku**, a dział marketingu nie posiada jednoznacznej informacji, które kanały marketingowe generują najbardziej wartościowych klientów.
2. Niska retencja klientów
Według założeń biznesowych jedynie około **22% klientów** składa drugie zamówienie w ciągu 6 miesięcy od pierwszego zakupu.
3. Problemy z zarządzaniem zapasami. Najpopularniejsze produkty są regularnie niedostępne w magazynie, co prowadzi do utraty części sprzedaży. Jednocześnie część asortymentu zalega przez wiele miesięcy, generując dodatkowe koszty magazynowania.
4. Brak przejrzystości rentowności
Firma nie przeprowadziła dotychczas kompleksowej analizy marżowości poszczególnych kategorii produktowych, co utrudnia podejmowanie decyzji cenowych i zakupowych.
5. Niespójność danych między działami
Marketing, sprzedaż i logistyka korzystają z różnych raportów i wskaźników, przez co podejmowane decyzje często opierają się na odmiennych interpretacjach danych.
6. CAC (Customer Acquisition Cost)** – średni koszt pozyskania jednego nowego klienta.
7. Retencja – odsetek klientów powracających na kolejny zakup.
   
## 📝 Proces analizy

### 1. Przygotowanie danych

Przed rozpoczęciem właściwej analizy przeprowadzono kompleksową kontrolę jakości danych we wszystkich tabelach. Proces obejmował identyfikację oraz obsługę problemów, które mogły wpływać na wiarygodność wyników analizy.

W ramach przygotowania danych:

* usunięto i scalono duplikaty przy zachowaniu powiązanej historii danych,
* obsłużono braki danych oraz wartości wymagające dodatkowej weryfikacji,
* ujednolicono formaty dat, numerów telefonów, adresów e-mail oraz danych tekstowych,
* poprawiono literówki i niespójne nazwy kategorii oraz lokalizacji,
* zidentyfikowano błędne i nietypowe wartości,
* wykryto wartości odstające z wykorzystaniem metody IQR,
* naprawiono wybrane problemy z integralnością danych pomiędzy tabelami,
* zachowano historyczne rekordy w przypadkach, w których ich usunięcie mogłoby prowadzić do utraty istotnych informacji.

Dzięki temu przygotowano spójny i uporządkowany zbiór danych, który mógł zostać wykorzystany w dalszej analizie. Proces oczyszczania danych został przeprowadzony za pomocą **PostgreSQL** i **SQL** i znajduje się w osobnym projekcie https://github.com/Arturstrag/ShopFlow-E-commerce-Projekt-oczyszczenia-danych


### 2. Analiza biznesowa 
Przeprowadzono kompleksową analizę biznesową danych e-commerce, obejmującą sprzedaż i rentowność kategorii, retencję i aktywację klientów, efektywność kanałów marketingowych, sezonowość sprzedaży, zachowania zakupowe, zwroty, program lojalnościowy oraz zarządzanie zapasami. Analiza pozwoliła zidentyfikować kluczowe obszary wymagające działań biznesowych, m.in. niską marżowość Elektroniki, problem z aktywacją nowych klientów, brak mierzalnego efektu programu lojalnościowego oraz jednoczesne niedobory i nadmiary magazynowe. Analizę biznesową przeprowadzono w **Microsoft Excel** wraz z **Copilotem**. Pełna analiza biznesowa znajduje się w pliku analysis.md. Poniżej przedstawiono odpowiedzi na najważniejsze problemy sklepu ShopFlow: 

1. **Które kategorie generują największy przychód?** 

![Przychód wg kategorii](images/Przychód_wg_kategorii.png)

```excel
=SUMIFS(order_items!$G$2:$G$48646;order_items!$H$2:$H$48646;A7)
```

![Przychód wg kategorii – wykres](images/Przychód_wg_kategorii_wykres.png)

**Obserwacja:** Kategoria Elektronika generuje najwyższy przychód: **10 447 785,11 zł**, czyli **38%** przychodu ujętego w zestawieniu. Łączny przychód ośmiu kategorii wynosi **27 738 887,20 zł**. Najniższy wynik ma kategoria Akcesoria: **727 558,10 zł**.

**Rekomendacja:**  Należy priorytetyzować Elektronikę w budżecie marketingowym i 
eksponować ją na stronie głównej sklepu. Należy też monitorować to razem z marżą, a nie tylko z samym przychodem.

2. **Które kategorie mają najwyższą marżę procentową, a które  najniższą?**

![Marża procentowa według kategorii](images/Marża_procentowa_wg_kategorii.png)

**Obserwacja:** Elektronika - kategoria generująca najwyższy przychód - ma 
jednocześnie najniższą marżę ze wszystkich kategorii, o **10+** punktów 
procentowych poniżej średniej. Akcesoria mają odwrotny profil: niski **przychód**, ale 
najwyższą **marżę**. 

**Rekomendacja:** Należy zestawić tabele przychodu według kategorii i marży procentowej w jednej tabeli dla zarządu - Elektronika i Akcesoria to skrajne, ale uzupełniające się przypadki. 
Rozważyć podniesienie widoczności Akcesoriów jako produktów dodatkowych przy 
zakupie elektroniki (cross-sell), co podniosłoby łączną marżę koszyka bez utraty 
wolumenu głównej kategorii. 

3. **Które produkty mają wysoką sprzedaż, ale niską marżę?**
    
![Produkty o niskiej marży procentowej](images/Niska_marża_procentowa.png)

**Obserwacja:** Wszystkie 10 produktów o wysokiej sprzedaży i niskiej marży to 
Elektronika - potwierdza to i pogłębia wniosek z **Pytania 2** na poziomie konkretnych 
SKU. Co ważniejsze: ich realna marża **(13,7–16,6%)** jest wyraźnie niższa niż średnia katalogowa marża Elektroniki **(35,4%, patrz Pytanie 2)** - te konkretne produkty są 
sprzedawane z rabatami, które dodatkowo zjadają i tak już najniższą marżę wśród wszystkich kategorii produktowych. 

**Rekomendacja:** Zacząć renegocjację cen zakupu od tych konkretnych, 
zidentyfikowanych 10 produktów - to najszybszy sposób na poprawę marży bez ryzyka utraty wolumenu w całej kategorii. Dodatkowo: sprawdzić politykę rabatową dla tych konkretnych SKU - być może są rutynowo obejmowane promocjami, które 
nie powinny na nie obowiązywać, skoro już wyjściowo mają niską marżę katalogową.

4. **Jacy klienci wracają najczęściej (drugi zakup)?**  
   
![Retencja klientów – wariant 1](images/retencja_klientów_1.png)

**Ogółem:** **44,0%** klientów, którzy zrealizowali chociaż jeden zakup (nie licząc 
anulowanych), robi drugi zakup w ciągu 90 dni. 

**Obserwacja:** To wciąż dwukrotnie więcej niż zakładał zarząd **(22% retencji)**. Różnice 
między kanałami są umiarkowane **(44,5-47,8 punktu procentowego)**, rozstęp około 4 punktów procentowych. Kanał pozyskania ma niewielki, ale zauważalny wpływ na szansę powrotu 
(**Meta Ads i Influencer najwyżej, Newsletter najniżej)**. Prawdziwym problemem nie 
jest to, że klienci nie wracają - tylko to, że część w ogóle nie robi pierwszego zakupu. 

**Rekomendacja:** Zarząd powinien przeformułować cel z "podnieść retencję z **22% do 
30%"** na dokładniejszy: "podnieść aktywację (odsetek zarejestrowanych klientów, 
którzy w ogóle kupują)" - to jest metryka, która faktycznie ma miejsce do poprawy. 
Dodatkowo: skoro Newsletter ma najniższą retencję spośród kanałów, a 
jednocześnie nie wyróżnia się wysokim LTV, warto zapytać 
marketing, czy baza **61 000** subskrybentów jest odpowiednio segmentowana.

5. **Jakie produkty są zagrożone brakiem w magazynie w najbliższym 
miesiącu?** 

![Najniższy stan magazynowy](images/Najniższy_stan_magazynowy.png)

**Wynik:** **434** aktywne produkty (ok. **22%** całego katalogu) mają stan magazynowy 
na poziomie progu zamówienia lub poniżej niego, w tym 15+ produktów z zerowym 
stanem, np. "Organ Moda Eco", "Dziadek Uroda Basic", "Warzywo akcesoria". 

**Obserwacja:** Skala problemu (**22%** katalogu) jest dużo większa, niż sugerowałaby 
anegdota zarządu ("część produktów notorycznie brakuje"). To nie jest problem 
pojedynczych SKU - to problem systemowy w procesie uzupełniania zapasów.

**Rekomendacja:** Priorytetyzować automatyczne alerty reorderowe (próg już istnieje 
jako reorder_level - brakuje tylko automatyzacji akcji) zamiast ręcznego monitoringu. 
Zacząć od produktów z zerowym stanem i wysoką historyczną sprzedażą.

6. **Który kanał marketingowy generuje klientów o najwyższym LTV?** 

![LTV](images/LTV.png)

**Obserwacja:** Różnice są zaskakująco małe **(6 496-6 990 zł, rozstęp ~7%)** - żaden 
kanał nie "wygrywa" dramatycznie. Meta Ads generuje najwięcej klientów w liczbach 
bezwzględnych, ale ma środkowy LTV, nie najwyższy - mimo że pochłania 
największy budżet (**42%** wydatków marketingowych)

**Rekomendacja:** Skoro LTV na klienta jest podobny między kanałami, decyzję o 
alokacji budżetu oprzeć na koszcie pozyskania klienta (CAC) per kanał, a nie na LTV - to następny raport, który trzeba zestawić (dane o koszcie kampanii nie są w obecnym zbiorze ShopFlow, ale warto to zaznaczyć jako świadomą lukę, a nie 
przeoczenie). 

7.  **Ilu klientów robi zakupy tylko raz i nigdy nie wraca?** 

![Klienci z jednym zakupem](images/klienci_z_jednym_zakupem.png)

**Obserwacja:** To jest prawdziwy problem retencyjny ShopFlow - nie **"22%** wraca", 
tylko **15,8%** zarejestrowanych klientów nigdy nawet nie zaczęło kupować. Wśród 
tych, którzy raz kupili, zdecydowana większość **(94,4%)** wraca kiedykolwiek - więc 
historia "klienci nie wracają" jest błędna, ale historia "duża część zarejestrowanych 
nigdy nie kupuje" jest prawdziwa i istotna.

**Rekomendacja:** Priorytet numer jeden dla CRM: kampania aktywacyjna (nie 
retencyjna!) skierowana do **791** zarejestrowanych klientów bez żadnego 
zrealizowanego zakupu - np. rabat powitalny z ograniczonym czasem. To 
bezpośrednio odpowiada na piąty cel zarządu ("wdrożyć kulturę decyzji opartych na 
danych") - pokazuje, że dane prowadzą do innego wniosku niż intuicja. 

8. **Czy członkowie programu lojalnościowego kupują częściej i 
więcej?**

![Lojalność klientów](images/Lojalność_klientów.png)

**Obserwacja:** Brak mierzalnej różnicy - członkowie programu lojalnościowego 
zachowują się statystycznie tak samo jak pozostali klienci, a nawet nieznacznie 
gorzej na wszystkich trzech metrykach. To zaprzecza założeniu, że program 
lojalnościowy działa.

**Rekomendacja:** To jest najważniejszy pojedynczy wniosek do zakomunikowania 
zarządowi w kontekście programu ShopFlow Club (uruchomionego 8 miesięcy temu - 
być może efekt jeszcze się nie zmaterializował, ale warto to zbadać teraz, a nie za 
rok). Zaproponować: 
- sprawdzenie tych samych metryk tylko dla klientów 
zarejestrowanych w programie od 3+ miesięcy, żeby wykluczyć efekt "za wcześnie 
na wyniki", 
- jeśli różnica nadal nie wystąpi, zrewidować mechanikę programu przed dalszą inwestycją w jego rozwój.

9.  **Które produkty mają najdłuższy czas "zalegania" na magazynie?** 

![Zaleganie na magazynie](images/zaleganie_na_magazywnie.png)

**Wynik:** **830** produktów (ponad **40%** katalogu) ma stan magazynowy powyżej **500** sztuk. Top przykłady: "Dziewięć Moda Premium" (**1 999** szt. w magazynie, 
sprzedanych tylko **27** szt.), "Szwedzki Moda Pro" (**1 997** szt., sprzedanych **34** szt.). 

**Obserwacja:** Skala zalegania jest bardzo duża - **40%** katalogu ma stan magazynowy 
nieproporcjonalny do realnej sprzedaży. To spójne z narracją biznesową ("inne 
produkty zalegają miesiącami"), ale skala (**40%**, nie "kilka produktów") jest większa, 
niż sugerowałaby anegdota. 

**Rekomendacja:** Wprowadzić regularny raport "rotacja zapasów" (stan / sprzedaż 
miesięczna) jako stały element pracy zespołu zakupowego, z automatycznym 
oznaczaniem produktów poniżej progu rotacji do wyprzedaży lub wycofania z oferty. 



## 💡Podsumowanie
Analiza danych sklepu internetowego ShopFlow pozwoliła zweryfikować kluczowe założenia biznesowe oraz wskazać obszary wymagające dalszej optymalizacji. Przed rozpoczęciem analizy przeprowadzono kompleksowe oczyszczenie i ujednolicenie danych, dzięki czemu wszystkie wnioski zostały oparte na spójnym i wiarygodnym zbiorze informacji.

Najważniejsze wnioski z analizy wskazują, że:

1. Problem ShopFlow nie dotyczy retencji, lecz aktywacji klientów.
 Analiza wykazała, że 94,4% klientów dokonujących pierwszego zakupu wraca po kolejne zamówienia, natomiast 15,8% zarejestrowanych użytkowników nigdy nie dokonuje zakupu. Sugeruje to, że działania biznesowe powinny koncentrować się na zwiększaniu aktywacji nowych klientów, a nie na poprawie retencji.

2. Elektronika jest strategiczną, ale wymagającą kategorią.
 Kategoria generuje najwyższy przychód, jednak jednocześnie osiąga najniższą marżę oraz najwyższy udział zwrotów. Wskazuje to na potrzebę odrębnej strategii obejmującej politykę cenową, promocje, dobór asortymentu oraz kontrolę jakości produktów.

3. Program lojalnościowy nie wykazuje obecnie mierzalnego wpływu na zachowania klientów.
 Po ośmiu miesiącach funkcjonowania uczestnicy programu nie osiągają lepszych wyników pod względem częstotliwości zakupów ani wartości klienta. Przed dalszymi inwestycjami warto przeprowadzić szczegółową ocenę skuteczności programu i zweryfikować jego założenia.

4. Zarządzanie zapasami wymaga optymalizacji procesu prognozowania popytu.
 Analiza wykazała, że 22% produktów jest zagrożonych brakiem w magazynie, podczas gdy 40% katalogu wykazuje nadmierne stany magazynowe. Współwystępowanie niedoborów i nadwyżek sugeruje problem systemowy związany z planowaniem zakupów i uzupełnianiem zapasów.

5. Ocena kanałów marketingowych powinna uwzględniać jakość pozyskiwanych klientów.
 Choć Meta Ads odpowiada za największy wolumen nowych klientów, generowany przez ten kanał poziom LTV nie jest najwyższy. Oznacza to, że decyzje budżetowe powinny opierać się nie tylko na liczbie pozyskanych klientów, lecz również na ich długoterminowej wartości dla firmy.

