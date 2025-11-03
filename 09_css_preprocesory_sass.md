# CSS Preprocesory - SASS/SCSS

## Wprowadzenie

SASS (Syntactically Awesome Style Sheets) to preprocesor CSS który dodaje funkcje, które brakuje w czystym CSS[1][2]. SCSS to rozszerzenie SASS z składnią bardziej podobną do CSS.

**Czego się nauczysz w tym module:**
- ✅ Co to preprocesory i dlaczego ich używać
- ✅ SASS vs SCSS - różnice
- ✅ Zmienne w SASS
- ✅ Zagnieżdżanie (Nesting)
- ✅ Mixiny - reużywalne bloki CSS
- ✅ Funkcje i operacje matematyczne
- ✅ Instalacja i kompilacja
- ✅ Praktyczne przykłady

---

## Część 1: Wprowadzenie do SASS

### Dlaczego SASS?

Czysty CSS:
- Brak zmiennych (trzeba pamiętać wartości)
- Powtarzający się kod
- Trudno się utrzymuje
- Brak organizacji

Z SASS:
- Zmienne
- Zagnieżdżanie
- Mixiny
- Funkcje
- Import plików
- Możliwość DRY (Don't Repeat Yourself)

### SCSS vs SASS

**SCSS (Sassy CSS)** - wygląda jak CSS:
```scss
$color: red;

body {
    color: $color;
}
```

**SASS** - mniej znaków:
```sass
$color: red

body
    color: $color
```

**Rekomendacja:** Używaj SCSS - bardziej popularne i łatwiejsze.

---

## Część 2: Zmienne (Variables)

Zmienne przechowują wartości do wielokrotnego użytku.

```scss
// Zmienne
$primary-color: #3498db;
$secondary-color: #2ecc71;
$spacing: 16px;
$font-stack: 'Helvetica', Arial, sans-serif;

// Użycie
body {
    font-family: $font-stack;
    color: $primary-color;
    margin: $spacing;
}

button {
    background-color: $primary-color;
    padding: $spacing / 2;
}
```

### Operacje Matematyczne

```scss
$base-size: 16px;

p {
    font-size: $base-size;
    margin-bottom: $base-size * 1.5;
    padding: $base-size / 2;
}
```

### Zakresy Zmiennych

```scss
$global: red;  // Globalna

.container {
    $local: blue;  // Lokalna w .container
    color: $local;
}

// $local NIE dostępna tutaj
```

---

## Część 3: Zagnieżdżanie (Nesting)

Zagnieżdżanie pozwala na hierarchiczną strukturę CSS.

```scss
// Czysty CSS (po kompilacji)
.card {
    padding: 20px;
    border-radius: 8px;
}

.card h2 {
    margin-top: 0;
    color: #333;
}

.card p {
    color: #666;
}

.card:hover {
    box-shadow: 0 8px 16px rgba(0,0,0,0.2);
}
```

**Z SCSS (bardziej czytelne):**
```scss
.card {
    padding: 20px;
    border-radius: 8px;

    h2 {
        margin-top: 0;
        color: #333;
    }

    p {
        color: #666;
    }

    &:hover {
        box-shadow: 0 8px 16px rgba(0,0,0,0.2);
    }
}
```

### `&` - Odwołanie do Rodzica

```scss
.button {
    background-color: blue;
    padding: 10px 20px;

    &:hover {                  // .button:hover
        background-color: darkblue;
    }

    &:active {                 // .button:active
        transform: scale(0.95);
    }

    &.large {                  // .button.large
        padding: 20px 40px;
    }

    &.disabled {               // .button.disabled
        opacity: 0.5;
        cursor: not-allowed;
    }
}
```

---

## Część 4: Mixiny (Mixins)

Mixiny to reużywalne bloki CSS.

### Proste Mixiny

```scss
// Definiuj
@mixin center-content {
    display: flex;
    justify-content: center;
    align-items: center;
}

// Użyj
.hero {
    height: 100vh;
    @include center-content;
}

.modal {
    @include center-content;
}
```

### Mixiny z Argumentami

```scss
@mixin button-style($bg-color, $text-color) {
    background-color: $bg-color;
    color: $text-color;
    padding: 10px 20px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
}

.btn-primary {
    @include button-style(blue, white);
}

.btn-secondary {
    @include button-style(gray, black);
}

.btn-danger {
    @include button-style(red, white);
}
```

### Mixiny z Domyślnymi Wartościami

```scss
@mixin box-shadow($x: 0, $y: 0, $blur: 8px, $color: rgba(0,0,0,0.1)) {
    box-shadow: $x $y $blur $color;
}

.card {
    @include box-shadow();                    // Domyślne
}

.card:hover {
    @include box-shadow(0, 4px, 16px, rgba(0,0,0,0.2));  // Custom
}
```

### Praktyczne Mixiny

```scss
// Media Query Mixin
@mixin mobile {
    @media (max-width: 768px) {
        @content;
    }
}

@mixin tablet {
    @media (min-width: 768px) and (max-width: 1024px) {
        @content;
    }
}

@mixin desktop {
    @media (min-width: 1024px) {
        @content;
    }
}

// Użycie
.container {
    width: 90%;
    
    @include mobile {
        width: 100%;
    }
    
    @include desktop {
        width: 1200px;
    }
}
```

---

## Część 5: Dziedziczenie (Extend)

Dziedziczenie pozwala na dzielenie CSS właściwości.

```scss
// Bazowe style
%button-base {
    padding: 10px 20px;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: all 0.3s;
}

// Rozszerzaj
.btn-primary {
    @extend %button-base;
    background-color: blue;
    color: white;
}

.btn-secondary {
    @extend %button-base;
    background-color: gray;
    color: black;
}
```

---

## Część 6: Import i Modularność

Podziel CSS na wiele plików!

```scss
// _variables.scss
$primary-color: #3498db;
$secondary-color: #2ecc71;

// _mixins.scss
@mixin center-content {
    display: flex;
    justify-content: center;
    align-items: center;
}

// _buttons.scss
@import 'variables';
@import 'mixins';

.button {
    background-color: $primary-color;
    @include center-content;
}

// style.scss (główny)
@import 'variables';
@import 'mixins';
@import 'buttons';
@import 'cards';
@import 'forms';
```

Każdy plik odpowiada za inną część projektu!

---

## Część 7: Instalacja i Kompilacja

### Instalacja Node.js

1. Pobierz z https://nodejs.org/
2. Zainstaluj

### Instalacja SASS

```bash
npm install -g sass
```

### Kompilacja

```bash
# Kompiluj jeden plik
sass input.scss output.css

# Obserwaj zmiany
sass --watch input.scss output.css

# Obserwaj cały folder
sass --watch scss:css
```

### W Edytorze Kodu

VS Code - rozszerzenie "Live Sass Compiler"
1. Pobierz z marketplace
2. Kliknij "Watch Sass"
3. CSS kompiluje się automatycznie

---

## Część 8: Praktyczne Przykłady

### Przykład 1: Kompleksny Project Setup

```scss
// _variables.scss
$primary: #3498db;
$secondary: #2ecc71;
$spacing-unit: 8px;
$font-stack: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;

// _mixins.scss
@mixin responsive($breakpoint) {
    @if $breakpoint == 'mobile' {
        @media (max-width: 480px) { @content; }
    }
    @if $breakpoint == 'tablet' {
        @media (max-width: 768px) { @content; }
    }
    @if $breakpoint == 'desktop' {
        @media (min-width: 1024px) { @content; }
    }
}

// _buttons.scss
@mixin button-variant($bg, $text) {
    background-color: $bg;
    color: $text;
    padding: $spacing-unit * 2 $spacing-unit * 3;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: all 0.3s;

    &:hover {
        transform: translateY(-2px);
        box-shadow: 0 4px 8px rgba(0,0,0,0.2);
    }
}

.button {
    font-family: $font-stack;
    
    &.primary {
        @include button-variant($primary, white);
    }

    &.secondary {
        @include button-variant($secondary, white);
    }
}

// style.scss
@import 'variables';
@import 'mixins';
@import 'buttons';

body {
    font-family: $font-stack;
    background-color: #f5f5f5;
    margin: 0;
}

.container {
    width: 90%;
    max-width: 1200px;
    margin: 0 auto;
    padding: $spacing-unit * 2;

    @include responsive('mobile') {
        padding: $spacing-unit;
    }
}
```

### Przykład 2: Theme System

```scss
// _themes.scss
$light-theme: (
    'primary': #3498db,
    'secondary': #2ecc71,
    'text': #333,
    'background': #fff,
);

$dark-theme: (
    'primary': #2980b9,
    'secondary': #27ae60,
    'text': #fff,
    'background': #1a1a1a,
);

@mixin apply-theme($theme) {
    color: map-get($theme, 'text');
    background-color: map-get($theme, 'background');
}

body {
    @include apply-theme($light-theme);

    &.dark-mode {
        @include apply-theme($dark-theme);
    }
}
```

---

## Część 9: Best Practices

1. **Organizuj Pliki** - różne pliki dla różnych komponentów
2. **Używaj Zmiennych** - dla kolorów, spacingów, czcionek
3. **DRY Principle** - nie powtarzaj się
4. **Mixiny dla Browsers Prefixes** - SASS może to zrobić za Ciebie
5. **Nie Zagnieżdżaj Zbyt Głęboko** - maksymalnie 3 poziomy
6. **Używaj Extend Dla Bazowych Style** - dla dużych pakietów
7. **Używaj Include Dla Logiki** - dla mixinów z działanemi

---

## Część 10: Ćwiczenia

### Ćwiczenie 1: Zmienne i Zagnieżdżanie

Stwórz SCSS z:
- Zmiennymi dla kolorów
- Zagnieżdżoną strukturą dla navigacji
- Pseudo-klasami z `&`

### Ćwiczenie 2: Mixiny

Utwórz mixiny do:
- Wyśrodkowania (`@mixin center-content`)
- Buttonów (`@mixin button-style`)
- Box shadow (`@mixin box-shadow`)

Użyj ich w CSS.

### Ćwiczenie 3: Modularny Project

Stwórz strukturę:
- `_variables.scss`
- `_buttons.scss`
- `_cards.scss`
- `style.scss` (import wszystkiego)

### Ćwiczenie 4: Responsive SCSS

Stwórz responsive design SCSS z:
- Mobilne breakpoints
- Tablet breakpoints
- Desktop breakpoints

Używaj mixinów dla media queries.

---

## Zaawansowane Koncepty (Bonus)

### Operacje na Listach

```scss
$sizes: (small: 10px, medium: 16px, large: 24px);

@each $name, $size in $sizes {
    .text-#{$name} {
        font-size: $size;
    }
}
```

### Funkcje

```scss
@function lighten-color($color, $percent) {
    @return mix(white, $color, $percent);
}

.button {
    background-color: $primary;

    &:hover {
        background-color: lighten-color($primary, 10%);
    }
}
```

---

## Podsumowanie

W tym module nauczyliśmy się:

✅ **Preprocesory** - dlaczego SASS jest lepszy  
✅ **Zmienne** - przechowywanie wartości  
✅ **Zagnieżdżanie** - hierarchiczna struktura  
✅ **Mixiny** - reużywalne bloki  
✅ **Dziedziczenie** - extend i %  
✅ **Modularność** - import plików  
✅ **Instalacja** - Node.js i SASS compiler  
✅ **Best Practices** - organizacja projektu  

---

## Zasoby Dodatkowe

- [SASS Official Guide](https://sass-lang.com/guide)
- [SCSS Compiler Online](https://jsoncrack.com/editor/scss-compiler)
- [SASS Playground](https://sass-lang.com/playground/)

---

*Jesteś gotowy do Modułu 10? Nauczymy się Best Practices i Projektowania! 🚀*