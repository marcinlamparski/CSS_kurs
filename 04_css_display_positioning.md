# CSS Display i Positioning

## Wprowadzenie

Właściwości `display` i `position` to dwie najważniejsze właściwości do kontrolowania layoutu strony internetowej. W tym module nauczysz się jak elementy zajmują przestrzeń i jak je pozycjonować[1][2].

**Czego się nauczysz w tym module:**
- ✅ Wartości `display` (block, inline, inline-block, none)
- ✅ Ukrywanie elementów (visibility vs display)
- ✅ Pozycjonowanie (static, relative, absolute, fixed, sticky)
- ✅ Z-index i układanie warstw
- ✅ Praktyczne zastosowania layoutów
- ✅ Responsive design z display

---

## Część 1: Właściwość `display`

Właściwość `display` mówi przeglądarce, jak element powinien być renderowany[1].

### `display: block` - Element Blokowy

Zajmuje **całą szerokość dostępną** i tworzy nową linię.

```css
div, p, h1, h2, section, header, footer {
    display: block;  /* Domyślnie dla tych elementów */
}
```

**Charakterystyka:**
- Zajmuje całą szerokość
- Nowa linia przed i po
- Respektuje margin, padding, border ze wszystkich stron
- Szerokość i wysokość są efektywne

```html
<p>Paragraph 1</p>
<p>Paragraph 2</p>
<!-- Każdy na osobnej linii -->
```

### `display: inline` - Element Liniowy

Zajmuje **tylko tyle miejsca ile potrzebuje** i NIE tworzy nowej linii.

```css
span, a, strong, em {
    display: inline;  /* Domyślnie dla tych elementów */
}
```

**Charakterystyka:**
- Obok siebie (w tej samej linii)
- Nie tworzy nowych linii
- Margin lewy/prawy działają
- Margin górny/dolny NIE działają!
- Width i height NIE działają!

```html
<span>Tekst 1</span><span>Tekst 2</span><span>Tekst 3</span>
<!-- Wszystkie w tej samej linii -->
```

### `display: inline-block` - Mieszany

Kombinacja `block` i `inline` - najlepsze z obu światów!

```css
button, img {
    display: inline-block;
}
```

**Charakterystyka:**
- Obok siebie (jak inline)
- Ale respektuje width, height, margin ze wszystkich stron (jak block)
- Perfekcyjne dla buttonów, obrazów, małych komponentów

```css
button {
    display: inline-block;
    padding: 10px 20px;
    margin: 5px;
    width: auto;
    height: auto;
}
```

### `display: none` - Całkowicie Ukryty

Element jest całkowicie usunięty ze strony - **nie zajmuje miejsca**.

```css
.ukryty {
    display: none;  /* Nie widać, nie zajmuje miejsca */
}
```

vs `visibility: hidden` (zajmuje miejsce):

```css
.niewidoczny {
    visibility: hidden;  /* Niewidoczny, ale zajmuje miejsce */
}
```

### Porównanie Wartości Display

| Wartość | Obok Siebie | Nowa Linia | Width/Height | Margin Wszystko | Użycie |
|---------|------------|-----------|--------------|-----------------|--------|
| `block` | NIE | TAK | TAK | TAK | `<div>`, `<p>` |
| `inline` | TAK | NIE | NIE | Częściowo | `<span>`, `<a>` |
| `inline-block` | TAK | NIE | TAK | TAK | Komponenty |
| `none` | - | - | - | - | Ukrywanie |

### Praktyczne Przykłady Display

```html
<nav>
    <a href="/">Home</a>
    <a href="/about">About</a>
    <a href="/contact">Contact</a>
</nav>
```

**Linki domyślnie są inline - jak je wyrównać obok siebie w kolumnie?**

```css
/* Opcja 1: inline-block */
nav a {
    display: inline-block;
    padding: 10px 15px;
    border-bottom: 2px solid transparent;
}

nav a:hover {
    border-bottom: 2px solid blue;
}

/* Opcja 2: block z flexbox (moduł 5) */
nav {
    display: flex;
}

nav a {
    padding: 10px 15px;
}
```

---

## Część 2: Właściwość `position`

Właściwość `position` mówi jak element powinien być pozycjonowany[2].

### `position: static` (DOMYŚLNIE)

Element zajmuje swoją naturalną pozycję w dokumencie.

```css
div {
    position: static;  /* Domyślnie */
}
```

Właściwości `top`, `right`, `bottom`, `left` NIE działają!

### `position: relative` - Względnie do Naturalnej Pozycji

Element jest pozycjonowany **względem swojej normalnej pozycji**.

```css
div {
    position: relative;
    top: 20px;        /* Przesuń 20px w dół */
    left: 10px;       /* Przesuń 10px w prawo */
}
```

**Charakterystyka:**
- Zajmuje miejsce w przepływie dokumentu (normalnie)
- Ale może być przesunięty za pomocą `top`, `right`, `bottom`, `left`
- Nie wpływa na położenie innych elementów
- Przydatne do drobnych adjustmentów

```html
<div class="normal">Normalny</div>
<div class="przesuniete">Przesunięty (ale zajmuje naturalne miejsce)</div>
<div class="normal">Normalny</div>
```

```css
.przesuniete {
    position: relative;
    top: 50px;        /* Wychodzi do dołu */
    left: 100px;      /* Wychodzi w prawo */
}
```

### `position: absolute` - Absolutnie Pozycjonowany

Element jest wyjęty ze strumienia dokumentu i pozycjonowany **względem najbliższego przodka z `position: relative/absolute/fixed`** (lub `<html>`)[2].

```css
.container {
    position: relative;  /* Ustaw kontekst pozycjonowania */
}

.box {
    position: absolute;
    top: 50px;
    left: 100px;
}
```

**Charakterystyka:**
- Wyjęty ze strumienia - NIE zajmuje naturalnego miejsca
- Inne elementy go ignorują
- Pozycjonowany względem rodzica z `position` (lub `<html>`)
- Idealne do modali, tooltipów, drop-downów

```html
<div class="container">
    <div class="box">Absolutny box</div>
    <p>Tekst - box go nie wpłynie</p>
</div>
```

```css
.container {
    position: relative;
    width: 300px;
    height: 200px;
    border: 1px solid black;
}

.box {
    position: absolute;
    top: 50px;        /* 50px od góry kontenera */
    left: 50px;       /* 50px od lewej kontenera */
    background-color: red;
    width: 100px;
    height: 100px;
}
```

### `position: fixed` - Przylgnięty do Viewportu

Element jest pozycjonowany **względem okna przeglądarki** i zostaje na miejscu nawet przy scrollowaniu[2].

```css
.sticky-header {
    position: fixed;
    top: 0;           /* Przylgnij do góry */
    width: 100%;
    background-color: white;
    z-index: 100;     /* Bądź na wierzchu */
}
```

**Charakterystyka:**
- Zawsze widoczny (nawet przy scrollowaniu)
- Pozycjonowany względem okna
- Wyjęty ze strumienia
- Idealne do headeru, stopki, floating buttonu

```css
/* Sticky header */
header {
    position: fixed;
    top: 0;
    width: 100%;
    height: 60px;
    background-color: navy;
    color: white;
}

body {
    padding-top: 60px;  /* Place for header */
}

/* Floating button */
.float-button {
    position: fixed;
    bottom: 20px;
    right: 20px;
    width: 60px;
    height: 60px;
    border-radius: 50%;
    background-color: green;
    cursor: pointer;
}
```

### `position: sticky` - Lepki (Pośredni)

Element jest normalnie w przepływie, ale **przykleja się do viewportu** gdy scrolujesz do niego[2].

```css
h2 {
    position: sticky;
    top: 0;           /* Przylgnij 0px od góry */
    background-color: lightgray;
}
```

**Charakterystyka:**
- Normalnie w przepływie (do pewnego punktu)
- Przy scrollowaniu przylgnięty do viewportu
- Idealny do sekcji nagłówków
- Mniej wspierany niż `fixed` (check dla starszych przeglądarek)

```html
<section>
    <h2>Sekcja 1</h2>
    <p>Treść...</p>
</section>

<section>
    <h2>Sekcja 2</h2>
    <p>Treść...</p>
</section>
```

```css
h2 {
    position: sticky;
    top: 0;
    background-color: #f0f0f0;
    padding: 10px;
}
```

### Porównanie Position

| Wartość | Strumień | Względem | Zajmuje Miejsce | Użycie |
|---------|----------|---------|-----------------|--------|
| `static` | TAK | - | TAK | Domyślnie |
| `relative` | TAK | Naturalne | TAK | Drobne adjustmenty |
| `absolute` | NIE | Rodzic z `position` | NIE | Modals, tooltips |
| `fixed` | NIE | Viewport | NIE | Header, float button |
| `sticky` | TAK (do punktu) | Viewport | TAK | Sticky headers |

---

## Część 3: Z-Index i Warstwy

Gdy elementy się nakładają, `z-index` mówi który powinien być na wierzchu[1].

```css
.box1 {
    position: absolute;
    z-index: 1;       /* Niżej */
}

.box2 {
    position: absolute;
    z-index: 2;       /* Wyżej */
}
```

**Zasady:**
- Wyższy `z-index` = bliżej przeglądarki
- Domyślnie `z-index: auto` (domyślny porządek DOM)
- Tylko działa z `position: relative/absolute/fixed/sticky`
- Elementy `inline` mają niższy `z-index` od elementów `block`

```html
<div class="background">Tło</div>
<div class="modal">Modal (powinien być na wierzchu)</div>
```

```css
.background {
    position: absolute;
    z-index: 1;
}

.modal {
    position: absolute;
    z-index: 100;  /* Dużo wyżej */
}
```

---

## Część 4: Praktyczne Przykłady

### Przykład 1: Sticky Header

```html
<header>
    <h1>Moja Strona</h1>
</header>

<main>
    <section>
        <h2>Sekcja 1</h2>
        <p>Zawartość...</p>
    </section>
</main>
```

```css
header {
    position: sticky;
    top: 0;
    background-color: navy;
    color: white;
    padding: 20px;
    z-index: 50;
}

section {
    padding: 40px;
}
```

### Przykład 2: Modal Dialog

```html
<div class="modal-overlay">
    <div class="modal">
        <h2>Wiadomość</h2>
        <p>Zawartość modalu</p>
        <button>Zamknij</button>
    </div>
</div>
```

```css
.modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background-color: rgba(0,0,0,0.5);
    z-index: 999;
    display: flex;
    align-items: center;
    justify-content: center;
}

.modal {
    position: relative;
    background-color: white;
    padding: 30px;
    border-radius: 8px;
    max-width: 500px;
    z-index: 1000;
}
```

### Przykład 3: Floating Action Button

```html
<body>
    <div class="fab">📧</div>
    <!-- ... zawartość strony ... -->
</body>
```

```css
.fab {
    position: fixed;
    bottom: 30px;
    right: 30px;
    width: 70px;
    height: 70px;
    background-color: #ff6b6b;
    color: white;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 2em;
    cursor: pointer;
    box-shadow: 0 4px 8px rgba(0,0,0,0.3);
    z-index: 50;
}

.fab:hover {
    background-color: #ff5252;
    box-shadow: 0 6px 12px rgba(0,0,0,0.4);
}
```

---

## Część 5: Ćwiczenia

### Ćwiczenie 1: Display

Stwórz menu nawigacyjne z linkami. Domyślnie linki są `inline`. Zmień na:
1. `display: block` - linki pod sobą
2. `display: inline-block` - linki obok siebie
3. Dodaj padding i background każdemu linkowi

### Ćwiczenie 2: Position Relative

Stwórz kartę produktu z nagłówkiem "NOWY" w górnym lewym rogu. Użyj:
- `position: relative` na karcie
- `position: absolute` na etykiecie "NOWY"
- Ustaw prawidłowe `top` i `left`

### Ćwiczenie 3: Sticky Section

Stwórz blogpost z nagłówkami sekcji:
- Sekcja 1, Sekcja 2, Sekcja 3
- Ustaw nagłówki jako `position: sticky` `top: 0`
- Dodaj background color żeby wyróżnić

### Ćwiczenie 4: Z-Index

Stwórz dwa `<div>` które się nakładają. Zmień `z-index` aby zmienić kolejność nakładania.

---

## Podsumowanie

W tym module nauczyliśmy się:

✅ **Display** - block, inline, inline-block, none  
✅ **Position** - static, relative, absolute, fixed, sticky  
✅ **Z-Index** - kontrolowanie warstw  
✅ **Praktyczne aplikacje** - sticky header, modal, FAB  

---

## Zasoby Dodatkowe

- [MDN Display Property](https://developer.mozilla.org/en-US/docs/Web/CSS/display)
- [MDN Position Property](https://developer.mozilla.org/en-US/docs/Web/CSS/position)
- [CSS Positioning Guide](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Styling_basics/Positioning)

---

*Jesteś gotowy do Modułu 5? Nauczymy się Flexbox - rewolucyjnego systemu layoutu! 🚀*