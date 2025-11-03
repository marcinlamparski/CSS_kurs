# CSS Animacje i Przejścia

## Wprowadzenie

Animacje i przejścia dodają ruchu i interaktywności do stron internetowych. CSS pozwala na tworzenie gładkich animacji bez JavaScript![1][2]

**Czego się nauczysz w tym module:**
- ✅ Przejścia (Transitions) - proste animacje
- ✅ Animacje (Animations) - zaawansowane animacje
- ✅ Keyframes - definiowanie klatek animacji
- ✅ Timowanie i easing
- ✅ Transform - transformacje elementów
- ✅ Performance i best practices
- ✅ Praktyczne efekty

---

## Część 1: Przejścia (Transitions)

Przejścia to proste animacje między dwoma stanami[1].

### Podstawowa Składnia

```css
.button {
    background-color: blue;
    transition: background-color 0.3s;  /* Co się zmienia, jak długo */
}

.button:hover {
    background-color: red;              /* Nowy stan */
}
```

Przy hover, kolor się zmienia płynnie przez 0.3s zamiast natychmiast!

### `transition-property` - Co Animować

```css
div {
    transition-property: background-color;   /* Tylko kolor */
    transition-property: all;                /* Wszystkie właściwości */
    transition-property: width, height;      /* Wiele */
    transition-property: transform;          /* Transformacja */
}
```

### `transition-duration` - Jak Długo

```css
div {
    transition-duration: 0.3s;    /* 0.3 sekundy */
    transition-duration: 300ms;   /* 300 milisekund (równo) */
    transition-duration: 1s;      /* 1 sekunda */
}
```

### `transition-delay` - Opóźnienie

```css
div {
    transition-delay: 0.1s;       /* Czekaj 0.1s zanim zacznij */
}
```

### `transition-timing-function` - Tempo

```css
div {
    transition-timing-function: linear;        /* Równe */
    transition-timing-function: ease;          /* Naturalnie (domyślnie) */
    transition-timing-function: ease-in;       /* Powoli na początek */
    transition-timing-function: ease-out;      /* Powoli na koniec */
    transition-timing-function: ease-in-out;   /* Powoli wszędzie */
}
```

### Skrót `transition`

```css
div {
    transition: background-color 0.3s ease 0.1s;
    /* property duration timing-function delay */
}

/* Wszystkie właściwości */
div {
    transition: all 0.3s ease;
}
```

### Praktyczne Przykłady Przejść

```css
/* Button na hover */
button {
    background-color: blue;
    color: white;
    transition: all 0.3s ease;
    cursor: pointer;
}

button:hover {
    background-color: darkblue;
    transform: scale(1.05);
}

button:active {
    transform: scale(0.95);
}

/* Link z podkreśleniem */
a {
    text-decoration: none;
    border-bottom: 2px solid transparent;
    transition: border-color 0.3s;
}

a:hover {
    border-bottom-color: blue;
}

/* Kartę na hover */
.card {
    background-color: white;
    box-shadow: 0 2px 8px rgba(0,0,0,0.1);
    transition: box-shadow 0.3s ease;
}

.card:hover {
    box-shadow: 0 8px 16px rgba(0,0,0,0.2);
}
```

---

## Część 2: Transformacje (Transform)

Transform zmienia wygląd elementu bez wpływu na layout![2]

### `rotate` - Obróć

```css
div {
    transform: rotate(45deg);   /* Obróć 45 stopni */
    transform: rotate(-90deg);  /* Obróć -90 stopni */
    transform: rotateX(45deg);  /* Obróć wokół osi X */
    transform: rotateY(45deg);  /* Obróć wokół osi Y */
}
```

### `scale` - Przeskaluj

```css
div {
    transform: scale(2);        /* 2x większe */
    transform: scale(0.5);      /* Pół rozmiaru */
    transform: scaleX(1.5);     /* 1.5x szersze */
    transform: scaleY(0.7);     /* 0.7x wysokie */
}
```

### `translate` - Przesuń

```css
div {
    transform: translate(50px, 100px);  /* Przesuń 50px w prawo, 100px w dół */
    transform: translateX(50px);        /* Tylko poziomo */
    transform: translateY(-20px);       /* Tylko pionowo */
}
```

### `skew` - Skrzywienie

```css
div {
    transform: skew(45deg);     /* Skrzywienie */
    transform: skewX(10deg);    /* Tylko poziomo */
    transform: skewY(20deg);    /* Tylko pionowo */
}
```

### Kombinacja `transform`

```css
div {
    transform: rotate(45deg) scale(1.2) translate(50px, 100px);
}
```

### Transform z Transition

```css
button {
    transition: transform 0.3s ease;
}

button:hover {
    transform: scale(1.1) rotate(-5deg);
}
```

---

## Część 3: Animacje (Animations)

Animacje to bardziej zaawansowane, mogą mieć wiele etapów![2]

### Definiowanie Keyframes

```css
@keyframes slideIn {
    0% {
        opacity: 0;
        transform: translateX(-100px);
    }
    50% {
        opacity: 0.5;
    }
    100% {
        opacity: 1;
        transform: translateX(0);
    }
}
```

### Stosowanie Animacji

```css
div {
    animation-name: slideIn;            /* Która animacja */
    animation-duration: 1s;             /* Jak długo */
    animation-timing-function: ease-in-out; /* Tempo */
    animation-delay: 0.2s;              /* Opóźnienie */
    animation-iteration-count: 1;       /* Ile razy */
}
```

### `animation-iteration-count` - Ile Razy

```css
div {
    animation-iteration-count: 1;       /* Raz */
    animation-iteration-count: infinite; /* Na zawsze */
    animation-iteration-count: 3;       /* 3 razy */
}
```

### `animation-direction` - Kierunek

```css
div {
    animation-direction: normal;        /* Od 0% do 100% */
    animation-direction: reverse;       /* Od 100% do 0% */
    animation-direction: alternate;     /* 0->100->0->100... */
    animation-direction: alternate-reverse; /* 100->0->100->0... */
}
```

### `animation-fill-mode` - Stan Przed/Po

```css
div {
    animation-fill-mode: none;           /* Bez zmian */
    animation-fill-mode: forwards;       /* Zostań w 100% */
    animation-fill-mode: backwards;      /* Zacznij od 0% */
    animation-fill-mode: both;           /* Obie */
}
```

### Skrót `animation`

```css
div {
    animation: slideIn 1s ease-in-out 0.2s infinite alternate;
    /* name duration timing-function delay iteration-count direction */
}
```

---

## Część 4: Praktyczne Animacje

### Przykład 1: Pulsujący Guzik

```css
@keyframes pulse {
    0%, 100% {
        box-shadow: 0 0 0 0 rgba(255, 0, 0, 0.7);
    }
    50% {
        box-shadow: 0 0 0 10px rgba(255, 0, 0, 0);
    }
}

button {
    animation: pulse 2s infinite;
}
```

### Przykład 2: Ładowanie (Loading)

```css
@keyframes spin {
    0% {
        transform: rotate(0deg);
    }
    100% {
        transform: rotate(360deg);
    }
}

.loader {
    border: 4px solid #f3f3f3;
    border-top: 4px solid blue;
    border-radius: 50%;
    width: 40px;
    height: 40px;
    animation: spin 1s linear infinite;
}
```

### Przykład 3: Floating Item

```css
@keyframes float {
    0%, 100% {
        transform: translateY(0px);
    }
    50% {
        transform: translateY(-20px);
    }
}

.floating {
    animation: float 3s ease-in-out infinite;
}
```

### Przykład 4: Fade In

```css
@keyframes fadeIn {
    0% {
        opacity: 0;
    }
    100% {
        opacity: 1;
    }
}

.fade-in {
    animation: fadeIn 1s ease-in;
}
```

### Przykład 5: Slide Down

```css
@keyframes slideDown {
    0% {
        opacity: 0;
        transform: translateY(-30px);
    }
    100% {
        opacity: 1;
        transform: translateY(0);
    }
}

.slide-down {
    animation: slideDown 0.5s ease-out;
}
```

### Przykład 6: Bounce

```css
@keyframes bounce {
    0%, 100% {
        transform: translateY(0);
    }
    25% {
        transform: translateY(-10px);
    }
    50% {
        transform: translateY(0);
    }
    75% {
        transform: translateY(-5px);
    }
}

.bounce {
    animation: bounce 1s ease-in-out infinite;
}
```

### Przykład 7: Shake (Drżenie)

```css
@keyframes shake {
    0%, 100% {
        transform: translateX(0);
    }
    25% {
        transform: translateX(-10px);
    }
    75% {
        transform: translateX(10px);
    }
}

.shake {
    animation: shake 0.5s ease-in-out;
}
```

---

## Część 5: Performance

### CSS Animations są Szybkie!

Animacje CSS są renderowane przez GPU, nie CPU. Dlatego są szybkie.

### Użyj `transform` i `opacity`

Szybkie:
```css
.fast {
    animation: move 1s;
}

@keyframes move {
    0% { transform: translateX(0); }
    100% { transform: translateX(100px); }
}
```

Powolne (unikaj):
```css
.slow {
    animation: move 1s;
}

@keyframes move {
    0% { left: 0; }
    100% { left: 100px; }
}
```

### Włąż `will-change` Dla Zaawansowanych Animacji

```css
div {
    will-change: transform;
    animation: spin 2s infinite;
}
```

---

## Część 6: Ćwiczenia

### Ćwiczenie 1: Hover Transition

Stwórz buttona, który przy hover:
- Zmienia kolor
- Przeskalowuje się
- Zmienia cień

Wszystko animowane przez 0.3s.

### Ćwiczenie 2: Animowana Litera

Stwórz HTML z pismem "HELLO" gdzie każda litera ma inny `animation-delay`. Wszystkie animują się jednocześnie ale z opóźnieniem.

### Ćwiczenie 3: Loader Animation

Stwórz animowany loader (spinner):
- Okrąg który się obraca
- Animacja na zawsze
- Używa `animation: spin 1s linear infinite`

### Ćwiczenie 4: Fade In on Load

Stwórz stronę gdzie:
- Na ładowaniu strony, elementy `fade in`
- Każdy element ma inny `animation-delay`
- Po 2 sekundach elementy pojawiają się

---

## Best Practices Animacji

1. **Używaj Transitions** dla prostych zmian stanu (hover, focus)
2. **Używaj Animations** dla bardziej złożonych sekwencji
3. **Bądź Konserwatywny** - animacje powinny być subtelne
4. **Prefers Reduced Motion** - szanuj preferencje użytkownika:
   ```css
   @media (prefers-reduced-motion: reduce) {
       * {
           animation: none !important;
           transition: none !important;
       }
   }
   ```
5. **Performance First** - używaj `transform` i `opacity`
6. **Testuj** na wolnych urządzeniach

---

## Podsumowanie

W tym module nauczyliśmy się:

✅ **Transitions** - proste animacje między stanami  
✅ **Transform** - rotacja, skalowanie, przesunięcie  
✅ **Animations** - zaawansowane animacje  
✅ **Keyframes** - definiowanie klatek  
✅ **Timowanie** - duration, delay, easing  
✅ **Performance** - szybkie animacje CSS  
✅ **Praktyczne efekty** - pulse, bounce, fade, slide  

---

## Zasoby Dodatkowe

- [MDN Transitions](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Transitions)
- [MDN Animations](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Animations)
- [MDN Transform](https://developer.mozilla.org/en-US/docs/Web/CSS/transform)
- [Animista - Animation Library](https://animista.net/)

---

*Jesteś gotowy do Modułu 9? Nauczymy się SASS/SCSS - preprocesora CSS! 🚀*