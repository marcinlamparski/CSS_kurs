# CSS Media Queries i Responsive Design

## Wprowadzenie

Responsive Design to umiejętność tworzenia stron, które wyglądają dobrze na wszystkich urządzeniach - od smartphonów do dużych monitorów[1][2].

**Czego się nauczysz w tym module:**
- ✅ Co to Media Queries
- ✅ Breakpointy (punkty przełączenia)
- ✅ Mobile-First vs Desktop-First
- ✅ Flexible Units (%, em, rem, vw)
- ✅ Responsive Images
- ✅ Praktyczne strategie responsive design
- ✅ Testowanie responsive design

---

## Część 1: Wprowadzenie do Responsive Design

### Dlaczego Responsive Design?

Statystyki:
- 60%+ użytkowników przegląda strony mobilnie
- Użytkownicy oczekują dobrej jakości na każdym urządzeniu
- Google faworyzuje responsive design w wyszukiwaniu

### Viewport Meta Tag

**WAŻNE:** Zawsze dodawaj to w `<head>`:

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
</head>
```

Bez tego, mobile viewports mogą być błędne!

---

## Część 2: Media Queries

Media Queries pozwalają na stosowanie CSS na podstawie charakterystyki urządzenia[1].

### Podstawowa Składnia

```css
@media (warunek) {
    /* CSS który dotyczy warunku */
}
```

### Media Query po Szerokości (Najczęstsze)

```css
/* Na ekranach mniejszych niż 768px */
@media (max-width: 768px) {
    body {
        font-size: 14px;
    }
}

/* Na ekranach większych niż 768px */
@media (min-width: 768px) {
    body {
        font-size: 16px;
    }
}

/* Między 768px a 1024px */
@media (min-width: 768px) and (max-width: 1024px) {
    body {
        font-size: 15px;
    }
}
```

### Warunki Media Query

| Warunek | Opis | Przykład |
|---------|------|---------|
| `min-width` | Minimum szerokość | `(min-width: 768px)` |
| `max-width` | Maksimum szerokość | `(max-width: 768px)` |
| `orientation` | Orientacja | `(orientation: landscape)` |
| `aspect-ratio` | Proporcja ekranu | `(aspect-ratio: 16/9)` |
| `color` | Czy kolor | `(color)` |
| `prefers-dark-mode` | Ciemny motyw | `(prefers-color-scheme: dark)` |

### Praktycznie

```css
/* Mobilne (domyślnie) */
body {
    font-size: 14px;
}

/* Tablet */
@media (min-width: 768px) {
    body {
        font-size: 15px;
    }
}

/* Desktop */
@media (min-width: 1024px) {
    body {
        font-size: 16px;
    }
}

/* Duży monitor */
@media (min-width: 1440px) {
    body {
        font-size: 18px;
    }
}
```

---

## Część 3: Breakpointy (Punkty Przełączenia)

Breakpointy to szerokości gdzie zmieniamy layout.

### Popularne Breakpointy

```css
/* Mobile First */
$mobile: 320px;
$tablet: 768px;
$desktop: 1024px;
$large: 1440px;
$xlarge: 1920px;
```

### Standardowe Breakpointy (Bootstrap)

- `xs`: < 576px (mobilne)
- `sm`: ≥ 576px (małe)
- `md`: ≥ 768px (średnie - tablet)
- `lg`: ≥ 992px (duże - desktop)
- `xl`: ≥ 1200px (bardzo duże)
- `xxl`: ≥ 1400px (ultra duże)

### Kiedy Zmieniać Breakpointy?

Zmień breakpointy gdy design wymaga zmian:

```css
/* Zwykle 2-3 breakpointy wystarczy */
@media (max-width: 768px) { /* Tablet */ }
@media (max-width: 480px) { /* Mobilne */ }
```

---

## Część 4: Mobile-First vs Desktop-First

### Mobile-First (REKOMENDOWANY!)

Piszesz CSS najpierw dla mobilnych, potem dodajesz dla większych ekranów.

```css
/* Mobilne (domyślnie) */
body {
    font-size: 14px;
    display: block;
}

nav {
    display: block;  /* Pionowo */
}

/* Tablet i wyżej */
@media (min-width: 768px) {
    body {
        font-size: 16px;
    }

    nav {
        display: flex;  /* Poziomo */
    }
}
```

**Zalety:**
- Prostszy kod
- Szybsze na mobilnych
- Domyślnie responsywne

### Desktop-First

Piszesz CSS dla dużych ekranów, potem zmniejszasz dla mniejszych.

```css
/* Desktop (domyślnie) */
body {
    font-size: 16px;
}

/* Tablet i mniejsze */
@media (max-width: 768px) {
    body {
        font-size: 15px;
    }
}
```

**Wada:** Dodatkowy CSS dla mobilnych (gorsze performance).

---

## Część 5: Flexible Layouts

Zamiast pisać breakpointy dla każdego piksela, używaj elastycznych jednostek.

### Użyj Procentów

```css
.container {
    width: 90%;           /* 90% szerokości rodzica */
    max-width: 1200px;    /* Ale max 1200px */
    margin: 0 auto;       /* Wyśrodkuj */
}
```

### Użyj `rem` dla Tekstu

```css
html {
    font-size: 16px;
}

h1 {
    font-size: 2rem;      /* 32px, ale skaluje się */
}

p {
    font-size: 1rem;      /* 16px */
    line-height: 1.6rem;  /* 25.6px */
}

@media (max-width: 768px) {
    html {
        font-size: 14px;  /* Wszystko skaluje się */
    }
}
```

### Użyj `em` dla Komponentów

```css
.button {
    padding: 0.75em 1.5em;
    font-size: 1em;
}

.button.small {
    font-size: 0.875em;
}

.button.large {
    font-size: 1.25em;
}
```

### Viewport Units

```css
h1 {
    font-size: 5vw;       /* 5% szerokości viewportu */
    line-height: 1.2;
}

.hero {
    height: 100vh;        /* Pełna wysokość okna */
}
```

---

## Część 6: Responsive Images

Obrazy powinny być responsywne!

### 1. `max-width: 100%`

```css
img {
    max-width: 100%;
    height: auto;         /* Zachowaj proporcje */
    display: block;
}
```

### 2. `srcset` - Różne Obrazy Na Różne Rozdzielczości

```html
<img
    src="image-small.jpg"
    srcset="image-small.jpg 480w,
            image-medium.jpg 800w,
            image-large.jpg 1200w"
    sizes="(max-width: 480px) 100vw,
           (max-width: 768px) 80vw,
           1200px"
    alt="Opis">
```

Browser automatycznie wybierze odpowiedni obraz!

### 3. `<picture>` - Różne Obrazy dla Różnych Warunków

```html
<picture>
    <source media="(max-width: 600px)" srcset="image-small.jpg">
    <source media="(max-width: 1200px)" srcset="image-medium.jpg">
    <img src="image-large.jpg" alt="Opis">
</picture>
```

### 4. `object-fit` - Jak Obrazek Dopasować

```css
img {
    width: 100%;
    height: 200px;
    object-fit: cover;    /* Przycnij, ale bez deformacji */
    object-fit: contain;  /* Pokaż całe, mogą być marginesy */
    object-fit: fill;     /* Deformuj aby wypełnić */
}
```

---

## Część 7: Praktyczne Przykłady

### Przykład 1: Responsywny Tekst

```css
/* Mobilne */
body {
    font-size: 14px;
    line-height: 1.5;
}

h1 {
    font-size: 1.5rem;    /* 21px */
    margin-bottom: 1rem;
}

p {
    font-size: 1rem;      /* 14px */
    margin-bottom: 1rem;
}

/* Tablet */
@media (min-width: 768px) {
    body {
        font-size: 15px;
    }

    h1 {
        font-size: 2rem;  /* 30px */
    }

    p {
        font-size: 1rem;  /* 15px */
    }
}

/* Desktop */
@media (min-width: 1024px) {
    body {
        font-size: 16px;
    }

    h1 {
        font-size: 2.5rem;  /* 40px */
    }
}
```

### Przykład 2: Responsywny Layout (Mobile-First)

```css
/* Mobilne - jedna kolumna */
.container {
    display: block;
}

.sidebar {
    margin-bottom: 20px;
}

/* Tablet - dwie kolumny */
@media (min-width: 768px) {
    .container {
        display: flex;
        gap: 20px;
    }

    .main {
        flex: 2;
    }

    .sidebar {
        flex: 1;
        margin-bottom: 0;
    }
}

/* Desktop - trzy kolumny */
@media (min-width: 1024px) {
    .container {
        display: grid;
        grid-template-columns: 1fr 2fr 1fr;
        gap: 30px;
    }
}
```

### Przykład 3: Ukrywanie Elementów

```css
/* Desktop menu */
.desktop-menu {
    display: none;
}

/* Mobilne menu */
.mobile-menu {
    display: block;
}

/* Na tabletach i wyżej pokaż desktop menu */
@media (min-width: 768px) {
    .desktop-menu {
        display: block;
    }

    .mobile-menu {
        display: none;
    }
}
```

### Przykład 4: Gęsty/Rzadki Layout

```css
/* Mobilne - gęsty */
.grid {
    display: grid;
    grid-template-columns: 1fr;
    gap: 10px;
    padding: 10px;
}

/* Tablet - medium */
@media (min-width: 768px) {
    .grid {
        grid-template-columns: repeat(2, 1fr);
        gap: 15px;
        padding: 15px;
    }
}

/* Desktop - rzadki */
@media (min-width: 1024px) {
    .grid {
        grid-template-columns: repeat(3, 1fr);
        gap: 20px;
        padding: 30px;
    }
}
```

---

## Część 8: Testowanie Responsive Design

### 1. DevTools (F12)

1. Naciśnij `F12`
2. Kliknij ikona mobilnego urządzenia
3. Zmień szerokość i testuj

### 2. Rzeczywiste Urządzenia

Zawsze testuj na prawdziwych telefonach i tabletach!

### 3. Online Narzędzia

- [Responsively App](https://responsively.app/)
- [Google Mobile-Friendly Test](https://search.google.com/test/mobile-friendly)

---

## Część 9: Ćwiczenia

### Ćwiczenie 1: Mobile-First

Stwórz prostą stronę:
- Mobilne: 1 kolumna
- Tablet: 2 kolumny
- Desktop: 3 kolumny

Używaj `@media (min-width:...)`

### Ćwiczenie 2: Ukrywanie Menu

Stwórz nawigację:
- Mobilne: hamburger ikona
- Desktop: pełne menu

Ukryj `nav a` na mobilnych, pokaż na dużych.

### Ćwiczenie 3: Responsywne Obrazy

Stwórz galeię gdzie:
- Mobilne: 1 obrazek w rzędzie
- Tablet: 2 obrazki
- Desktop: 4 obrazki

Użyj `grid-template-columns` z `@media`.

### Ćwiczenie 4: Font Scaling

Stwórz stronę gdzie:
- Mobilne: mniejsze fonty
- Tablet: średnie
- Desktop: duże

Użyj `rem` i zmień `html font-size` w breakpointach.

---

## Best Practices Responsive Design

1. **Mobile-First** - Zacznij od mobilnych
2. **Flexible Units** - Używaj %, em, rem, vw
3. **Test Often** - Testuj na wielu urządzeniach
4. **Optimize Images** - Używaj `srcset`
5. **Performance** - CSS Media Queries są szybkie
6. **Keep It Simple** - 2-3 breakpointy wystarczy
7. **Touch-Friendly** - Buttony minimum 44px x 44px

---

## Podsumowanie

W tym module nauczyliśmy się:

✅ **Media Queries** - warunki CSS  
✅ **Breakpointy** - punkty przełączenia layoutu  
✅ **Mobile-First** - najlepsza strategia  
✅ **Flexible Units** - procenty, em, rem, vw  
✅ **Responsive Images** - srcset, picture  
✅ **Praktyczne aplikacje** - layouty, tekst, galerie  
✅ **Testowanie** - DevTools i rzeczywiste urządzenia  

---

## Zasoby Dodatkowe

- [MDN Media Queries](https://developer.mozilla.org/en-US/docs/Web/CSS/Media_Queries)
- [Mobile-First CSS](https://developer.mozilla.org/en-US/docs/Mobile/Viewport_meta_tag)
- [Responsive Images Guide](https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/CSS_layout/Responsive_Design)

---

*Jesteś gotowy do Modułu 8? Nauczymy się Animacji i Przejść! 🚀*