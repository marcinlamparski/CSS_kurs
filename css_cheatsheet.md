# CSS Cheatsheet - Ściąga Dla Uczniów

Szybka referencja najczęściej używanych właściwości CSS.

---

## 📐 Struktura CSS

```css
selektor {
    właściwość: wartość;
    właściwość: wartość;
}
```

**Pamiętaj:** Po każdej wartości stawiamy **średnik (;)**

---

## 🎯 Selektory

| Selektor | Przykład | Opis |
|----------|----------|------|
| Element | `p { }` | Wszystkie elementy `<p>` |
| Klasa | `.nazwa { }` | Elementy z `class="nazwa"` |
| ID | `#nazwa { }` | Element z `id="nazwa"` |
| Uniwersalny | `* { }` | Wszystkie elementy |
| Grupa | `h1, h2, p { }` | Wiele selectorów naraz |

---

## 🎨 Kolory

### Właściwość `color` - Kolor Tekstu

```css
p {
    color: red;              /* Nazwa koloru */
    color: #FF0000;          /* Heksadecymalny */
    color: rgb(255, 0, 0);   /* RGB */
}
```

### Właściwość `background-color` - Kolor Tła

```css
body {
    background-color: lightblue;
}

div {
    background-color: #F5F5F5;
}
```

### Popularne Kolory

```
red, blue, green, yellow, orange, purple, pink,
black, white, gray, brown, cyan, navy, lime, teal
```

---

## 🔤 Czcionka i Tekst

### Rodzaj Czcionki - `font-family`

```css
p {
    font-family: Arial, sans-serif;
    font-family: "Times New Roman", serif;
    font-family: "Courier New", monospace;
}
```

**Kategorie czcionek:**
- `serif` - Czcionki z zataczkami
- `sans-serif` - Czcionki bez zataczek
- `monospace` - Wszystkie znaki równej szerokości

### Rozmiar - `font-size`

```css
p {
    font-size: 16px;   /* Piksele (najpopularniejsze) */
    font-size: 1.5em;  /* Względem rodzica */
    font-size: 1rem;   /* Względem root (html) */
}
```

### Grubość - `font-weight`

```css
p {
    font-weight: normal;   /* lub 400 */
    font-weight: bold;     /* lub 700 */
    font-weight: 900;      /* Bardzo grube */
}
```

### Styl - `font-style`

```css
p {
    font-style: normal;   /* Zwykły */
    font-style: italic;   /* Kursywa */
}
```

### Wyrównanie - `text-align`

```css
h1 {
    text-align: left;     /* Wyrównaj do lewej (domyślnie) */
    text-align: center;   /* Wyśrodkuj */
    text-align: right;    /* Wyrównaj do prawej */
    text-align: justify;  /* Wyjustuj */
}
```

### Dekoracja - `text-decoration`

```css
a {
    text-decoration: none;       /* Usuń podkreślenie */
    text-decoration: underline;  /* Podkreślenie */
    text-decoration: line-through; /* Przekreślenie */
}
```

### Wysokość Linii - `line-height`

```css
p {
    line-height: 1.5;    /* 1.5x wysokości czcionki */
    line-height: 20px;   /* 20 pikseli */
}
```

---

## 📦 Model Pudełka

### Obramowanie - `border`

```css
div {
    border: 2px solid black;           /* Wszędzie 2px */
    border-top: 2px dashed red;        /* Tylko górny */
    border-right: 1px dotted blue;     /* Prawy */
    border-bottom: 3px solid green;    /* Dolny */
    border-left: 1px dotted orange;    /* Lewy */
}
```

**Style obramowania:** `solid`, `dashed`, `dotted`, `double`

### Zaokrąglenie - `border-radius`

```css
div {
    border-radius: 5px;              /* Wszystkie rogi */
    border-radius: 10px 20px;        /* Różne rogi */
    border-radius: 50%;              /* Koło */
}
```

### Wypełnienie (Wewnątrz) - `padding`

```css
div {
    padding: 20px;                    /* Wszędzie 20px */
    padding: 10px 20px;               /* Góra/dół 10px, Lewo/prawo 20px */
    padding: 10px 20px 30px 40px;     /* Góra, Prawo, Dół, Lewo */
    
    padding-top: 10px;
    padding-right: 15px;
    padding-bottom: 20px;
    padding-left: 25px;
}
```

### Margines (Na Zewnątrz) - `margin`

```css
div {
    margin: 20px;                     /* Wszędzie 20px */
    margin: 10px 20px;                /* Góra/dół 10px, Lewo/prawo 20px */
    margin: 10px 20px 30px 40px;      /* Góra, Prawo, Dół, Lewo */
    
    margin-top: 10px;
    margin-right: 15px;
    margin-bottom: 20px;
    margin-left: 25px;
    
    margin: 0 auto;                   /* Wyrównanie na środku */
}
```

### Rozmiar - `width` i `height`

```css
div {
    width: 300px;          /* Szerokość */
    height: 200px;         /* Wysokość */
    
    width: 50%;            /* Procent */
    max-width: 100%;       /* Maksymalna szerokość */
}
```

### Skreślenie Box Model - `box-sizing`

```css
div {
    box-sizing: border-box;   /* Szerokość = padding + border + content */
    box-sizing: content-box;  /* Szerokość = tylko content (domyślnie) */
}
```

---

## 📍 Display i Pozycjonowanie

### Display - `display`

```css
div {
    display: block;        /* Element blokowy (całą linię) */
    display: inline;       /* Element liniowy (obok siebie) */
    display: inline-block; /* Mieszany */
    display: none;         /* Ukryj element */
    display: flex;         /* Flexbox (omówimy później) */
    display: grid;         /* CSS Grid (omówimy później) */
}
```

### Tło - `background`

```css
div {
    background-color: lightblue;
    background-image: url('obraz.jpg');
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
}
```

### Cień - `box-shadow`

```css
div {
    box-shadow: 2px 2px 5px gray;       /* Offset-x, Offset-y, Blur, Kolor */
    box-shadow: 0 0 10px rgba(0,0,0,0.5); /* Z przezroczystością */
}
```

---

## 📋 Jednostki Długości

| Jednostka | Opis | Przykład |
|-----------|------|---------|
| `px` | Piksele (absolutne) | `16px` |
| `%` | Procent (względnie) | `50%` |
| `em` | Względem rodzica | `1.5em` |
| `rem` | Względem root `<html>` | `1rem` |
| `vh` | Wysokość viewportu | `50vh` |
| `vw` | Szerokość viewportu | `100vw` |

---

## 🎪 Pseudo-klasy (Szybki Przegląd)

```css
a:hover {
    color: red;              /* Najedź myszką */
}

button:active {
    transform: scale(0.95);  /* Kliknięcie */
}

input:focus {
    border: 2px solid blue;  /* Focus */
}
```

---

## 📱 Media Queries (Responsywny Design)

```css
/* Na ekranach mniejszych niż 768px */
@media (max-width: 768px) {
    body {
        font-size: 14px;
    }
    
    .sidebar {
        display: none;
    }
}
```

---

## 🔑 Najczęściej Robione Błędy

| Błąd | ❌ Źle | ✅ Dobrze |
|------|--------|----------|
| Brakujący średnik | `color: red` | `color: red;` |
| Spacje w nazwach | `class = "my class"` | `class="my-class"` |
| Zapomnienie cudzysłowów | `font-family: Times New Roman;` | `font-family: "Times New Roman";` |
| CSS liniowy | `<p style="color:red;">` | Użyj `.css` |
| Błędna ścieżka | `href="style.css"` | `href="./style.css"` (jeśli inna folder) |
| Zapomniana `<link>` | Brak połączenia | `<link rel="stylesheet" href="style.css">` |

---

## 🚀 Skrót do Powodzenia

### Krok 1: Utwórz HTML
```html
<!DOCTYPE html>
<html>
<head>
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <h1>Witaj!</h1>
</body>
</html>
```

### Krok 2: Stwórz CSS
```css
h1 {
    color: blue;
    text-align: center;
}
```

### Krok 3: Otwórz w Przeglądarce
```bash
# Kliknij dwa razy na plik HTML lub
open index.html
```

### Krok 4: Edytuj i Odśwież
- Edytuj `style.css`
- Naciśnij `Ctrl+R` (Ctrl+Shift+R na cache)
- Obserwuj zmiany

**Gotowe!** 🎉

---

## 📚 Szybkie Referencje Online

- [MDN CSS Reference](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference)
- [W3Schools CSS Tutorial](https://www.w3schools.com/css/)
- [CSS Tricks](https://css-tricks.com/)
- [Can I Use](https://caniuse.com/) - Wsparcie przeglądarek

---

**Zapisz tę ściągę i miej przy sobie podczas kodowania!** 💾