# CSS Flexbox - Nowoczesny Layout

## Wprowadzenie

Flexbox (Flexible Box Layout) to nowoczesny system do tworzenia layoutów. Zastępuje starsze metody i jest **znacznie prostszy** do pracy[1][2].

**Czego się nauczysz w tym module:**
- ✅ Co to Flexbox i jak go używać
- ✅ Flex container i flex items
- ✅ Właściwości flex containera (direction, wrap, justify-content, align-items)
- ✅ Właściwości flex itemów (flex, align-self, order)
- ✅ Praktyczne aplikacje Flexbox
- ✅ Responsywne layouty z Flexbox

---

## Część 1: Wprowadzenie do Flexbox

Flexbox to system do rozmieszczania elementów w linii (lub kolumnie) z automatycznym rozmieszczeniem przestrzeni[1].

### Dlaczego Flexbox?

Przed Flexbox:
- Używaliśmy `float`, `display: inline-block`, tabeli
- Skomplikowane i nieprzewidywalne
- Trudno wyrównać elementy pionowo

Z Flexbox:
- Prosty, przewidywalny system
- Wyrównanie pionowe i poziome
- Responsywne layouty
- Świetnie wspierany (IE 11+)

### Podstawowa Struktura

```html
<div class="flex-container">
    <div class="flex-item">Item 1</div>
    <div class="flex-item">Item 2</div>
    <div class="flex-item">Item 3</div>
</div>
```

```css
.flex-container {
    display: flex;  /* WAŻNE: aktywuj flexbox */
}

.flex-item {
    /* Elementy są automatycznie w wierszu */
}
```

### Flex Container vs Flex Item

- **Flex Container** - rodzic z `display: flex`
- **Flex Item** - bezpośrednie dzieci flex containera

```
Flex Container
├── Flex Item 1
├── Flex Item 2
└── Flex Item 3
```

---

## Część 2: Osie Flexbox

Flexbox ma **dwie osie**:

```
┌─────────────────────────────────────────┐
│ Main Axis (Główna oś) →                 │
│                                          │
│  ├─ Flex Item 1                         │
│  ├─ Flex Item 2                         │
│  └─ Flex Item 3                         │
│                                          │
│ Cross Axis (Oś krzyżowa) ↓              │
└─────────────────────────────────────────┘
```

**Main Axis (Główna)** - kierunek itemów (domyślnie poziom →)  
**Cross Axis (Krzyżowa)** - prostopadła do głównej (domyślnie pion ↓)

---

## Część 3: Właściwości Flex Containera

### 1. `flex-direction` - Kierunek Itemów

```css
.flex-container {
    display: flex;
    flex-direction: row;           /* → (domyślnie) */
    flex-direction: row-reverse;   /* ← */
    flex-direction: column;        /* ↓ */
    flex-direction: column-reverse; /* ↑ */
}
```

**Wizualizacja:**
```
row:           Item1  Item2  Item3 →
row-reverse:   Item3  Item2  Item1 ←
column:        Item1
               Item2 ↓
               Item3
column-reverse: Item3
               Item2 ↑
               Item1
```

### 2. `justify-content` - Rozmieszczenie Na Głównej Osi

```css
.flex-container {
    display: flex;
    justify-content: flex-start;    /* Na początek (domyślnie) */
    justify-content: flex-end;      /* Na koniec */
    justify-content: center;        /* Wyśrodkuj */
    justify-content: space-between; /* Równa przestrzeń pomiędzy */
    justify-content: space-around;  /* Równa przestrzeń dookoła */
    justify-content: space-evenly;  /* Dokładnie równa wszędzie */
}
```

**Wizualizacja:**
```
flex-start:     Item1 Item2 Item3 ___
flex-end:       ___ Item1 Item2 Item3
center:         __ Item1 Item2 Item3 __
space-between:  Item1 __ Item2 __ Item3
space-around:   _ Item1 _ Item2 _ Item3 _
space-evenly:   _ Item1 _ Item2 _ Item3 _
```

### 3. `align-items` - Rozmieszczenie Na Osi Krzyżowej

```css
.flex-container {
    display: flex;
    align-items: stretch;     /* Rozciągnij (domyślnie) */
    align-items: flex-start;  /* Na początek */
    align-items: flex-end;    /* Na koniec */
    align-items: center;      /* Wyśrodkuj */
    align-items: baseline;    /* Wyrównaj do linii tekstu */
}
```

**Wizualizacja:**
```
stretch:    ┌─────────┐
            │ Item1   │
            │ Item2   │
            │ Item3   │
            └─────────┘

center:     ┌─────────┐
            │         │
            │ Item1   │
            │ Item2   │
            │ Item3   │
            │         │
            └─────────┘
```

### 4. `flex-wrap` - Zawijanie Itemów

```css
.flex-container {
    display: flex;
    flex-wrap: nowrap;    /* Wszystko w jednej linii (domyślnie) */
    flex-wrap: wrap;      /* Zawijaj do kolejnych linii */
    flex-wrap: wrap-reverse; /* Zawijaj wstecz */
}
```

**Użyteczne!** Domyślnie Flexbox zmniejsza itemy aby zmieściły się. `flex-wrap: wrap` pozwala na przepływanie do linii.

### 5. `gap` - Odstęp Między Itemami

```css
.flex-container {
    display: flex;
    gap: 20px;           /* Odstęp wszędzie */
    gap: 10px 20px;      /* Odstęp pionowy, poziomy */
    row-gap: 10px;       /* Tylko pomiędzy wierszami */
    column-gap: 20px;    /* Tylko pomiędzy kolumnami */
}
```

**Super przydatne!** Nie musisz już margin na elementy.

---

## Część 4: Właściwości Flex Itemów

### 1. `flex` - Rozmiar Flex Itema

```css
.flex-item {
    flex: 1;    /* Weź równą część dostępnej przestrzeni */
    flex: 2;    /* Weź 2x więcej niż `flex: 1` */
    flex: 0;    /* Nie rośnij */
}
```

**Praktycznie:**
```html
<div class="flex-container">
    <div class="flex-item" style="flex: 1;">1</div>
    <div class="flex-item" style="flex: 2;">2</div>
    <div class="flex-item" style="flex: 1;">1</div>
</div>
```

Środkowy item będzie 2x szerszy!

### 2. `flex-grow` - Rośnij

```css
.flex-item {
    flex-grow: 1;   /* Rośnij, jeśli jest miejsce */
    flex-grow: 0;   /* Nie rośnij (domyślnie) */
}
```

### 3. `flex-shrink` - Kurczenie

```css
.flex-item {
    flex-shrink: 1;   /* Kurczenie się (domyślnie) */
    flex-shrink: 0;   /* Nie kurczysz się */
}
```

### 4. `flex-basis` - Bazowa Szerokość

```css
.flex-item {
    flex-basis: 200px;   /* Domyślnie 200px szerokości */
    flex: 1 1 200px;     /* Skrót: grow shrink basis */
}
```

### 5. `align-self` - Wyrównanie Pojedynczego Itema

```css
.flex-item {
    align-self: flex-start;  /* Wyrównaj do góry */
    align-self: flex-end;    /* Wyrównaj do dołu */
    align-self: center;      /* Wyśrodkuj */
}
```

### 6. `order` - Zmień Kolejność

```css
.flex-item:nth-child(1) { order: 3; }  /* Trzeci */
.flex-item:nth-child(2) { order: 1; }  /* Pierwszy */
.flex-item:nth-child(3) { order: 2; }  /* Drugi */
```

Domyślnie `order: 0`. Wyższe wartości idą na koniec.

---

## Część 5: Praktyczne Przykłady

### Przykład 1: Nawigacja Horizontalna

```html
<nav>
    <a href="/">Logo</a>
    <a href="/about">O nas</a>
    <a href="/products">Produkty</a>
    <a href="/contact">Kontakt</a>
</nav>
```

```css
nav {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 1rem;
    background-color: navy;
}

nav a {
    color: white;
    text-decoration: none;
    padding: 0.5rem 1rem;
}

nav a:hover {
    background-color: rgba(255,255,255,0.1);
}
```

**Wynik:** Logo na lewo, linki na prawo, wszystko wyrównane pionowo.

### Przykład 2: Trzy Kolumny

```html
<div class="three-columns">
    <div class="column">Kolumna 1</div>
    <div class="column">Kolumna 2</div>
    <div class="column">Kolumna 3</div>
</div>
```

```css
.three-columns {
    display: flex;
    gap: 20px;
}

.column {
    flex: 1;  /* Każda kolumna równa szerokość */
    padding: 20px;
    background-color: lightgray;
}
```

### Przykład 3: Responsywny Layout

```html
<div class="grid">
    <div class="card">Karta 1</div>
    <div class="card">Karta 2</div>
    <div class="card">Karta 3</div>
    <div class="card">Karta 4</div>
</div>
```

```css
.grid {
    display: flex;
    flex-wrap: wrap;
    gap: 20px;
}

.card {
    flex: 1 1 250px;  /* Rośnij, kurczysz się, bazowo 250px */
    background-color: white;
    padding: 20px;
    border: 1px solid #ddd;
}
```

Na dużych ekranach: 4 kolumny  
Na średnich: 2-3 kolumny  
Na małych: 1 kolumna  
*Wszystko automatycznie!*

### Przykład 4: Sticky Footer

```html
<body class="flex-body">
    <header>Header</header>
    <main>Zawartość</main>
    <footer>Footer</footer>
</body>
```

```css
.flex-body {
    display: flex;
    flex-direction: column;
    min-height: 100vh;  /* Minimum wysokość okna */
}

main {
    flex: 1;  /* Rośnij i zajmij przestrzeń */
}

footer {
    background-color: gray;
    padding: 20px;
    margin-top: auto;
}
```

### Przykład 5: Wyrównanie Pionu i Poziomu

```html
<div class="centered">
    <div class="content">Wyśrodkowany Content!</div>
</div>
```

```css
.centered {
    display: flex;
    justify-content: center;  /* Poziom */
    align-items: center;      /* Pion */
    height: 100vh;            /* Pełna wysokość */
}

.content {
    text-align: center;
}
```

**To jest najłatwszy sposób na wyrównanie w CSS!**

---

## Część 6: Ćwiczenia

### Ćwiczenie 1: Menu Flexbox

Stwórz nawigację z logo na lewo i linkami na prawo:
- Logo powinno być po lewej
- Linki powinny być po prawej
- Wszystko wyrównane pionowo
- Dodaj gap między elementami

### Ćwiczenie 2: Kolumny

Stwórz 3 kolumny artykułów:
- Każda kolumna powinna być równa szerokość
- Między kolumnami jest 20px odstępu
- Gdy zmienisz szerokość okna, kolumny się dostosowują

### Ćwiczenie 3: Karty w Siatce

Stwórz siatkę kart (4 karty w rzędzie na dużych ekranach):
- Karty powinny być responsywne
- Użyj `flex-wrap` aby zawijały się do kolejnych linii
- Każda karta powinna być elastyczna

### Ćwiczenie 4: Wyrównanie

Stwórz element, który jest wyśrodkowany zarówno poziomo jak i pionowo:
- Użyj Flexbox
- Wysokość minimum 300px
- Zawartość wewnątrz powinna być wyśrodkowana

---

## Cheatsheet Flexbox

```css
/* Container */
.flex-container {
    display: flex;
    flex-direction: row;              /* row | column */
    justify-content: center;          /* wyrównanie główne */
    align-items: center;              /* wyrównanie krzyżowe */
    flex-wrap: wrap;                  /* zawijanie */
    gap: 20px;                        /* odstępy */
}

/* Item */
.flex-item {
    flex: 1;                          /* rośnij */
    flex-basis: 200px;                /* bazowa szerokość */
    align-self: center;               /* wyrównanie indywidualne */
    order: 1;                         /* zmień kolejność */
}
```

---

## Podsumowanie

W tym module nauczyliśmy się:

✅ **Flexbox Basics** - display: flex  
✅ **Osie** - Main axis i Cross axis  
✅ **Container Properties** - direction, justify-content, align-items, wrap, gap  
✅ **Item Properties** - flex, grow, shrink, basis, align-self, order  
✅ **Praktyczne aplikacje** - nawigacja, kolumny, karty, wyrównanie  

---

## Zasoby Dodatkowe

- [MDN Flexbox](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/CSS_layout/Flexbox)
- [CSS Tricks Flexbox Guide](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)
- [Flexbox Playground](https://flexboxplayground.tetadecoder.com/)

---

*Jesteś gotowy do Modułu 6? Nauczymy się CSS Grid - drugiego fiara systemu layoutu! 🚀*