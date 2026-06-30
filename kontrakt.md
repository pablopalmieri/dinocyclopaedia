# DINOCYCLOPEDIA — Kontrakt Projektowy

> Dokument roboczy. Aktualizować przy każdej istotnej zmianie ustaleń.  
> Wersja: 1.0 | Data: 2026-06-30

---

## 1. Cel projektu

Stworzenie drukowanego albumu przyrodniczego w formacie **A4** zawierającego opisy wymyślonych dinozaurów. Każdy gatunek zajmuje **rozkładówkę dwustronicową** (lewa + prawa strona A4). Docelowo strony będą drukowane i zbindowane w książkę.

---

## 2. Nastrój i styl

| Wymiar | Wzorzec |
|---|---|
| Wizualny | Klasyczne atlasy XIX/XX w. — Audubon, Larousse |
| Narracyjny | Pseudo-naukowy, naturalistyczny — David Attenborough |
| Humor | Subtelne mrugnięcie okiem — Addams Family |
| Makabra | Łagodna, nie infantylna — akcenty, nie dominanta |
| Adresat | Dorosły i dziecko jednocześnie |

**Hasło przewodnie:** *Pseudo-naukowy atlas przyrodniczy z przymrużeniem oka — Addams Family meets David Attenborough.*

Styl pisarski: pseudo-naukowy, z humorem, ale NIE infantylny. Subtelna makabra dozwolona, szczególnie w sekcji "Zachowanie i tryb życia".

---

## 3. Layout rozkładówki

### Strona lewa (ilustracja + dane systematyczne)

```
┌─────────────────────────────────────────┐
│  [Nagłówek: np. "Dinozaury Drapieżne"]  │
│  ─────────────────────────────────────  │
│                                         │
│   ┌─────────────────────────────────┐   │
│   │                                 │   │
│   │      ILUSTRACJA 16:9            │   │
│   │      (fotorealistyczna)         │   │
│   │                                 │   │
│   └─────────────────────────────────┘   │
│                                         │
│  NAZWA ZWYCZAJOWA                       │
│  Nazwa łacińska (kursywa)               │
│  Etymologia nazwy                       │
│  ─────────────────────────────────────  │
│  SYSTEMATYKA (mała czcionka, 10 poz.)   │
│  Domena › Królestwo › Typ › ... itd.    │
│  ─────────────────────────────────────  │
│  Środowisko | Dieta  (hasłowo, ikonki)  │
│  Rozmiar i masa (humorystyczne porówn.) │
│  ─────────────────────────────────────  │
│  ⚑ CIEKAWOSTKA (subtelna makabra)       │
└─────────────────────────────────────────┘
```

### Strona prawa (opisy + cytat badacza)

```
┌─────────────────────────────────────────┐
│  [Nagłówek lustrzany]        [Nr str.]  │
│  ─────────────────────────────────────  │
│                                         │
│  OPIS GATUNKU                           │
│  Pseudo-naukowy, z humorem,             │
│  kilka akapitów                         │
│                                         │
│  ─────────────────────────────────────  │
│  MIEJSCE WYSTĘPOWANIA                   │
│  Opis siedliska (fikcyjny lecz          │
│  brzmiący poważnie)                     │
│                                         │
│  ─────────────────────────────────────  │
│  ZACHOWANIE I TRYB ŻYCIA                │
│  Tu może być "łagodna makabra"          │
│  i mrugnięcie do dziecka                │
│                                         │
│  ─────────────────────────────────────  │
│  [Ozdobna ramka / winieta na dole]      │
│  💬 CYTAT BADACZA                       │
└─────────────────────────────────────────┘
```

---

## 4. Paleta i typografia

| Element | Specyfikacja |
|---|---|
| Tło | Kremowo-zielone (stary papier z zielonym marmurkiem) |
| Akcent główny | Głęboka zieleń butelkowa |
| Akcent ozdobny | Złoto — separatory, nagłówki, ramki |
| Typografia tytułowa | Elegancki serif (np. Playfair Display, IM Fell) |
| Typografia treści | Czytelny serif lub delikatny sans-serif |
| Ozdobniki | Subtelne winiety botaniczne, cienkie linie dekoracyjne |
| Format | Dwustronicowy spread A4 — każda strona osobno, razem rozkładówka |

---

## 5. Struktura repozytorium GitHub

```
dinocyclopedia/
├── template.html          ← bazowy szablon HTML (modyfikowany przez Pawła)
├── grafiki/
│   ├── glazozer.jpg
│   ├── nastepny_dinozaur.jpg
│   └── ...
└── dane/
    ├── glazozer.json
    └── ...
```

### Schemat pliku JSON (przykład)

```json
{
  "id": "glazozer",
  "nazwa_zwyczajowa": "Głazozer",
  "nazwa_łacinska": "Saxivorator magnificus",
  "etymologia": "...",
  "kategoria": "Dinozaury Roślinożerne",
  "numer_strony": 12,
  "systematyka": {
    "domena": "Eukaryota",
    "królestwo": "Animalia",
    "typ": "Chordata",
    "gromada": "Reptilia",
    "rząd": "...",
    "rodzina": "...",
    "rodzaj": "...",
    "gatunek": "..."
  },
  "środowisko": "lasy iglaste, tereny górskie",
  "dieta": "skały wapienne, granit, okazjonalnie turystyczny ekwipunek",
  "rozmiar": "12 m długości",
  "masa": "8 ton (porównywalne z 4 dorosłymi hipopotamami lub 1 dostawczym TIR-em)",
  "ciekawostka": "...",
  "opis_gatunku": "...",
  "miejsce_wystepowania": "...",
  "zachowanie": "...",
  "badacz_cytat": {
    "autor": "dr Patrycja Imaszewska-Palm",
    "cytat": "..."
  }
}
```

> **Uwaga:** Pole `badacz_cytat` może być puste — wtedy AI dobiera losowo z listy badaczy.

---

## 6. Workflow dla każdej nowej strony

1. Paweł wrzuca nową grafikę + plik JSON do repozytorium GitHub
2. Paweł podaje AI:
   - **raw URL** do grafiki (GitHub raw content)
   - **raw URL** do pliku JSON (lub wkleja treść bezpośrednio)
   - opcjonalnie: numer strony
3. AI uploaduje grafikę do Canva (`upload-asset-from-url`)
4. AI generuje wypełniony HTML na podstawie `template.html` i danych JSON
5. AI importuje HTML do Canva (`import-design-from-url`)
6. Paweł weryfikuje i ewentualnie ręcznie koryguje numer strony w Canva

---

## 7. Sekcje generowane/opracowywane przez AI

Dla każdego dinozaura AI opracowuje (na podstawie surowego opisu z JSON):

1. **Nazwa zwyczajowa** — finalna, dopracowana forma
2. **Nazwa łacińska** — pseudo-naukowa binominalna
3. **Etymologia nazwy** — humorystyczna ale brzmiąca poważnie
4. **Systematyka** — 10 poziomów taksonomicznych (fikcyjna ale spójna)
5. **Środowisko + dieta** — hasłowo, z ikonkami
6. **Rozmiar i masa** — z humorystycznym porównaniem do codziennych obiektów
7. **Ciekawostka** — subtelna makabra, sekcja ⚑
8. **Opis gatunku** — kilka akapitów, pseudo-naukowy, z humorem
9. **Miejsce występowania** — fikcyjne siedlisko, brzmiące poważnie
10. **Zachowanie i tryb życia** — tu "łagodna makabra" i mrugnięcie do dziecka
11. **Cytat badacza** — dobierany zgodnie z listą poniżej

---

## 8. Lista badaczy i specjalności cytatów

| Badacz | Specjalność cytatów |
|---|---|
| dr Patrycja Imaszewska-Palm | Nieudane plany i ekspedycyjne katastrofy |
| prof. Krystyna Imaszewska | Geografia i przyroda |
| dr Zbigniew Imaszewski | Uprawa roślin i ogrodnictwo |
| mgr Bulka | Udawana odwaga (strachliwa kocica) |
| dr Pazur | Jedzenie i przygody (kot-obżartuch) |
| red. Paweł Palm | Filmowo-reporterski |
| kpt. Marian Palm | Podróżnicze |
| prof. Małgorzata Palm | Słowotwórcze łańcuszki (np. syn profesora X donosi, że doktor Y wspomina, że...) |
| Węgiel & Karmel | Squeek-squeek-chrr-pip! (koszatniczki) |

**Zasada doboru:** Cytat dobierany losowo z listy, chyba że dane JSON wskazują konkretnego badacza w polu `badacz_cytat.autor`. Cytat musi być spójny ze specjalnością badacza i nawiązywać do konkretnego gatunku dinozaura opisywanego na stronie.

---

## 9. Wymogi techniczne HTML (import do Canva)

- Każda strona (lewa i prawa) jako osobny element z atrybutem `data-document-role="page"`
- Strony NIE mogą być zagnieżdżone w sobie
- Format A4: `width: 210mm; height: 297mm` (lub odpowiednik w px przy 96dpi: 794×1123px)
- Opcjonalny tytuł strony: `data-label="Głazozer — strona lewa"`
- Czcionki ładowane z Google Fonts lub Fontshare przez CDN
- Grafika dinozaura osadzona przez URL (raw GitHub lub Canva asset URL po uploadzie)
- Plik musi być hostowany pod publicznym URL HTTPS do importu

---

## 10. Zasady aktualizacji kontraktu

Gdy kontekst rozmowy zostanie utracony, Paweł:

1. Wkleja ten plik (lub jego URL z GitHub) na początku nowej rozmowy
2. Dodaje komendę: *"Kontynuuj zgodnie z kontraktem"*
3. Podaje dane nowego dinozaura (raw URL grafiki + JSON lub opis)

Przy każdej istotnej zmianie ustaleń (layout, paleta, workflow) — zaktualizować ten plik i wgrać nową wersję do repozytorium jako `KONTRAKT.md`.

---

*Projekt: Dinocyclopedia | Autor: Paweł Palm | Współpraca: AI (Perplexity/Claude)*
