# HTML + CSS Exam Snippets

Copy a block, paste it, then change text, colors, and sizes.
Every CSS block assumes this reset at the top of your CSS:

```css
* { margin: 0; padding: 0; box-sizing: border-box; }
body { font-family: Arial, sans-serif; line-height: 1.6; color: #333; }
img { max-width: 100%; display: block; }
a { text-decoration: none; color: inherit; }
```

---

## PART 1 — GOOGLE SEARCH PHRASES THAT WORK

Add "w3schools" or "mdn" to the end of a search to get clean, simple results.
The W3Schools "How To" section (w3schools.com/howto) has a copy-paste example for almost every component.

| Need | Search this |
|---|---|
| Any component | `w3schools how to <thing>` (e.g. `w3schools how to dropdown`) |
| Centering | `css center div horizontally vertically` |
| Navbar | `w3schools responsive top navigation` |
| Dropdown menu | `w3schools css dropdown navbar` |
| Hamburger menu | `css only hamburger menu checkbox` |
| Sidebar | `w3schools fixed sidebar` |
| Image gallery | `w3schools responsive image grid` |
| Image with text over it | `w3schools image text overlay` |
| Cards | `w3schools css cards` |
| Pricing table | `w3schools pricing table` |
| Forms | `w3schools css forms` |
| Login form | `w3schools login form` |
| Table styling | `w3schools css tables` |
| Footer stick to bottom | `css sticky footer flexbox` |
| Modal / popup | `css only modal target` |
| Accordion / FAQ | `html details summary` |
| Tooltip | `w3schools css tooltip` |
| Animations | `w3schools css animations keyframes` |
| Hover effects | `w3schools image hover effects` |
| Flexbox reference | `css tricks flexbox guide` |
| Grid reference | `css tricks grid guide` |
| Grid areas layout | `css grid template areas example` |
| Media queries | `w3schools media queries` |
| Google fonts | `fonts.google.com` (pick font → copy `<link>`) |
| Icons | `font awesome cdn` |
| Color palettes | `coolors.co` |
| Gradients | `cssgradient.io` |
| Box shadows | `css box shadow examples` |
| Any property | `mdn css <property>` (e.g. `mdn css position`) |
| Any tag | `mdn html <tag>` (e.g. `mdn html input`) |
| Validate HTML | `validator.w3.org` |

---

## PART 2 — PAGE LAYOUTS

### Centered container (use inside any section)
```css
.container { width: 90%; max-width: 1100px; margin: 0 auto; }
```

### Classic layout: header, sidebar, main, footer (Grid areas)
```html
<div class="layout">
  <header class="head">Header</header>
  <aside class="side">Sidebar</aside>
  <main class="content">Main content</main>
  <footer class="foot">Footer</footer>
</div>
```
```css
.layout {
  display: grid;
  grid-template-areas:
    "head head"
    "side content"
    "foot foot";
  grid-template-columns: 250px 1fr;
  min-height: 100vh;
}
.head    { grid-area: head;    background: #1e3a5f; color: #fff; padding: 20px; }
.side    { grid-area: side;    background: #eee; padding: 20px; }
.content { grid-area: content; padding: 20px; }
.foot    { grid-area: foot;    background: #1e3a5f; color: #fff; padding: 15px; text-align: center; }

@media (max-width: 768px) {
  .layout {
    grid-template-areas: "head" "content" "side" "foot";
    grid-template-columns: 1fr;
  }
}
```

### Two columns
```css
.two-col { display: flex; gap: 30px; }
.two-col > * { flex: 1; }
@media (max-width: 768px) { .two-col { flex-direction: column; } }
```

### Three columns
```css
.three-col { display: grid; grid-template-columns: repeat(3, 1fr); gap: 20px; }
@media (max-width: 768px) { .three-col { grid-template-columns: 1fr; } }
```

### Footer always at bottom of screen
```css
body { display: flex; flex-direction: column; min-height: 100vh; }
main { flex: 1; }
```

---

## PART 3 — NAVIGATION

### Basic navbar
```html
<nav class="navbar">
  <a href="#" class="logo">Logo</a>
  <ul class="nav-links">
    <li><a href="#">Home</a></li>
    <li><a href="#">About</a></li>
    <li><a href="#" class="active">Services</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
</nav>
```
```css
.navbar { display: flex; justify-content: space-between; align-items: center;
          padding: 15px 40px; background: #222; color: #fff; }
.logo { font-size: 1.5rem; font-weight: bold; }
.nav-links { display: flex; list-style: none; gap: 25px; }
.nav-links a:hover, .nav-links a.active { color: orange; }
```
Make it stick to top: add `position: sticky; top: 0; z-index: 100;` to `.navbar`.

### Dropdown menu
```html
<li class="dropdown">
  <a href="#">More ▾</a>
  <ul class="dropdown-menu">
    <li><a href="#">Option 1</a></li>
    <li><a href="#">Option 2</a></li>
  </ul>
</li>
```
```css
.dropdown { position: relative; }
.dropdown-menu { display: none; position: absolute; top: 100%; left: 0;
                 background: #fff; color: #333; list-style: none;
                 min-width: 160px; box-shadow: 0 4px 8px rgba(0,0,0,0.15); }
.dropdown-menu li a { display: block; padding: 10px 15px; }
.dropdown-menu li a:hover { background: #eee; }
.dropdown:hover .dropdown-menu { display: block; }
```

### Hamburger menu (CSS only, no JavaScript)
```html
<nav class="navbar">
  <a href="#" class="logo">Logo</a>
  <input type="checkbox" id="menu-toggle">
  <label for="menu-toggle" class="hamburger">☰</label>
  <ul class="nav-links">
    <li><a href="#">Home</a></li>
    <li><a href="#">About</a></li>
    <li><a href="#">Contact</a></li>
  </ul>
</nav>
```
```css
#menu-toggle, .hamburger { display: none; }
.hamburger { font-size: 1.8rem; cursor: pointer; }

@media (max-width: 768px) {
  .navbar { flex-wrap: wrap; }
  .hamburger { display: block; }
  .nav-links { display: none; width: 100%; flex-direction: column; gap: 10px; padding-top: 15px; }
  #menu-toggle:checked ~ .nav-links { display: flex; }
}
```

### Vertical sidebar menu
```css
.sidebar { width: 220px; height: 100vh; position: fixed; top: 0; left: 0;
           background: #222; color: #fff; padding-top: 20px; }
.sidebar a { display: block; padding: 12px 20px; }
.sidebar a:hover { background: #444; }
.main-with-sidebar { margin-left: 220px; padding: 20px; }
```

### Breadcrumbs
```html
<ul class="breadcrumb">
  <li><a href="#">Home</a></li>
  <li><a href="#">Products</a></li>
  <li>Shoes</li>
</ul>
```
```css
.breadcrumb { display: flex; list-style: none; gap: 8px; }
.breadcrumb li + li::before { content: "/"; margin-right: 8px; color: #999; }
.breadcrumb a { color: #0275d8; }
```

### Pagination
```html
<div class="pagination">
  <a href="#">&laquo;</a><a href="#" class="active">1</a><a href="#">2</a><a href="#">3</a><a href="#">&raquo;</a>
</div>
```
```css
.pagination { display: flex; gap: 5px; }
.pagination a { padding: 8px 14px; border: 1px solid #ddd; }
.pagination a.active, .pagination a:hover { background: #1e3a5f; color: #fff; }
```

---

## PART 4 — HERO / BANNER

### Background image with dark overlay
```html
<section class="hero">
  <h1>Big Title</h1>
  <p>Subtitle text</p>
  <a href="#" class="btn">Learn More</a>
</section>
```
```css
.hero { height: 80vh; display: flex; flex-direction: column;
        justify-content: center; align-items: center; text-align: center; color: #fff;
        background: linear-gradient(rgba(0,0,0,.5), rgba(0,0,0,.5)),
                    url("https://picsum.photos/1600/900") center/cover; }
.hero h1 { font-size: 3rem; }
```

### Split hero (text left, image right)
```html
<section class="split-hero">
  <div><h1>Title</h1><p>Text</p><a href="#" class="btn">Button</a></div>
  <img src="https://picsum.photos/600/400" alt="">
</section>
```
```css
.split-hero { display: flex; align-items: center; gap: 40px; padding: 60px 10%; }
.split-hero > * { flex: 1; }
@media (max-width: 768px) { .split-hero { flex-direction: column; } }
```

### Gradient background
```css
.gradient { background: linear-gradient(135deg, #667eea, #764ba2); color: #fff; }
```

---

## PART 5 — BUTTONS

```css
.btn { display: inline-block; padding: 12px 28px; background: #007bff; color: #fff;
       border: none; border-radius: 6px; cursor: pointer; font-size: 1rem;
       transition: background 0.3s; }
.btn:hover { background: #0056b3; }

.btn-outline { background: transparent; border: 2px solid #007bff; color: #007bff; }
.btn-outline:hover { background: #007bff; color: #fff; }

.btn-round { border-radius: 50px; }
.btn-full  { display: block; width: 100%; text-align: center; }
.btn-red   { background: #dc3545; }
.btn-green { background: #28a745; }
```

---

## PART 6 — CARDS & CONTENT BLOCKS

### Card grid
```html
<div class="cards">
  <div class="card">
    <img src="https://picsum.photos/400/250" alt="">
    <div class="card-body">
      <h3>Title</h3>
      <p>Description text.</p>
      <a href="#" class="btn">Read More</a>
    </div>
  </div>
  <!-- copy card -->
</div>
```
```css
.cards { display: grid; grid-template-columns: repeat(auto-fit, minmax(250px, 1fr)); gap: 25px; }
.card { background: #fff; border-radius: 8px; overflow: hidden;
        box-shadow: 0 2px 8px rgba(0,0,0,.1); transition: transform .3s; }
.card:hover { transform: translateY(-5px); }
.card-body { padding: 20px; }
```

### Profile / team card
```html
<div class="profile">
  <img src="https://i.pravatar.cc/150" alt="">
  <h3>Name</h3>
  <p class="role">Job Title</p>
  <p>Short bio.</p>
</div>
```
```css
.profile { text-align: center; padding: 25px; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,.1); }
.profile img { width: 120px; height: 120px; border-radius: 50%; object-fit: cover; margin: 0 auto 15px; }
.role { color: #888; }
```

### Pricing table
```html
<div class="pricing">
  <div class="plan">
    <h3>Basic</h3>
    <p class="price">$9<span>/mo</span></p>
    <ul><li>Feature 1</li><li>Feature 2</li><li>Feature 3</li></ul>
    <a href="#" class="btn">Choose</a>
  </div>
  <div class="plan featured"> ... </div>
  <div class="plan"> ... </div>
</div>
```
```css
.pricing { display: grid; grid-template-columns: repeat(auto-fit, minmax(220px, 1fr)); gap: 20px; }
.plan { text-align: center; padding: 30px; border: 1px solid #ddd; border-radius: 8px; }
.plan.featured { border: 2px solid #007bff; transform: scale(1.05); }
.price { font-size: 2.5rem; font-weight: bold; margin: 15px 0; }
.price span { font-size: 1rem; color: #888; }
.plan ul { list-style: none; margin-bottom: 20px; }
.plan li { padding: 8px 0; border-bottom: 1px solid #eee; }
```

### Testimonial / quote
```html
<blockquote class="testimonial">
  <p>"This is a great product, would recommend."</p>
  <cite>— Customer Name</cite>
</blockquote>
```
```css
.testimonial { background: #f4f6f8; border-left: 5px solid #007bff; padding: 20px 25px; font-style: italic; }
.testimonial cite { display: block; margin-top: 10px; font-style: normal; font-weight: bold; }
```

### Feature boxes with icons (needs Font Awesome, see Part 12)
```html
<div class="features">
  <div class="feature"><i class="fa-solid fa-bolt"></i><h3>Fast</h3><p>Text</p></div>
  <div class="feature"><i class="fa-solid fa-lock"></i><h3>Secure</h3><p>Text</p></div>
  <div class="feature"><i class="fa-solid fa-heart"></i><h3>Loved</h3><p>Text</p></div>
</div>
```
```css
.features { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 25px; text-align: center; }
.feature i { font-size: 2.5rem; color: #007bff; margin-bottom: 10px; }
```

### Stats / counters row
```html
<div class="stats">
  <div><h2>500+</h2><p>Clients</p></div>
  <div><h2>20</h2><p>Years</p></div>
  <div><h2>99%</h2><p>Happy</p></div>
</div>
```
```css
.stats { display: flex; justify-content: space-around; text-align: center; padding: 40px; background: #1e3a5f; color: #fff; }
```

### Timeline
```html
<div class="timeline">
  <div class="event"><h4>2020</h4><p>Something happened.</p></div>
  <div class="event"><h4>2022</h4><p>Something else.</p></div>
</div>
```
```css
.timeline { border-left: 3px solid #007bff; padding-left: 25px; }
.event { position: relative; margin-bottom: 25px; }
.event::before { content: ""; position: absolute; left: -33px; top: 5px;
                 width: 13px; height: 13px; border-radius: 50%; background: #007bff; }
```

### Alert boxes
```html
<div class="alert success">Saved successfully.</div>
<div class="alert error">Something went wrong.</div>
<div class="alert warning">Be careful.</div>
```
```css
.alert { padding: 15px; border-radius: 5px; margin-bottom: 10px; }
.success { background: #d4edda; color: #155724; }
.error   { background: #f8d7da; color: #721c24; }
.warning { background: #fff3cd; color: #856404; }
```

### Badge / tag
```css
.badge { display: inline-block; padding: 3px 10px; border-radius: 12px; background: #007bff; color: #fff; font-size: .8rem; }
```

### Progress bar
```html
<div class="progress"><div class="bar" style="width: 70%;">70%</div></div>
```
```css
.progress { background: #ddd; border-radius: 20px; overflow: hidden; }
.bar { background: #28a745; color: #fff; text-align: center; padding: 4px 0; }
```

---

## PART 7 — IMAGES & MEDIA

### Image gallery grid
```html
<div class="gallery">
  <img src="https://picsum.photos/400/300?1" alt="">
  <img src="https://picsum.photos/400/300?2" alt="">
  <img src="https://picsum.photos/400/300?3" alt="">
  <img src="https://picsum.photos/400/300?4" alt="">
</div>
```
```css
.gallery { display: grid; grid-template-columns: repeat(auto-fill, minmax(200px, 1fr)); gap: 10px; }
.gallery img { width: 100%; height: 200px; object-fit: cover; border-radius: 6px; transition: transform .3s; }
.gallery img:hover { transform: scale(1.05); }
```

### Text on top of image
```html
<div class="img-box">
  <img src="https://picsum.photos/600/400" alt="">
  <div class="img-text">Caption</div>
</div>
```
```css
.img-box { position: relative; }
.img-text { position: absolute; bottom: 0; left: 0; right: 0;
            background: rgba(0,0,0,.6); color: #fff; padding: 15px; }
```

### Hover overlay on image
```css
.img-box .overlay { position: absolute; inset: 0; background: rgba(0,0,0,.6); color: #fff;
                    display: flex; justify-content: center; align-items: center;
                    opacity: 0; transition: opacity .3s; }
.img-box:hover .overlay { opacity: 1; }
```

### Figure with caption
```html
<figure>
  <img src="pic.jpg" alt="description">
  <figcaption>Caption text</figcaption>
</figure>
```

### Round image / avatar
```css
.avatar { width: 100px; height: 100px; border-radius: 50%; object-fit: cover; }
```

### Video, audio, YouTube, Google Map
```html
<video src="video.mp4" controls width="100%"></video>

<audio src="song.mp3" controls></audio>

<!-- YouTube: on YouTube click Share → Embed → copy -->
<iframe width="560" height="315" src="https://www.youtube.com/embed/VIDEO_ID" allowfullscreen></iframe>

<!-- Google Maps: on Google Maps click Share → Embed a map → copy -->
<iframe src="PASTE_EMBED_URL" width="100%" height="300" style="border:0;" loading="lazy"></iframe>
```

### Responsive iframe (keeps 16:9)
```css
iframe { width: 100%; aspect-ratio: 16 / 9; border: 0; }
```

---

## PART 8 — FORMS

### Login form (centered on page)
```html
<div class="login-page">
  <form class="login-box">
    <h2>Login</h2>
    <input type="text" placeholder="Username" required>
    <input type="password" placeholder="Password" required>
    <label><input type="checkbox"> Remember me</label>
    <button type="submit" class="btn btn-full">Login</button>
    <p class="small">Don't have an account? <a href="#">Sign up</a></p>
  </form>
</div>
```
```css
.login-page { min-height: 100vh; display: flex; justify-content: center; align-items: center; background: #f4f6f8; }
.login-box { background: #fff; padding: 40px; width: 350px; border-radius: 10px;
             box-shadow: 0 4px 15px rgba(0,0,0,.1); display: flex; flex-direction: column; gap: 15px; }
.login-box h2 { text-align: center; }
.login-box input[type="text"], .login-box input[type="password"] {
  padding: 12px; border: 1px solid #ccc; border-radius: 6px; }
.small { font-size: .9rem; text-align: center; }
.small a { color: #007bff; }
```

### All input types (for reference)
```html
<input type="text">       <input type="email">     <input type="password">
<input type="number" min="1" max="10">            <input type="tel">
<input type="date">       <input type="time">      <input type="color">
<input type="range" min="0" max="100">            <input type="file">
<input type="url">        <input type="search">
<input type="checkbox">   <input type="radio" name="group">
<input type="submit" value="Send">                <input type="reset">
<textarea rows="4"></textarea>
<select><option>One</option><option selected>Two</option></select>
```
Useful attributes: `required`, `placeholder`, `value`, `disabled`, `readonly`, `checked`, `maxlength`, `pattern`.

### Grouping fields
```html
<fieldset>
  <legend>Personal Info</legend>
  ...inputs...
</fieldset>
```

### Two inputs side by side
```css
.form-row { display: flex; gap: 15px; }
.form-row > * { flex: 1; }
```

### General form styling
```css
input, select, textarea { width: 100%; padding: 10px; border: 1px solid #ccc;
                          border-radius: 6px; font-family: inherit; font-size: 1rem; }
input:focus, textarea:focus, select:focus { outline: none; border-color: #007bff;
                                            box-shadow: 0 0 5px rgba(0,123,255,.4); }
input[type="checkbox"], input[type="radio"] { width: auto; }
label { display: block; margin: 10px 0 5px; font-weight: bold; }
```

---

## PART 9 — TABLES

```html
<table class="styled-table">
  <caption>Table Title</caption>
  <thead><tr><th>Name</th><th>Score</th><th>Grade</th></tr></thead>
  <tbody>
    <tr><td>Alice</td><td>92</td><td>A</td></tr>
    <tr><td>Bob</td><td>85</td><td>B</td></tr>
  </tbody>
  <tfoot><tr><td colspan="2">Average</td><td>A-</td></tr></tfoot>
</table>
```
```css
.styled-table { width: 100%; border-collapse: collapse; }
.styled-table th, .styled-table td { padding: 12px; border: 1px solid #ddd; text-align: left; }
.styled-table thead { background: #1e3a5f; color: #fff; }
.styled-table tbody tr:nth-child(even) { background: #f4f6f8; }
.styled-table tbody tr:hover { background: #e2e8f0; }
caption { font-weight: bold; margin-bottom: 10px; }
```
Merge cells: `colspan="2"` (across), `rowspan="2"` (down).
Scroll table on phone: wrap it in `<div style="overflow-x:auto;">`.

---

## PART 10 — INTERACTIVE WITHOUT JAVASCRIPT

### FAQ / accordion
```html
<details>
  <summary>What is your return policy?</summary>
  <p>You can return items within 30 days.</p>
</details>
```
```css
details { border: 1px solid #ddd; border-radius: 6px; padding: 12px; margin-bottom: 10px; }
summary { font-weight: bold; cursor: pointer; }
details[open] summary { margin-bottom: 10px; }
```

### Modal popup
```html
<a href="#popup" class="btn">Open Popup</a>
<div id="popup" class="modal">
  <div class="modal-box">
    <a href="#" class="close">&times;</a>
    <h2>Hello</h2>
    <p>Popup content.</p>
  </div>
</div>
```
```css
.modal { display: none; position: fixed; inset: 0; background: rgba(0,0,0,.6);
         justify-content: center; align-items: center; z-index: 1000; }
.modal:target { display: flex; }
.modal-box { background: #fff; padding: 30px; border-radius: 8px; width: 90%; max-width: 400px; position: relative; }
.close { position: absolute; top: 10px; right: 15px; font-size: 1.5rem; }
```

### Tooltip
```html
<span class="tooltip">Hover me<span class="tip">Tooltip text</span></span>
```
```css
.tooltip { position: relative; cursor: pointer; border-bottom: 1px dotted; }
.tip { visibility: hidden; position: absolute; bottom: 125%; left: 50%; transform: translateX(-50%);
       background: #333; color: #fff; padding: 5px 10px; border-radius: 4px; white-space: nowrap; }
.tooltip:hover .tip { visibility: visible; }
```

### Smooth scroll to sections
```css
html { scroll-behavior: smooth; }
```
Link: `<a href="#about">About</a>` → target: `<section id="about">`.

---

## PART 11 — FOOTER

### Multi-column footer
```html
<footer class="footer">
  <div class="footer-cols">
    <div><h4>About</h4><p>Short company description.</p></div>
    <div><h4>Links</h4><ul><li><a href="#">Home</a></li><li><a href="#">About</a></li></ul></div>
    <div><h4>Contact</h4><p>Email: info@site.com</p><p>Phone: 123-456-7890</p></div>
  </div>
  <p class="copyright">&copy; 2026 Site Name</p>
</footer>
```
```css
.footer { background: #222; color: #ccc; padding: 40px 10% 20px; }
.footer-cols { display: grid; grid-template-columns: repeat(auto-fit, minmax(200px, 1fr)); gap: 30px; }
.footer h4 { color: #fff; margin-bottom: 10px; }
.footer ul { list-style: none; }
.footer a:hover { color: orange; }
.copyright { text-align: center; border-top: 1px solid #444; margin-top: 30px; padding-top: 15px; }
```

---

## PART 12 — FONTS & ICONS

### Google Fonts
Go to fonts.google.com → pick font → "Get embed code" → paste in `<head>`:
```html
<link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;600&display=swap" rel="stylesheet">
```
```css
body { font-family: 'Poppins', sans-serif; }
```
Good choices: Poppins, Roboto, Open Sans, Montserrat, Lato, Playfair Display (headings).

### Font Awesome icons
Search "font awesome cdn" → copy link into `<head>`:
```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.0/css/all.min.css">
```
Use:
```html
<i class="fa-solid fa-house"></i>
<i class="fa-solid fa-envelope"></i>
<i class="fa-brands fa-facebook"></i>
<i class="fa-brands fa-instagram"></i>
```
Search icon names at fontawesome.com/icons.

### HTML symbols (no library needed)
`&copy;` © `&reg;` ® `&trade;` ™ `&rarr;` → `&larr;` ← `&times;` × `&hearts;` ♥ `&#9733;` ★ `&nbsp;` (space) `&amp;` & `&lt;` < `&gt;` >

---

## PART 13 — CSS EFFECTS

### Transitions & hover
```css
.box { transition: all 0.3s ease; }
.box:hover { transform: scale(1.05); }          /* grow */
.box:hover { transform: translateY(-5px); }     /* lift */
.box:hover { transform: rotate(5deg); }         /* tilt */
.box:hover { box-shadow: 0 8px 20px rgba(0,0,0,.2); }
.box:hover { opacity: .8; }
img:hover  { filter: grayscale(100%); }
```

### Keyframe animations
```css
@keyframes fadeIn { from { opacity: 0; } to { opacity: 1; } }
@keyframes slideUp { from { transform: translateY(40px); opacity: 0; } to { transform: translateY(0); opacity: 1; } }
@keyframes pulse { 0%,100% { transform: scale(1); } 50% { transform: scale(1.1); } }
@keyframes spin { to { transform: rotate(360deg); } }

.hero h1 { animation: slideUp 1s ease; }
.icon    { animation: pulse 2s infinite; }
.loader  { width: 40px; height: 40px; border: 4px solid #ddd; border-top-color: #007bff;
           border-radius: 50%; animation: spin 1s linear infinite; }
```

### Shadows
```css
box-shadow: 0 2px 8px rgba(0,0,0,.1);          /* soft */
box-shadow: 0 10px 25px rgba(0,0,0,.2);        /* deep */
text-shadow: 2px 2px 4px rgba(0,0,0,.5);       /* text */
```

### Gradients
```css
background: linear-gradient(to right, #ff7e5f, #feb47b);
background: linear-gradient(135deg, #667eea, #764ba2);
background: radial-gradient(circle, #fff, #ccc);
```

### Glass effect
```css
.glass { background: rgba(255,255,255,.2); backdrop-filter: blur(10px);
         border: 1px solid rgba(255,255,255,.3); border-radius: 12px; }
```

### Custom list bullets
```css
ul.check { list-style: none; }
ul.check li::before { content: "✔ "; color: green; }
```

### Custom scrollbar (Chrome)
```css
::-webkit-scrollbar { width: 8px; }
::-webkit-scrollbar-thumb { background: #888; border-radius: 4px; }
```

---

## PART 14 — CENTERING (the most googled thing)

```css
/* text */
.center-text { text-align: center; }

/* block horizontally */
.center-block { width: 60%; margin: 0 auto; }

/* anything, both ways (flex) */
.center-flex { display: flex; justify-content: center; align-items: center; height: 100vh; }

/* anything, both ways (grid) */
.center-grid { display: grid; place-items: center; height: 100vh; }

/* absolute */
.center-abs { position: absolute; top: 50%; left: 50%; transform: translate(-50%, -50%); }
```

---

## PART 15 — QUICK REFERENCE

### Flexbox
| Property | Values |
|---|---|
| `display` | `flex` |
| `flex-direction` | `row`, `column` |
| `justify-content` | `flex-start`, `center`, `flex-end`, `space-between`, `space-around`, `space-evenly` |
| `align-items` | `stretch`, `center`, `flex-start`, `flex-end` |
| `flex-wrap` | `wrap`, `nowrap` |
| `gap` | `20px` |
| child `flex` | `1` (fill equally), `0 0 200px` (fixed 200px) |
| child `order` | `1`, `2`... |
| child `align-self` | same as align-items, for one item |

### Grid
| Property | Example |
|---|---|
| `grid-template-columns` | `200px 1fr`, `repeat(3, 1fr)`, `repeat(auto-fit, minmax(250px, 1fr))` |
| `grid-template-rows` | `auto 1fr auto` |
| `gap` | `20px` |
| `grid-template-areas` | see Part 2 |
| child `grid-column` | `1 / 3` or `span 2` |
| child `grid-row` | `span 2` |
| `place-items` | `center` |

### Position
| Value | Behavior |
|---|---|
| `static` | default |
| `relative` | moved from normal spot; anchor for absolute children |
| `absolute` | placed inside nearest positioned parent (`top/right/bottom/left`) |
| `fixed` | stuck to screen while scrolling |
| `sticky` | normal until scroll hits it, then sticks (`top: 0`) |
| `z-index` | higher number = on top (only works on positioned elements) |

### Units
| Unit | Meaning |
|---|---|
| `px` | fixed pixels |
| `%` | percent of parent |
| `rem` | relative to root font size (1rem = 16px default) |
| `em` | relative to element's font size |
| `vh` / `vw` | percent of screen height / width |
| `fr` | fraction of free space (grid only) |

### Display
`block` (full width, new line) · `inline` (in text, no width/height) · `inline-block` (in line but sizable) · `none` (hidden) · `flex` · `grid`

### Selectors
```css
*                 /* everything */
h1, h2            /* both */
.nav a            /* a inside .nav */
.nav > a          /* direct child only */
h2 + p            /* p right after h2 */
a:hover  a:active  input:focus
li:first-child  li:last-child  li:nth-child(odd)  li:nth-child(3)
p::first-letter  p::first-line  .box::before  .box::after
input[type="text"]   a[href^="https"]
```

### Text styling
```css
font-size: 1.2rem;  font-weight: bold;  font-style: italic;
text-align: center;  text-transform: uppercase;  text-decoration: underline;
letter-spacing: 2px;  line-height: 1.8;  color: #333;
text-overflow: ellipsis; white-space: nowrap; overflow: hidden;   /* "..." cut-off */
```

### Borders & backgrounds
```css
border: 2px solid #333;  border-radius: 10px;  border-bottom: 1px dashed #ccc;
outline: none;
background-color: #f4f4f4;
background-image: url("bg.jpg");
background-size: cover;  background-position: center;  background-repeat: no-repeat;
background-attachment: fixed;   /* parallax effect */
```

### Overflow
`overflow: hidden` (cut off) · `overflow: auto` (scroll when needed) · `overflow-x: auto` (sideways scroll)

### Media query breakpoints
```css
@media (max-width: 1024px) { /* tablet landscape */ }
@media (max-width: 768px)  { /* tablet */ }
@media (max-width: 480px)  { /* phone */ }
```

### Dark mode (follows system setting)
```css
@media (prefers-color-scheme: dark) {
  body { background: #121212; color: #eee; }
}
```

### CSS variables
```css
:root { --main: #1e3a5f; --accent: #f4a261; }
.btn { background: var(--accent); }
```

---

## PART 16 — PLACEHOLDER CONTENT

- Images: `https://picsum.photos/WIDTH/HEIGHT` (add `?1`, `?2` for different pictures)
- Profile photos: `https://i.pravatar.cc/150`
- Dummy text: search "lorem ipsum generator", or in VS Code type `lorem` then Tab (Emmet)

---

## PART 17 — DEBUGGING CHECKLIST

1. CSS not working? Check `<link rel="stylesheet" href="style.css">` file name and same folder.
2. Add `* { outline: 1px solid red; }` to see every box.
3. Right-click → Inspect in Chrome to see which CSS is applied or crossed out.
4. Class in HTML `class="card"` → in CSS `.card` (dot). ID `id="main"` → `#main` (hash).
5. Missing `;` or `}` breaks everything after it.
6. Image not showing? Check spelling, file extension (.jpg vs .png), and folder.
7. `z-index` not working? The element needs `position` set.
8. Absolute element in the wrong place? Give the parent `position: relative`.
