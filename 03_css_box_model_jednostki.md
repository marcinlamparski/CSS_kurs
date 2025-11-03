# CSS Box Model w Głębi, Jednostki CSS

## Wprowadzenie

W Module 1 poznaliśmy podstawy Box Model. Teraz zagłębimy się głębiej i nauczymy się wszystkich niuansów, które są kluczowe dla profesjonalnego layoutu stron internetowych[1][2].

**Czego się nauczysz w tym module:**
- ✅ Pełne wyjaśnienie Model Pudełka
- ✅ Właściwości `box-sizing`
- ✅ Marginesy, paddingowe, obramowania w szczegółach
- ✅ Wszystkie jednostki CSS (`px`, `em`, `rem`, `%`, `vh`, `vw`)
- ✅ Zaawansowane techniki Box Model
- ✅ Debugowanie Box Model za pomocą DevTools
- ✅ Praktyczne przypadki użycia

---

## Część 1: Model Pudełka Szczegółowo

### Cztery Warstwy

```
┌──────────────────────────────────────────────┐
│  MARGIN - Przestrzeń na ZEWNĄTRZ            │
│  ┌──────────────────────────────────────────┐│
│  │ BORDER - Obramowanie                     ││
│  │ ┌──────────────────────────────────────┐ ││
│  │ │ PADDING - Przestrzeń do WEWNĄTRZ     │ ││
│  │ │ ┌──────────────────────────────────┐ │ ││
│  │ │ │ CONTENT - Zawartość              │ │ ││
│  │ │ │ (tekst, obrazy, elementy HTML)   │ │ ││
│  │ │ └──────────────────────────────────┘ │ ││
│  │ └──────────────────────────────────────┘ ││
│  └──────────────────────────────────────────┘│
└──────────────────────────────────────────────┘
```

### Szczegółowe Wyjaśnienia

**1. Content (Zawartość)**
- Obszar gdzie znajduje się rzeczywista zawartość elementu
- Rozmiar określony przez `width` i `height`
- Zawiera tekst, obrazy, inne elementy HTML

**2. Padding (Wypełnienie)**
- Transparentna przestrzeń WEWNĄTRZ obramowania
- Pomiędzy zawartością a obramowaniem
- Dziedziczy kolor tła elementu!

**3. Border (Obramowanie)**
- Linia (lub inny kształt) wokół paddingu
- Ma swoją grubość, styl, kolor
- Może być różne z każdej strony

**4. Margin (Margines)**
- Przezroczysta przestrzeń NA ZEWNĄTRZ obramowania
- Pomiędzy tym elementem a innymi
- NIE dziedziczy koloru tła

### Praktyczna Wizualizacja

```html
<div class="box">To jest zawartość</div>
```

```css
.box {
    width: 200px;
    height: 100px;
    background-color: lightblue;
    
    padding: 20px;        /* Wewnętrzna przestrzeń */
    border: 5px solid red;    /* Obramowanie */
    margin: 10px;         /* Zewnętrzna przestrzeń */
}
```

**Całkowita szerokość elementu:**
10px (margin-left) + 5px (border-left) + 20px (padding-left) + 200px (width) + 20px (padding-right) + 5px (border-right) + 10px (margin-right) = **275px**

---

## Część 2: Właściwość `box-sizing`

To jest WAŻNA właściwość![1] Zmienia jak CSS oblicza wymiary elementu.

### `box-sizing: content-box` (DOMYŚLNIE)

```css
.box {
    width: 200px;
    padding: 20px;
    border: 5px solid black;
    box-sizing: content-box;
}
```

**Wyjaśnienie:**
- `width: 200px` = tylko zawartość
- Rzeczywista szerokość = 200 + 40 (padding) + 10 (border) = **250px**
- Padding i border SĄ DODAWANE do szerokości

### `box-sizing: border-box` (REKOMENDOWANY!)

```css
.box {
    width: 200px;
    padding: 20px;
    border: 5px solid black;
    box-sizing: border-box;
}
```

**Wyjaśnienie:**
- `width: 200px` = zawartość + padding + border
- Rzeczywista szerokość = **200px** (dokładnie!)
- Padding i border są WLICZONE w szerokość

### Dlaczego `border-box`?

Jest **znacznie łatwiej** pracować z `border-box`! Zalecenie dla każdego projektu:

```css
/* Zastosuj na wszystkie elementy */
* {
    box-sizing: border-box;
}
```

### Porównanie

| Cecha | `content-box` | `border-box` |
|-------|---------------|-------------|
| Zawartość | 200px | 200px - padding - border |
| Padding | POWIĘKSZA | Wliczone |
| Border | POWIĘKSZA | Wliczone |
| Łatwe do pracy | Trudne | Bardzo łatwe |
| Domyślnie | TAK | NIE |

---

## Część 3: Margin, Padding, Border - Szczegóły

### Ustawianie Czterech Stron

Każda właściwość (margin, padding, border) można ustawić dla każdej strony osobno:

#### Notacja 1 Wartości - Wszystkie Strony Równe

```css
div {
    padding: 20px;  /* Top, Right, Bottom, Left = 20px */
}
```

#### Notacja 2 Wartości - Góra/Dół i Lewo/Prawo

```css
div {
    padding: 10px 20px;
    /* Top/Bottom = 10px, Right/Left = 20px */
}
```

#### Notacja 3 Wartości - Góra, Lewo/Prawo, Dół

```css
div {
    padding: 10px 20px 30px;
    /* Top = 10px, Right/Left = 20px, Bottom = 30px */
}
```

#### Notacja 4 Wartości - Prawo na Lewo (Zegarek!)

```css
div {
    padding: 10px 20px 30px 40px;
    /* Top = 10px, Right = 20px, Bottom = 30px, Left = 40px */
}
```

#### Indywidualne Strony

```css
div {
    padding-top: 10px;
    padding-right: 20px;
    padding-bottom: 30px;
    padding-left: 40px;
}
```

### Border - Style

```css
div {
    border-style: solid;       /* Ciągła linia */
    border-style: dashed;      /* Linia przerywana */
    border-style: dotted;      /* Punkty */
    border-style: double;      /* Podwójna linia */
    border-style: groove;      /* 3D zagłębienie */
    border-style: ridge;       /* 3D wyniesienie */
}
```

### Border - Skrót

```css
div {
    border: 5px solid red;
    /* border-width border-style border-color */
}
```

### Border-Radius - Zaokrąglenie

```css
div {
    border-radius: 5px;              /* Wszystkie rogi 5px */
    border-radius: 10px 20px;        /* Górny-lewy/Dolny-prawy, Górny-prawy/Dolny-lewy */
    border-radius: 10px 20px 30px;   /* Górny-lewy, Górny-prawy/Dolny-lewy, Dolny-prawy */
    border-radius: 10px 20px 30px 40px; /* Górny-lewy, Górny-prawy, Dolny-prawy, Dolny-lewy */
}
```

### Specjalne Efekty Granic

```css
div {
    border: 5px solid black;
    box-shadow: 0 0 10px rgba(0,0,0,0.3);  /* Cień */
}

button {
    border: 2px solid;
    border-image: linear-gradient(45deg, red, blue) 1;  /* Gradient! */
}
```

---

## Część 4: Jednostki CSS

Umiejętność wyboru prawidłowej jednostki to kluczowa umiejętność![2]

### Jednostki Absolutne

Te jednostki zawsze mają tę samą wielkość:

| Jednostka | Opis | Wartość |
|-----------|------|---------|
| `px` | Piksele | 1/96 cala |
| `cm` | Centymetry | 1 cm |
| `mm` | Milimetry | 1 mm |
| `in` | Cale | 1 cal (2.54 cm) |
| `pt` | Punkty | 1/72 cala |
| `pc` | Picas | 1/6 cala |

**Najpopularniejsza:** `px`

### Jednostki Względne

Te jednostki zmieniają się na podstawie kontekstu:

#### `em` - Względem Rodzica

```css
div {
    font-size: 16px;
}

div p {
    font-size: 1.5em;  /* 1.5 × 16px = 24px */
}
```

**Problem:** Zagnieżdżanie może być skomplikowane!

```css
div { font-size: 2em; }      /* 32px */
div div { font-size: 2em; }  /* 64px (2em × 32px) */
div div div { font-size: 2em; } /* 128px (2em × 64px) */
```

#### `rem` - Względem Root (`<html>`)

```css
html {
    font-size: 16px;  /* Domyślnie */
}

p {
    font-size: 1rem;      /* 16px */
    font-size: 1.5rem;    /* 24px */
}

div {
    font-size: 2rem;      /* 32px (zawsze względem HTML) */
    margin: 0.5rem;       /* 8px */
}
```

**Zaleta:** Konsystentne, bez zagnieżdżania!

#### Procenty `%`

```css
div {
    width: 100%;        /* Całą szerokość rodzica */
    height: 50%;        /* Połowę wysokości rodzica */
    padding: 10%;       /* 10% od szerokości */
}
```

#### Viewport Units

Względem rozmiar okna przeglądarki:

```css
div {
    width: 100vw;       /* 100% szerokości okna */
    height: 100vh;      /* 100% wysokości okna */
    width: 50vw;        /* 50% szerokości okna */
    height: 25vh;       /* 25% wysokości okna */
}
```

### Porównanie Jednostek

| Jednostka | Zaleta | Wada | Użycie |
|-----------|--------|------|--------|
| `px` | Precyzyjne | Nie skaluje się | Fiknie elementy |
| `em` | Skalowalne | Skomplikowane zagnieżdżanie | Rzadko |
| `rem` | Skalowalne, proste | Brak | Tekst, espacer |
| `%` | Responsywne | Względem rodzica | Szerokości, wysokości |
| `vw/vh` | Responsywne | Może być za duże | Pełnoekranowe sekcje |

### Zalecenie

Dla nowoczesnych stron:

```css
html {
    font-size: 16px;  /* Bazowa wielkość */
}

* {
    box-sizing: border-box;  /* Zawsze! */
}

body {
    font-size: 1rem;
    line-height: 1.6;
}

h1 {
    font-size: 2rem;
    margin: 1rem 0;
}

p {
    font-size: 1rem;
    margin-bottom: 1rem;
}

button {
    padding: 0.5rem 1rem;
    font-size: 1rem;
}
```

---

## Część 5: Zaawansowane Koncepty Box Model

### Collapsing Margins (Zapadające Marginesy)

Dwa pionowe marginesy mogą się "zapaść" (wziąć wartość większą):

```css
p {
    margin-bottom: 20px;
}

div {
    margin-top: 30px;
}
```

**Wynik:** Przestrzeń między nimi = 30px (nie 50px!)

Większy margines "wygrywa".

### Negative Margins (Ujemne Marginesy)

```css
div {
    margin-top: -20px;   /* Przesuń do góry! */
}
```

Rzadko się używa, ale przydatne do zaawansowanych layoutów.

### `overflow` - Co Gdy Zawartość Nie Mieści Się

```css
div {
    width: 200px;
    height: 100px;
    overflow: visible;   /* Zawartość wychodzi poza (domyślnie) */
    overflow: hidden;    /* Przycnij zawartość */
    overflow: scroll;    /* Dodaj scrollbar */
    overflow: auto;      /* Scrollbar tylko gdy potrzebny */
}
```

### `visibility` vs `display: none`

```css
.hidden-visibility {
    visibility: hidden;  /* Ukryty, ale zajmuje miejsce */
}

.hidden-display {
    display: none;       /* Ukryty, NIE zajmuje miejsca */
}
```

---

## Część 6: Debugging Box Model

### Użyj DevTools (F12 → Inspect)

W przeglądarce:
1. Naciśnij `F12` (lub `Ctrl+Shift+I`)
2. Kliknij "Inspect" na elemencie
3. Przejdź do zakładki "Elements" / "Inspector"
4. Szukaj sekcji "Box Model" lub "Computed"

Zobaczysz wizualny diagram:
```
┌─────────────────────────────┐
│        MARGIN               │
│ ┌───────────────────────────┤
│ │ BORDER                    │
│ │ ┌─────────────────────────┤
│ │ │ PADDING                 │
│ │ │ ┌───────────────────────┤
│ │ │ │ CONTENT (200x100)     │
│ │ │ └───────────────────────┤
```

### Pokaż Box Model z CSS

```css
* {
    outline: 1px solid red;  /* Pokazuj granice wszystkiego */
}
```

Czasami przydatne do debugowania!

---

## Część 7: Praktyczne Przykłady

### Przykład 1: Karta (Card)

```html
<div class="card">
    <h2>Tytuł Karty</h2>
    <p>Zawartość karty</p>
</div>
```

```css
* {
    box-sizing: border-box;
}

.card {
    width: 300px;
    background-color: white;
    
    padding: 20px;           /* Wewnątrz karty */
    border: 1px solid #ddd;  /* Lekkie obramowanie */
    border-radius: 8px;      /* Zaokrąglone rogi */
    
    margin: 20px auto;       /* Wyśrodkuj */
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);  /* Subtelny cień */
}

.card h2 {
    margin-top: 0;           /* Bez marginesu u góry */
    margin-bottom: 10px;
}

.card p {
    margin: 0;               /* Bez marginesu */
    color: #666;
}
```

### Przykład 2: Kontener z Paddingiem

```html
<div class="container">
    <h1>Zawartość</h1>
    <p>Paragraf</p>
</div>
```

```css
.container {
    max-width: 1200px;
    margin: 0 auto;          /* Wyśrodkuj */
    padding: 20px;           /* Odstęp od krawędzi */
}

@media (min-width: 768px) {
    .container {
        padding: 40px;
    }
}
```

### Przykład 3: Buttony Różnych Rozmiarów

```css
button {
    box-sizing: border-box;
    border: 2px solid blue;
    border-radius: 4px;
    font-weight: bold;
    cursor: pointer;
}

button.small {
    padding: 0.5rem 0.75rem;
    font-size: 0.875rem;
}

button.medium {
    padding: 0.75rem 1.5rem;
    font-size: 1rem;
}

button.large {
    padding: 1rem 2rem;
    font-size: 1.25rem;
    width: 100%;
}
```

---

## Część 8: Ćwiczenia

### Ćwiczenie 1: Zastosuj `box-sizing`

Stwórz dwa elementy `<div>` - jeden z `content-box`, drugi z `border-box`. Oba mają być 200px szerokości z 20px paddingiem i 2px obramowaniem. Obserwuj różnicę!

### Ćwiczenie 2: Jednostki

Stwórz stronę z:
- Tekst główny w `rem`
- Nagłówki w `em` (będą skalować się w zależności od rodzica)
- Marginesy w `rem`
- Paddingowe w `px`

Zmień `font-size` na `html` i obserwuj jak wszystko się skaluje!

### Ćwiczenie 3: Responsywny Kontener

Stwórz kontener, który:
- Na małych ekranach: `width: 100%`, `padding: 10px`
- Na średnich: `width: 90%`, `padding: 20px`
- Na dużych: `width: 1200px`, `padding: 40px`, wyśrodkowany

Użyj mediów queries (omówimy w module 7)!

---

## Podsumowanie

W tym module nauczyliśmy się:

✅ **Box Model** - cztery warstwy (content, padding, border, margin)  
✅ **box-sizing** - dwa sposoby obliczania wymiarów  
✅ **Margin, Padding, Border** - szczegóły każdej warstwy  
✅ **Jednostki CSS** - px, em, rem, %, vw, vh  
✅ **Zaawansowane koncepty** - collapsing margins, overflow  
✅ **Debugging** - jak używać DevTools  
✅ **Praktyczne przykłady** - karty, kontenery, buttony  

---

## Zasoby Dodatkowe

- [MDN Box Model](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Styling_basics/Box_model)
- [CSS Units Guide](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Styling_basics/Values_and_units)
- [Margin Collapsing](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Mastering_margin_collapsing)

---

*Jesteś gotowy do Modułu 4? Nauczymy się Display i Positioning! 🚀*