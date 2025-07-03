Base Structure
```html
<!DOCTYPE html>    → Declares document type
<html>             → Root element
<head>             → Metadata (title, CSS, etc.)
<body>             → Visible content

<h1> to <h6>       → Headings
<p>                → Paragraph
<br>               → Line break
<hr>               → Horizontal line
<a href="#">       → Link
<img src="..." />  → Image

```

Forms
```html
<form>
  <label>Username</label>
  <input type="text" />

  <label>Password</label>
  <input type="password" />

  <button type="submit">Login</button>
</form>

```

Important tags
```html
<div>              → Generic container
<span>            → Inline container
<ul><li>          → Unordered list
<ol><li>          → Ordered list

```

CSS Essentials
```css
/* Tag selector */
p {
  color: blue;
}

/* Class selector */
.container {
  padding: 20px;
}

/* ID selector */
#loginBox {
  background-color: #f4f4f4;
}

```

Box Model
```
Content → Padding → Border → Margin
```

Common properties
```
color, background-color
font-size, font-family
width, height
margin, padding
border, border-radius
box-shadow

```

Layout
```css
.container {
  display: flex;
  justify-content: center;
  align-items: center;
}
```

Hover Example
```css
button:hover {
  background-color: #333;
  color: white;
}
```