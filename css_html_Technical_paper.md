
#  Web Development CSS & HTML Concepts

##  Box Model

The **CSS Box Model** is the foundation of layout in CSS. Every HTML element is treated as a box consisting of:

- `Content`: The actual content (text, image, etc.)
- `Padding`: Space between content and border
- `Border`: Encloses the padding and content
- `Margin`: Space outside the border

```
+---------------------------+
|       Margin              |
|  +---------------------+  |
|  |     Border          |  |
|  |  +---------------+  |  |
|  |  |   Padding     |  |  |
|  |  | +----------+  |  |  |
|  |  | | Content  |  |  |  |
|  |  | +----------+  |  |  |
|  |  +---------------+  |  |
|  +---------------------+  |
+---------------------------+
```

##  Inline vs Block Elements

### Block Elements
- Take the full width available.
- Start on a new line.

**Examples:**  
`<div>`, `<p>`, `<h1>`–`<h6>`, `<section>`, `<article>`

### Inline Elements
- Take only as much width as needed.
- Do not start on a new line.

**Examples:**  
`<span>`, `<a>`, `<img>`, `<strong>`, `<em>`

## 📍 CSS Positioning

### `position: relative`
- Positioned relative to its **normal** position.

### `position: absolute`
- Positioned relative to the **nearest positioned ancestor** (`relative`, `absolute`, `fixed`, or `sticky`).

### `position: fixed`
- Stays fixed relative to the **viewport**.

### `position: sticky`
- Toggles between `relative` and `fixed` depending on scroll position.

##  Common CSS Structural Classes

These are often used for layout and containers:

```css
.container {
  max-width: 1200px;
  margin: 0 auto;
}

.row {
  display: flex;
  flex-wrap: wrap;
}

.col {
  flex: 1;
}
```

##  Common CSS Styling Classes

```css
.text-center {
  text-align: center;
}

.bg-light {
  background-color: #f8f9fa;
}

.mt-4 {
  margin-top: 1rem;
}

.p-2 {
  padding: 0.5rem;
}

.hidden {
  display: none;
}
```

##  CSS Specificity

CSS rules are applied based on specificity. Higher specificity wins.

| Selector Type     | Specificity Value |
|-------------------|-------------------|
| Inline style      | 1000              |
| ID (`#id`)        | 100               |
| Class (`.class`)  | 10                |
| Element (`div`)   | 1                 |

Example:

```css
/* Wins due to higher specificity */
#box { color: red; }

.box { color: blue; } /* This will be overridden */
```

##  CSS Responsive Queries

**Media queries** make designs responsive.

```css
/* Tablets */
@media (min-width: 768px) {
  body {
    background-color: lightblue;
  }
}

/* Desktops */
@media (min-width: 1024px) {
  body {
    background-color: lightgreen;
  }
}
```

##  Flexbox vs Grid

###  Flexbox (1D layout)
Best for aligning items in **a row or a column**.

```css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

###  CSS Grid (2D layout)
Great for **rows and columns**.

```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
}
```

##  Common `<head>` Meta Tags

```html
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<meta name="description" content="Your site description here" />
<title>My Website</title>
```

- `charset`: Character encoding
- `viewport`: Responsive behavior
- `description`: SEO and snippet
- `title`: Page title

##  Other Important Concepts

###  Normalize vs Reset
- **Reset**: Removes all default browser styles.
- **Normalize**: Keeps useful defaults while making rendering consistent.

###  `z-index`
- Controls stack order of elements (higher = on top)

```css
.modal {
  position: absolute;
  z-index: 999;
}
```

###  Units
- `px`, `em`, `rem`, `%`, `vh`, `vw`

###  Pseudo Classes
```css
a:hover {
  color: red;
}

input:focus {
  border-color: blue;
}
```

##  References

- [MDN Web Docs - CSS](https://developer.mozilla.org/en-US/docs/Web/CSS)
- [W3Schools CSS Tutorial](https://www.w3schools.com/css/)
- [CSS Tricks - A Complete Guide](https://css-tricks.com/)
- [Flexbox Froggy Game](https://flexboxfroggy.com/)
- [Grid Garden Game](https://cssgridgarden.com/)
