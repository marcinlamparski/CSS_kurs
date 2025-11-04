# CSS Podstawy - Kurs Dla Początkujących

## Wprowadzenie

### Co to jest CSS?

**CSS** (ang. *Cascading Style Sheets* – Kaskadowe Arkusze Stylów) to język służący do opisywania wyglądu i formatowania stron internetowych napisanych w HTML. CSS definiuje, **jak** elementy HTML mają być wyświetlane na ekranie[1][2].

Jeśli HTML to szkielet strony internetowej, to **CSS to ubranie, które daje temu szkieletowi wygląd i styl**[3].

### Dlaczego stosujemy CSS?

Zamiast używać dodatkowych znaczników HTML do formatowania (co byłoby nieefektywne), CSS pozwala nam[1][2]:

1. **Oddzielić zawartość od prezentacji** - HTML odpowiada za strukturę, CSS za wygląd
2. **Zmienić wygląd całej strony w jednym miejscu** - modyfikujemy plik `.css` zamiast każdego znacznika HTML
3. **Zmniejszyć rozmiar plików** - kod HTML jest czystszy i lżejszy
4. **Łatwiej obsługiwać i utrzymywać witrynę** - zmiany są centralizowane
5. **Stworzyć responsywne strony** - które poprawnie wyglądają na różnych urządzeniach

### Przykład - Dlaczego CSS?

Bez CSS:
```html
<h1><font color="blue"><font face="Arial">Witaj na mojej stronie</font></font></h1>
<p><font color="blue"><font face="Arial">To jest paragraf tekstu.</font></font></p>
```

Z CSS:
```html
<!DOCTYPE html>
<html>
<head>
    <style>
        h1, p {
            color: blue;
            font-family: Arial;
        }
    </style>
</head>
<body>
    <h1>Witaj na mojej stronie</h1>
    <p>To jest paragraf tekstu.</p>
</body>
</html>
```

**Różnica?** Drugi kod jest czystszy, łatwiej się go edytuje, a zmiana kolorów dotyczy wszystkich elementów naraz[1].

---

## Część 1: Składnia CSS

### Struktura CSS

CSS składa się z **reguł**, a każda reguła ma prostą strukturę[2]:

```
selektor {
    właściwość: wartość;
    właściwość: wartość;
}
```

#### Elementy reguły CSS:

- **Selektor** - wskazuje, które elementy HTML mają być stylizowane
- **Właściwość** (ang. *property*) - określa, co chcemy zmienić (np. kolor, rozmiar czcionki)
- **Wartość** (ang. *value*) - określa, na co chcemy to zmienić (np. niebieski, 16px)

### Przykład:

```css
p {
    color: red;
    font-size: 18px;
}
```

| Element | Opis |
|---------|------|
| `p` | **Selektor** - każdy element `<p>` |
| `color` | **Właściwość** - zmienia kolor tekstu |
| `red` | **Wartość** - kolor czerwony |
| `font-size` | **Właściwość** - zmienia wielkość czcionki |
| `18px` | **Wartość** - 18 pikseli |

**Ważne:** Po każdej właściwości stawiamy średnik `;` - to koniec deklaracji![2]

---

## Część 2: Trzy Sposoby Dodawania CSS do HTML

Istnieją trzy główne metody dodawania CSS do strony[2][3]:

### 1. CSS Wewnętrzny (Internal CSS)

CSS wewnątrz tagu `<style>` w sekcji `<head>` dokumentu HTML.

```html
<!DOCTYPE html>
<html>
<head>
    <style>
        body {
            background-color: lightblue;
        }
        h1 {
            color: white;
            text-align: center;
        }
        p {
            font-family: Arial;
            font-size: 16px;
        }
    </style>
</head>
<body>
    <h1>Moja Strona</h1>
    <p>To jest paragraf.</p>
</body>
</html>
```

**Zalety:**
- Prosty do wdrożenia
- Styl dotyczy całej strony

**Wady:**
- Tylko dla jednej strony
- Mieszanie HTML z CSS

### 2. CSS Zewnętrzny (External CSS) - REKOMENDOWANY

Oddzielny plik `style.css` połączony z HTML za pomocą znacznika `<link>`.

**Plik: `index.html`**
```html
<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <h1>Moja Strona</h1>
    <p>To jest paragraf.</p>
</body>
</html>
```

**Plik: `style.css`**
```css
body {
    background-color: lightblue;
}

h1 {
    color: white;
    text-align: center;
}

p {
    font-family: Arial;
    font-size: 16px;
}
```

**Zalety:**
- Najczystszy kod
- Jeden plik CSS dla wielu stron HTML
- Łatwa konserwacja
- Szybszy ładunek strony (plik CSS jest cachowany)

**Wady:**
- Wymaga oddzielnego pliku

### 3. CSS Liniowy (Inline CSS)

CSS bezpośrednio w atrybucie `style` elementu HTML.

```html
<h1 style="color: blue; text-align: center;">Moja Strona</h1>
<p style="font-family: Arial; font-size: 16px;">To jest paragraf.</p>
```

**Zalety:**
- Szybkie testy i eksperymenty

**Wady:**
- Trudny do utrzymania
- Nieefektywny dla większych projektów
- Mieszanie HTML z CSS
- Ciężko zmienić styl dla wielu elementów[3]

**Rekomendacja:** Używaj **CSS Zewnętrznego** dla profesjonalnych projektów!

---

## Część 3: Selektory CSS

Selektor to sposób, w jaki mówimy CSS, które elementy HTML mają być stylizowane[2][4].

### 1. Selektor Elementu (Type Selector)

Stylizuje wszystkie elementy danego typu.

```css
p {
    color: navy;
}

h1 {
    font-size: 28px;
}
```

Efekt: Wszystkie `<p>` będą niebieskie, wszystkie `<h1>` będą duże.

### 2. Selektor Klasy (Class Selector)

Stylizuje elementy z konkretną klasą. Używamy `.` przed nazwą klasy[4].

```html
<!-- HTML -->
<p class="ważne">Ten tekst jest ważny!</p>
<p class="ważne">Ten też!</p>
<p>Ten tekst nie ma klasy.</p>
```

```css
/* CSS */
.ważne {
    color: red;
    font-weight: bold;
}
```

**Zalety:**
- Możemy przypisać tę samą klasę wielu elementom
- Możemy mieć wiele klas dla jednego elementu: `class="ważne destaczające"`

### 3. Selektor ID (ID Selector)

Stylizuje element z konkretnym ID. Używamy `#` przed nazwą ID[4].

```html
<!-- HTML -->
<h1 id="nagłówek">Główny Nagłówek</h1>
```

```css
/* CSS */
#nagłówek {
    color: green;
    font-size: 32px;
}
```

**Ważne:** ID musi być **unikalne** na stronie - jeden element, jedno ID![4]

### Porównanie Selectorów

| Selektor | Symbol | Cel | Specyficzność |
|----------|--------|-----|---|
| Elementu | żaden | Jeden typ elementu | Niska |
| Klasy | `.` | Wiele elementów | Średnia |
| ID | `#` | Jeden unikalny element | Wysoka |

---

## Część 4: Podstawowe Właściwości CSS

### 1. Kolor Tekstu - `color`

```css
p {
    color: red;           /* Nazwa koloru */
    color: #FF0000;       /* Kod heksadecymalny */
    color: rgb(255, 0, 0); /* Funkcja RGB */
}
```

**Sposoby określania koloru:**[5]
- **Nazwa:** `red`, `blue`, `green`, `navy`, itp.
- **Heksadecymalny:** `#FF0000` (łatwiej do zapamiętania: #RGB)
- **RGB:** `rgb(255, 0, 0)` (wartości 0-255)

### 2. Kolor Tła - `background-color`

```css
body {
    background-color: lightblue;
}

div {
    background-color: #F0F0F0;
}
```

### 3. Czcionka - `font-family`

```css
p {
    font-family: Arial, sans-serif;
}

h1 {
    font-family: "Times New Roman", serif;
}
```

**Ważne:** Jeśli nazwa czcionki ma spacje, opakowujemy ją w cudzysłów![5]

**Rodzaje czcionek:**
- `serif` - czcionki z zataczkami (tradycyjne)
- `sans-serif` - czcionki bez zataczek (nowoczesne)
- `monospace` - każdy znak zajmuje tyle samo miejsca

### 4. Rozmiar Czcionki - `font-size`

```css
p {
    font-size: 16px;
}

h1 {
    font-size: 32px;
}

small {
    font-size: 12px;
}
```

### 5. Grubość Czcionki - `font-weight`

```css
.zwykłe {
    font-weight: normal;  /* lub 400 */
}

.pogrubione {
    font-weight: bold;    /* lub 700 */
}

.wyjątkowo-grube {
    font-weight: 900;
}
```

### 6. Wyrównanie Tekstu - `text-align`

```css
h1 {
    text-align: center;   /* Wyśrodkuj */
}

p {
    text-align: left;     /* Wyrównaj do lewej (domyślnie) */
}

div {
    text-align: right;    /* Wyrównaj do prawej */
}

article {
    text-align: justify;  /* Wyjustuj */
}
```

---

## Część 5: Model Pudełka (Box Model) - Wprowadzenie

Każdy element HTML jest traktowany jako **pudełko**[6][7]. Model pudełka składa się z czterech warstw:

```
┌─────────────────────────────────────┐
│  MARGIN (Margines) - przestrzeń     │
│  ┌─────────────────────────────────┐│
│  │ BORDER (Obramowanie)            ││
│  │ ┌─────────────────────────────┐ ││
│  │ │ PADDING (Wypełnienie)       │ ││
│  │ │ ┌─────────────────────────┐ │ ││
│  │ │ │ CONTENT (Zawartość)     │ │ ││
│  │ │ │ Tekst, obrazy, itp.     │ │ ││
│  │ │ └─────────────────────────┘ │ ││
│  │ └─────────────────────────────┘ ││
│  └─────────────────────────────────┘│
└─────────────────────────────────────┘
```

### Wyjaśnienie Warstw[6][7]:

1. **Content** - Zawartość elementu (tekst, obraz)
2. **Padding** - Przestrzeń **wewnątrz** pudełka, między zawartością a obramowaniem
3. **Border** - Obramowanie wokół paddingu
4. **Margin** - Przestrzeń **na zewnątrz** pudełka, między obramowaniem a innymi elementami

### 1. Obramowanie - `border`

```css
p {
    border: 2px solid black;
}
```

Składnia: `border: SZEROKOŚĆ STYL KOLOR;`

**Style obramowania:**
- `solid` - linia ciągła
- `dashed` - linia przerywana
- `dotted` - linia punktowana

```css
div {
    border: 3px solid red;        /* Wszędzie 3px, czerwona, ciągła */
    border-top: 2px dotted blue;  /* Tylko górny brzeg */
}
```

### 2. Wypełnienie (Wewnętrzna Przestrzeń) - `padding`

```css
p {
    padding: 20px;                /* Wszędzie 20px */
    padding: 10px 20px;           /* Góra/dół 10px, Lewo/prawo 20px */
    padding: 10px 20px 30px 40px; /* Góra, Prawo, Dół, Lewo */
}
```

### 3. Margines (Zewnętrzna Przestrzeń) - `margin`

```css
div {
    margin: 20px;                 /* Wszędzie 20px */
    margin: 10px auto;            /* Wyrównanie na środku */
}

h1 {
    margin-bottom: 30px;          /* Tylko margines dolny */
}
```

---

## Część 6: Praktyczny Przykład

Stwórzmy prostą stronę z CSS:

**Plik: `index.html`**
```html
<!DOCTYPE html>
<html lang="pl">
<head>
    <meta charset="UTF-8">
    <title>Moja Pierwsza Strona CSS</title>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <h1>Witaj w CSS!</h1>
    
    <p class="intro">To jest moja pierwsza strona ze stylami CSS.</p>
    
    <div class="artykuł">
        <h2>Sekcja Artykułu</h2>
        <p>Lorem ipsum dolor sit amet. To jest przykładowy tekst.</p>
    </div>
    
    <footer id="stopka">
        <p>&copy; 2025 Moja Strona CSS</p>
    </footer>
</body>
</html>
```

**Plik: `style.css`**
```css
/* Stylu dla całego dokumentu */
body {
    background-color: #f0f0f0;
    font-family: Arial, sans-serif;
    margin: 0;
    padding: 20px;
}

/* Nagłówek */
h1 {
    color: #333;
    text-align: center;
    font-size: 32px;
    margin-bottom: 20px;
}

h2 {
    color: #666;
    font-size: 24px;
    border-bottom: 2px solid #007bff;
    padding-bottom: 10px;
}

/* Paragraf z klasą "intro" */
.intro {
    color: #007bff;
    font-size: 18px;
    font-weight: bold;
    text-align: center;
    margin: 20px 0;
}

/* Artykuł */
.artykuł {
    background-color: white;
    padding: 20px;
    border: 1px solid #ddd;
    border-radius: 5px;
    margin: 20px 0;
}

.artykuł p {
    color: #555;
    line-height: 1.6;
}

/* Stopka */
#stopka {
    text-align: center;
    color: #999;
    font-size: 12px;
    margin-top: 40px;
    padding-top: 20px;
    border-top: 1px solid #ddd;
}
```

**Wynik:** Strona z profesjonalnym wyglądem, separacją HTML od CSS, i łatwa do edycji!

---

## Część 7: Ćwiczenia Praktyczne - wykorzystaj kod (pliki html, css) z części 6

### Ćwiczenie 1: Zmiana Kolorów

Zmień kolory w pliku `style.css`:
- Zmień kolor `h1` na `#ff6b6b`
- Zmień `background-color` body na `#fffacd`
- Zmień kolor tekstu w `.intro` na `#2ecc71`

### Ćwiczenie 2: Dodaj Nową Klasę

Dodaj w HTML:
```html
<p class="ostrzeżenie">To jest ważne ostrzeżenie!</p>
```

Następnie w CSS stwórz:
```css
.ostrzeżenie {
    /* Twoja stylizacja */
}
```

Spróbuj dodać: czerwony tekst, żółte tło, pogrubienie, obramowanie.

### Ćwiczenie 3: Box Model

Stwórz nowy element `div` z klasą `karty`:
```html
<div class="karty">
    <h3>Karta</h3>
    <p>To jest zawartość karty.</p>
</div>
```

Stylizuj go używając:
- Białe tło (`background-color: white`)
- Padding wewnątrz (`padding: 15px`)
- Obramowanie (`border: 2px solid #ccc`)
- Margines (`margin: 10px`)

---

## Podsumowanie

W tej lekcji nauczyliśmy się:

✅ **Co to jest CSS** - Język do stylizowania HTML  
✅ **Dlaczego CSS** - Separacja zawartości od prezentacji  
✅ **Składnia CSS** - Selektory, właściwości, wartości  
✅ **Trzy sposoby dodawania CSS** - Zewnętrzny (najlepszy), wewnętrzny, liniowy  
✅ **Selektory** - Elementu, klasy, ID  
✅ **Podstawowe właściwości** - Kolory, czcionki, wyrównanie  
✅ **Model pudełka** - Margin, border, padding, content  

---

## Zasoby Dodatkowe

- [W3Schools CSS Tutorial](https://www.w3schools.com/css/)
- [MDN Web Docs - CSS](https://developer.mozilla.org/en-US/docs/Web/CSS)
- [CSS Tricks](https://css-tricks.com/)

---

**Gotowy do następnej lekcji? W następnej części nauczymy się:** Zaawansowanych selectorów, pseudoklas, displayu, flexboxa i jeszcze wiele więcej! 🚀

---

*Materiał przygotowany dla klasy 3 technikum informatycznego - Rok szkolny 2025*
