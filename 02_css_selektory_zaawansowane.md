# CSS Selektory Zaawansowane, Pseudo-klasy, Kombinatory

## Wprowadzenie

W Module 1 nauczyliśmy się podstawowych selectorów (elementu, klasy, ID). Teraz przejdziemy na zaawansowany poziom i nauczymy się bardziej złożonych metod wybierania elementów HTML[1][2].

**Czego się nauczysz w tym module:**
- ✅ Kombinatory CSS (descendant, child, sibling)
- ✅ Pseudo-klasy (`:hover`, `:focus`, `:nth-child()`, itp.)
- ✅ Pseudo-elementy (`::before`, `::after`, `::first-line`)
- ✅ Selektory atrybutów (`[type="text"]`)
- ✅ Specificity (specyficzność) - ważny koncept!
- ✅ Zaawansowane selektory w praktyce

---

## Część 1: Kombinatory CSS

Kombinatory opisują relacje między selectorami[1]. Pozwalają na precyzyjny wybór elementów na podstawie ich pozycji w drzewie HTML.

### 1. Selektor Potomka (Descendant Selector) - Spacja

Wybiera wszystkie elementy będące potomkami (na dowolnym poziomie) wybranego elementu.

```css
div p {
    color: blue;
}
```

```html
<div>
    <p>To będzie niebieskie</p>
    <section>
        <p>To też będzie niebieskie (potomek)</p>
    </section>
</div>
```

**Wyjaśnienie:** Wszystkie `<p>` wewnątrz `<div>`, niezależnie jak głębokie.

### 2. Selektor Dziecka (Child Selector) - >

Wybiera BEZPOŚREDNIE dzieci wybranego elementu (tylko jeden poziom głębi).

```css
div > p {
    color: red;
}
```

```html
<div>
    <p>To będzie czerwone (bezpośrednie dziecko)</p>
    <section>
        <p>To NIE będzie czerwone (wnuk, nie dziecko)</p>
    </section>
</div>
```

**Różnica:** `div p` vs `div > p` - pamiętaj!

### 3. Selektor Siostry (Sibling Selector) - +

Wybiera element, który natychmiast następuje po innym elemencie.

```css
h2 + p {
    font-weight: bold;
}
```

```html
<h2>Nagłówek</h2>
<p>To będzie pogrubione (siostra)</p>
<p>To NIE będzie pogrubione</p>
```

**Wyjaśnienie:** Tylko pierwszy `<p>` bezpośrednio po `<h2>`.

### 4. Selektor Siostry Ogólnie (General Sibling Selector) - ~

Wybiera wszystkie elementy, które są siostrami wybranego elementu.

```css
h2 ~ p {
    font-style: italic;
}
```

```html
<h2>Nagłówek</h2>
<p>Kursywa</p>
<p>Kursywa</p>
<p>Kursywa</p>
```

**Wyjaśnienie:** Wszystkie `<p>` które przychodzą po `<h2>`.

### Porównanie Kombinatorów

| Kombinator | Symbol | Opis | Przykład |
|-----------|--------|------|----------|
| Descendant | spacja | Wszystkie potomki | `div p` |
| Child | `>` | Bezpośrednie dzieci | `div > p` |
| Adjacent | `+` | Siostra obok | `h2 + p` |
| General | `~` | Wszystkie siostry | `h2 ~ p` |

---

## Część 2: Pseudo-klasy

Pseudo-klasy pozwalają na stylizowanie elementów na podstawie ich stanu lub pozycji[2].

### Pseudo-klasy Interakcji

#### `:hover` - Najedź myszką

```css
button:hover {
    background-color: darkblue;
    cursor: pointer;
}

a:hover {
    text-decoration: underline;
}
```

#### `:active` - Element naciśnięty

```css
button:active {
    transform: scale(0.98);
}
```

#### `:focus` - Element w focusie

```css
input:focus {
    border: 2px solid blue;
    outline: none;
}
```

#### `:visited` - Odwiedzone linki

```css
a:visited {
    color: purple;
}
```

### Pseudo-klasy Strukturalne

#### `:first-child` - Pierwsze dziecko

```css
li:first-child {
    font-weight: bold;
}
```

#### `:last-child` - Ostatnie dziecko

```css
li:last-child {
    border-bottom: none;
}
```

#### `:nth-child(n)` - n-te dziecko

```css
/* Każdy trzeci element */
li:nth-child(3n) {
    background-color: lightgray;
}

/* Parzyste wiersze */
tr:nth-child(even) {
    background-color: #f0f0f0;
}

/* Nieparzyste wiersze */
tr:nth-child(odd) {
    background-color: white;
}
```

**Wskazówki:**
- `2n` - co drugi element
- `2n+1` - nieparzyste
- `3n` - co trzeci
- `n+2` - od drugiego do końca

#### `:nth-of-type(n)` - n-ty element danego typu

```css
/* Drugi paragraf */
p:nth-of-type(2) {
    color: red;
}
```

### Pseudo-klasy Formularzy

#### `:checked` - Zaznaczone checkbox/radio

```css
input:checked {
    accent-color: green;
}
```

#### `:disabled` - Wyłączony element

```css
input:disabled {
    opacity: 0.5;
    cursor: not-allowed;
}
```

#### `:enabled` - Włączony element

```css
input:enabled {
    border: 1px solid blue;
}
```

#### `:valid` i `:invalid`

```css
input:valid {
    border: 2px solid green;
}

input:invalid {
    border: 2px solid red;
}
```

### Pseudo-klasy Logiczne

#### `:not(selector)` - Wszystko OPRÓCZ

```css
/* Wszystkie listę oprócz pierwszej */
li:not(:first-child) {
    border-top: 1px solid #ddd;
}

/* Wszystkie przyciski oprócz tych z klasą "primary" */
button:not(.primary) {
    background-color: gray;
}
```

---

## Część 3: Pseudo-elementy

Pseudo-elementy pozwalają na stylizowanie części elementu lub dodanie wirtualnych elementów[2].

### `::before` - Dodaj zawartość PRZED

```css
p::before {
    content: "➜ ";
    color: red;
}
```

```html
<p>Tekst artykułu</p>
```

**Wynik:** `➜ Tekst artykułu` (red strzałka na początku)

### `::after` - Dodaj zawartość PO

```css
a::after {
    content: " →";
    color: blue;
}
```

### `::first-line` - Stylizuj pierwszą linię

```css
p::first-line {
    font-weight: bold;
    text-transform: uppercase;
}
```

### `::first-letter` - Stylizuj pierwsze litery

```css
p::first-letter {
    font-size: 2em;
    font-weight: bold;
    color: red;
}
```

### `::selection` - Zaznaczony tekst

```css
::selection {
    background-color: yellow;
    color: black;
}

p::selection {
    background-color: blue;
    color: white;
}
```

---

## Część 4: Selektory Atrybutów

Wybierają elementy na podstawie ich atrybutów HTML[1].

### `[atryb]` - Posiada atrybut

```css
/* Wszystkie elementy z atrybutem data-role */
[data-role] {
    font-weight: bold;
}
```

### `[atryb="wartość"]` - Atryb równy wartości

```css
input[type="text"] {
    border: 1px solid blue;
}

a[target="_blank"] {
    color: purple;
}
```

### `[atryb~="wartość"]` - Atryb zawiera słowo

```css
/* Klasy zawierające "primary" */
[class~="primary"] {
    color: blue;
}
```

### `[atryb|="wartość"]` - Zaczyna się lub ma prefiks

```css
/* Tagi lang="en" lub lang="en-US" */
[lang|="en"] {
    font-family: "English Font";
}
```

### `[atryb^="wartość"]` - Zaczyna się od

```css
/* URLs zaczynające się od https */
a[href^="https"] {
    color: green;
}

/* Obrazki jpg */
img[src$=".jpg"] {
    border: 2px solid gold;
}
```

### `[atryb$="wartość"]` - Kończy się na

```css
/* Wszystkie linki do PDF */
a[href$=".pdf"] {
    background-image: url('pdf-icon.png');
}
```

### `[atryb*="wartość"]` - Zawiera gdziekolwiek

```css
/* Linki zawierające "example" */
a[href*="example"] {
    color: orange;
}
```

---

## Część 5: Specificity (Specyficzność)

Kiedy mamy wiele reguł CSS, której CSS ma być zastosowany? Odpowiedź: **Specificity**![1][2]

### Jak Obliczyć Specificity

Specificity liczy się na podstawie:

1. **Inline style** (atryb `style=""`) = 1000 punktów
2. **ID** (`#id`) = 100 punktów
3. **Klasa/Pseudo-klasa** (`.class`, `:hover`) = 10 punktów
4. **Element/Pseudo-element** (`p`, `::before`) = 1 punkt

### Przykłady Obliczania

```css
p                           /* 0001 */
.intro                      /* 0010 */
#nagłówek                   /* 0100 */
div p.intro                 /* 0011 */
#header .nav li             /* 0111 */
div#page .header span       /* 0113 */
```

**Wyższy numer = wyższa specyficzność = większy priorytet**

### Zasada Kaskady

```html
<p class="tekst" id="główny" style="color: green;">Jaki kolor?</p>
```

```css
p { color: blue; }              /* 0001 */
.tekst { color: red; }          /* 0010 */
#główny { color: yellow; }      /* 0100 */
```

**Wynik:** `green` (style inline ma najwyższy priorytet!)

### `!important` - Przebij Wszystko

```css
p {
    color: red !important;  /* To będzie zastosowane */
}

#główny {
    color: blue;            /* To zostanie zignorowane */
}
```

**Ostrzeżenie:** Używaj `!important` rzadko - to zła praktyka!

---

## Część 6: Praktyczne Przykłady

### Przykład 1: Stylizacja Tabeli

```html
<table>
    <tr>
        <th>Imię</th>
        <th>Wiek</th>
    </tr>
    <tr>
        <td>Anna</td>
        <td>25</td>
    </tr>
    <tr>
        <td>Marek</td>
        <td>30</td>
    </tr>
</table>
```

```css
/* Nagłówek */
th {
    background-color: #333;
    color: white;
    padding: 10px;
}

/* Wiersze na zmianę */
tr:nth-child(odd) {
    background-color: white;
}

tr:nth-child(even) {
    background-color: #f0f0f0;
}

/* Hover na wierszach */
tr:hover {
    background-color: #e0e0e0;
    cursor: pointer;
}

/* Ostatnia komórka */
td:last-child {
    text-align: right;
}
```

### Przykład 2: Menu Nawigacyjne

```html
<nav>
    <a href="/">Home</a>
    <a href="/about">O nas</a>
    <a href="/contact">Kontakt</a>
    <a href="https://external.com" target="_blank">Zewnętrzny link</a>
</nav>
```

```css
/* Wszystkie linki */
a {
    color: blue;
    text-decoration: none;
    padding: 10px;
    margin: 0 5px;
}

/* Hover */
a:hover {
    text-decoration: underline;
    color: darkblue;
}

/* Odwiedzone */
a:visited {
    color: purple;
}

/* Zewnętrzne linki */
a[target="_blank"]::after {
    content: " ↗";
    color: red;
}

/* Aktywny link */
a:active {
    font-weight: bold;
}
```

### Przykład 3: Formularz

```html
<form>
    <input type="text" required>
    <input type="email" required>
    <input type="password" required>
    <textarea disabled></textarea>
    <button>Wyślij</button>
</form>
```

```css
/* Wszystkie pola input */
input, textarea {
    padding: 10px;
    border: 1px solid #ccc;
    font-family: Arial;
}

/* Focus */
input:focus, textarea:focus {
    border: 2px solid blue;
    outline: none;
    box-shadow: 0 0 5px rgba(0,0,255,0.3);
}

/* Wyłączone */
textarea:disabled {
    background-color: #f0f0f0;
    cursor: not-allowed;
}

/* Przycisk */
button {
    padding: 10px 20px;
    background-color: green;
    color: white;
    border: none;
    cursor: pointer;
}

button:hover {
    background-color: darkgreen;
}

button:active {
    transform: scale(0.98);
}
```

---

## Część 7: Ćwiczenia

### Ćwiczenie 1: Stylizacja Listy

Utwórz HTML z listą:
```html
<ul>
    <li>Pierwszy element</li>
    <li>Drugi element</li>
    <li>Trzeci element</li>
    <li>Czwarty element</li>
</ul>
```

Zadanie:
1. Pierwsza `<li>` powinna być pogrubiona
2. Ostatnia `<li>` powinna mieć kolor czerwony
3. Parzyste elementy powinny mieć szare tło
4. Wszystkie elementy powinny zmienić tło na żółty przy hover

### Ćwiczenie 2: Pseudo-elementy

Utwórz cytat:
```html
<blockquote>To jest piękny cytat</blockquote>
```

Zadanie:
1. Dodaj cudzysłów `"` PRZED tekstem za pomocą `::before`
2. Dodaj cudzysłów `"` PO tekście za pomocą `::after`
3. Ustaw czcionkę italic
4. Dodaj szare tło

### Ćwiczenie 3: Selektory Atrybutów

Utwórz kilka linków:
```html
<a href="https://example.com">HTTPS Link</a>
<a href="http://example.com">HTTP Link</a>
<a href="/local">Lokalny Link</a>
<a href="#якорь">Anchor Link</a>
```

Zadanie:
1. Linki `https` powinny być zielone
2. Linki `http` powinny być pomarańczowe
3. Linki lokalne powinny być niebieskie
4. Wszystkie linki powinny mieć kurzor `pointer` przy hover

---

## Podsumowanie

W tym module nauczyliśmy się:

✅ **Kombinatory** - descendant, child, sibling  
✅ **Pseudo-klasy** - stany i pozycje (`:hover`, `:nth-child()`)  
✅ **Pseudo-elementy** - wirtualne części (`::before`, `::after`)  
✅ **Selektory atrybutów** - na podstawie cech HTML  
✅ **Specificity** - jak CSS decyduje co zastosować  
✅ **Praktyczne zastosowania** - tabele, menu, formularze  

---

## Zasoby Dodatkowe

- [MDN CSS Selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Selectors)
- [CSS Specificity Calculator](https://specificity.keegan.st/)
- [Pseudo-classes Guide](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes)

---

*Jesteś gotowy do Modułu 3? Nauczymy się Box Model w Głębi! 🚀*