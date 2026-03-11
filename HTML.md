# HTML

## Q : What is diff in Fragment and Layout?
A : ### Fragment (HTML)

A **fragment** is a **small part of HTML**, not the full page.

Example:

```html
<h1>Hello</h1>
<p>Welcome</p>
```

This is called a fragment because it **does not contain `<html>`, `<head>`, or `<body>`**.

A full HTML page would be:

```html
<html>
<head>
  <title>Page</title>
</head>
<body>
  <h1>Hello</h1>
  <p>Welcome</p>
</body>
</html>
```

**Key point:**
Fragment = **partial HTML content**

---

### Layout (HTML)

**Layout** means **how elements are arranged on a webpage**.

Example layout:

```html
<header>Header</header>
<nav>Menu</nav>
<main>Main Content</main>
<aside>Sidebar</aside>
<footer>Footer</footer>
```

Layout is usually controlled using **CSS (flexbox, grid, position)**.

**Key point:**
Layout = **structure of the webpage**

---

### Difference

| Fragment            | Layout                 |
| ------------------- | ---------------------- |
| Small piece of HTML | Page structure         |
| Not a full document | Arranges page elements |

