# CSS Grid - Zaawansowany System Layoutu

## Wprowadzenie

CSS Grid to potężny system do tworzenia dwuwymiarowych layoutów (Flexbox jest jednowymiarowy)[1][2]. Grid pozwala na precyzyjną kontrolę wierszy i kolumn.

**Czego się nauczysz w tym module:**
- ✅ Podstawy CSS Grid
- ✅ Grid container i grid items
- ✅ Definiowanie wierszy i kolumn
- ✅ Umieszczanie itemów w gridu
- ✅ Autoflow i zawijanie
- ✅ Praktyczne aplikacje Grid
- ✅ Grid vs Flexbox - kiedy używać

---

## Część 1: Podstawy Grid

### Co to CSS Grid?

CSS Grid to system do layoutu oparty na siatce wierszy i kolumn. Idealne do:
- Makiety stron
- Dashbordy
- Galerki
- Skomplikowane layouty

### Podstawowa Struktura

```html
<div class="grid-container">
    <div class="grid-item">Item 1</div>
    <div class="grid-item">Item 2</div>
    <div class="grid-item">Item 3</div>
    <div class="grid-item">Item 4</div>
    <div class="grid-item">Item 5</div>
    <div class="grid-item">Item 6</div>
</div>
```

```css
.grid-container {
    display: grid;  /* Aktywuj grid */
    grid-template-columns: 1fr 1fr 1fr;  /* 3 równe kolumny */
    grid-template-rows: 100px 100px;     /* 2 wiersze */
    gap: 10px;                            /* Odstępy */
}
```

---

## Część 2: Definiowanie Kolumn i Wierszy

### `grid-template-columns` - Definiuj Kolumny

```css
.grid {
    display: grid;
    grid-template-columns: 100px 200px 100px;  /* 3 kolumny: 100px, 200px, 100px */
}
```

### `grid-template-rows` - Definiuj Wiersze

```css
.grid {
    display: grid;
    grid-template-rows: 100px auto 50px;  /* 3 wiersze */
}
```

### Jednostka `fr` - Frakcja (Bardzo Ważna!)

`fr` to "frakcja" - elastyczna jednostka, dzieli dostępną przestrzeń.

```css
.grid {
    grid-template-columns: 1fr 1fr 1fr;  /* 3 równe kolumny */
    grid-template-columns: 1fr 2fr 1fr;  /* Środkowa 2x szersza */
    grid-template-columns: 200px 1fr;    /* Pierwsza stała 200px, reszta elastyczna */
}
```

### `repeat()` - Powtarzaj

```css
.grid {
    grid-template-columns: repeat(3, 1fr);        /* To samo co: 1fr 1fr 1fr */
    grid-template-columns: repeat(4, 100px);      /* 4 kolumny po 100px */
    grid-template-columns: repeat(auto-fit, 200px); /* Tyle kolumn ile się mieści */
}
```

### `auto-fit` i `auto-fill` - Responsywnie!

```css
.grid {
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
}
```

**Magia:** Kolumny są minimum 200px, ale rozciągają się do dostępnej przestrzeni. Przy zmniejszaniu okna automatycznie zmniejsza się liczba kolumn!

```css
.grid {
    grid-template-columns: repeat(auto-fill, 100px);
}
```

`auto-fit` - usuwa puste kolumny  
`auto-fill` - tworzy puste kolumny

### `minmax()` - Minimalna i Maksymalna Wysokość/Szerokość

```css
.grid {
    grid-template-columns: minmax(100px, 200px);  /* Min 100px, Max 200px */
    grid-template-rows: minmax(50px, auto);       /* Min 50px, rozciągnij się */
}
```

---

## Część 3: Rozmieszczanie Itemów

### `grid-column` i `grid-row` - Umieść Item

```css
.item {
    grid-column: 1;        /* Kolumna 1 */
    grid-row: 1;           /* Wiersz 1 */
}
```

### `grid-column-start` i `grid-column-end` - Rozciągnij Item

```css
.item {
    grid-column-start: 1;  /* Zacznij w kolumnie 1 */
    grid-column-end: 3;    /* Skończ przed kolumną 3 (zajmuje 1-2) */
}

/* Skrót */
.item {
    grid-column: 1 / 3;    /* To samo */
    grid-column: 1 / span 2; /* Zajmij 2 kolumny od 1 */
}
```

### Praktycznie

```html
<div class="grid-container">
    <div class="item">Item 1</div>
    <div class="item hero">Hero (rozciągnięty)</div>
    <div class="item">Item 3</div>
</div>
```

```css
.grid-container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(3, 100px);
    gap: 10px;
}

.hero {
    grid-column: 1 / 4;    /* Zajmij wszystkie 3 kolumny */
    grid-row: 1 / 3;       /* Zajmij 2 wiersze */
}
```

---

## Część 4: Wyrównanie w Gridu

### `justify-items` - Wyrównanie Itemów Poziomo

```css
.grid {
    justify-items: start;      /* Do lewej */
    justify-items: end;        /* Do prawej */
    justify-items: center;     /* Wyśrodkuj */
    justify-items: stretch;    /* Rozciągnij (domyślnie) */
}
```

### `align-items` - Wyrównanie Itemów Pionowo

```css
.grid {
    align-items: start;        /* Do góry */
    align-items: end;          /* Do dołu */
    align-items: center;       /* Wyśrodkuj */
    align-items: stretch;      /* Rozciągnij (domyślnie) */
}
```

### `justify-content` - Wyrównanie Gridu Poziomo

```css
.grid {
    justify-content: center;       /* Wyśrodkuj siatkę */
    justify-content: space-between; /* Równa przestrzeń */
}
```

### `align-content` - Wyrównanie Gridu Pionowo

```css
.grid {
    align-content: center;     /* Wyśrodkuj siatkę */
}
```

---

## Część 5: Praktyczne Przykłady

### Przykład 1: Makieta Strony

```html
<div class="page-grid">
    <header>Header</header>
    <nav>Navigation</nav>
    <main>Main Content</main>
    <aside>Sidebar</aside>
    <footer>Footer</footer>
</div>
```

```css
.page-grid {
    display: grid;
    grid-template-columns: 200px 1fr 200px;
    grid-template-rows: auto 1fr auto;
    gap: 10px;
    min-height: 100vh;
}

header {
    grid-column: 1 / -1;  /* Zajmij wszystkie kolumny */
}

nav {
    grid-row: 2;
    grid-column: 1;
}

main {
    grid-row: 2;
    grid-column: 2;
}

aside {
    grid-row: 2;
    grid-column: 3;
}

footer {
    grid-column: 1 / -1;
}
```

### Przykład 2: Galeria Responsywna

```html
<div class="gallery">
    <img src="1.jpg" alt="1">
    <img src="2.jpg" alt="2">
    <img src="3.jpg" alt="3">
    <!-- ... -->
</div>
```

```css
.gallery {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 15px;
    padding: 20px;
}

.gallery img {
    width: 100%;
    height: 200px;
    object-fit: cover;
    border-radius: 8px;
}
```

**Na dużych ekranach:** Wiele kolumn  
**Na małych ekranach:** Mniej kolumn  
**Automatycznie!**

### Przykład 3: Dashboard

```html
<div class="dashboard">
    <div class="stat">Stat 1</div>
    <div class="stat">Stat 2</div>
    <div class="stat">Stat 3</div>
    <div class="chart">Chart (rozciągnięty)</div>
    <div class="table">Table (rozciągnięty)</div>
</div>
```

```css
.dashboard {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    grid-template-rows: auto auto 1fr;
    gap: 20px;
    padding: 20px;
}

.stat {
    background-color: white;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
}

.chart {
    grid-column: 1 / -1;
    background-color: white;
    padding: 20px;
}

.table {
    grid-column: 1 / -1;
    background-color: white;
    padding: 20px;
}
```

### Przykład 4: Artykuł z Obrazem

```html
<article class="article-grid">
    <img src="hero.jpg" alt="Hero">
    <h1>Tytuł Artykułu</h1>
    <p class="content">Zawartość artykułu...</p>
    <aside>Sidebar</aside>
</article>
```

```css
.article-grid {
    display: grid;
    grid-template-columns: 200px 1fr;
    grid-template-rows: 300px auto auto auto;
    gap: 20px;
}

img {
    grid-column: 1 / -1;
    width: 100%;
    height: 300px;
    object-fit: cover;
}

h1 {
    grid-column: 1 / -1;
}

.content {
    grid-column: 1;
    grid-row: 3;
}

aside {
    grid-column: 2;
    grid-row: 3 / 5;
}
```

---

## Część 6: Grid vs Flexbox

| Cecha | Grid | Flexbox |
|-------|------|---------|
| Wymiary | 2D (wiersze + kolumny) | 1D (wiersz LUB kolumna) |
| Komplikacja | Bardziej zaawansowany | Prostszy |
| Idealny do | Makiety, galerki | Elementy nawigacji, komponenty |
| Precyzja | Wysoka | Średnia |
| Responsywność | Bardzo łatwa | Łatwa |

**Reguła:** Jeśli potrzebujesz dwuwymiarowego layoutu - Grid. Jeśli jednowymiarowego - Flexbox.

---

## Część 7: Ćwiczenia

### Ćwiczenie 1: Prosta Siatka

Stwórz siatkę 3x3:
- 9 itemów
- Równe kolumny
- Równe wiersze (100px każdy)
- Będę między itemami

### Ćwiczenie 2: Responsywna Galeria

Stwórz galerię zdjęć:
- Minimum 200px szerokości na karcie
- Automatycznie dostosuj liczbę kolumn
- Gap między kartami 15px

### Ćwiczenie 3: Layout Strony

Stwórz makiete strony z:
- Header (cały szeroki)
- Sidebar (200px lewa kolumna)
- Main (środek)
- Footer (cały szeroki)

### Ćwiczenie 4: Rozciągnięte Elementy

Stwórz siatkę gdzie:
- Hero zajmuje 2 wiersze i 2 kolumny
- Reszta elementy normalnie

---

## Cheatsheet Grid

```css
/* Container */
.grid {
    display: grid;
    grid-template-columns: repeat(3, 1fr);     /* 3 równe kolumny */
    grid-template-rows: 100px auto;            /* 2 wiersze */
    gap: 20px;                                  /* Odstęp */
}

/* Item */
.item {
    grid-column: 1 / 3;                        /* Zajmij kolumny 1-2 */
    grid-row: 1 / 4;                           /* Zajmij wiersze 1-3 */
}

/* Responsywnie */
.responsive {
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
}
```

---

## Podsumowanie

W tym module nauczyliśmy się:

✅ **Grid Basics** - display: grid  
✅ **Kolumny i Wiersze** - template-columns, template-rows  
✅ **fr Unit** - elastyczne jednostki  
✅ **Umieszczanie** - grid-column, grid-row  
✅ **Wyrównanie** - justify, align  
✅ **Praktyczne aplikacje** - makiety, galerki, dashbordy  
✅ **Grid vs Flexbox** - kiedy co używać  

---

## Zasoby Dodatkowe

- [MDN CSS Grid](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/CSS_layout/Grids)
- [CSS Tricks Grid Guide](https://css-tricks.com/snippets/css/complete-guide-grid/)
- [Grid Playground](https://www.cssgridplayground.com/)

---

*Jesteś gotowy do Modułu 7? Nauczymy się Media Queries i Responsive Design! 🚀*