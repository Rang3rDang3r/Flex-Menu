# Sammy's Big Flex Menu
Flexible navigation with a mobile menu.
View the demo on [codepen](https://codepen.io/smzr/pen/mdObpZb)

## Setup
### HTML
Everything is targeted by class, so you can change the `<nav>` tags to `<header>` if you prefer
```html
<nav class="navbar">
  <div class="navbar__inner">
    <div class="navbar__items">
      <a class="navbar__brand" href="#">
        <img src="https://via.placeholder.com/32" alt="Company Logo">
        <strong>Company Logo</strong>
      </a>
    </div>
    <div class="navbar__items navbar__items--right">
      <a class="navbar__item navbar__link">link 1</a>
      <a class="navbar__item navbar__link">link 2</a>
      <a class="navbar__item navbar__link">link 3</a>
      <a class="navbar__item navbar__link">link 4</a>
      <a class="navbar__item navbar__link">link 5</a>
      <div class="navbar__toggle" aria-label="Navigation bar toggle" role="button" tabindex="0">
        <svg aria-label="Menu" viewBox="0 0 100 80" width="32" height="32" role="img">
          <title>Menu</title>
          <rect width="100" height="20" rx="8"></rect>
          <rect y="30" width="100" height="20" rx="8"></rect>
          <rect y="60" width="100" height="20" rx="8"></rect>
        </svg>
      </div>
    </div>
  </div>
  <div class="navbar-sidebar__backdrop" role="presentation"></div>
  <aside class="navbar-sidebar">
    <div class="navbar-sidebar__header">
      <a class="navbar__brand" href="#">
        <img src="https://via.placeholder.com/32" alt="Company Logo">
        <strong>Company Logo</strong>
      </a>
     </div>
    <div class="navbar-sidebar__body">
      <div class="menu">
        <ul class="menu__list">
          <li class="menu__list-item">
            <a class="menu__link">link 1</a>
          </li>
          <li class="menu__list-item">
            <a class="menu__link">link 2</a>
          </li>
          <li class="menu__list-item">
            <a class="menu__link">link 3</a>
          </li>
          <li class="menu__list-item">
            <a class="menu__link">link 4</a>
          </li>
          <li class="menu__list-item">
            <a class="menu__link">link 5</a>
          </li>
        </ul>
      </div>
    </div>
  </aside>
</nav>
```

### CSS
Most of the layout is done with flex
```css
.navbar {
  position: sticky;
  top: 0;
  display: flex;
  background-color: #444;
  color: white;
  padding: .5rem 1rem;
  width: 100%;
  height: 60px;
}
  
.navbar__inner {
  display: flex;
  align-items: stretch;
  justify-content: space-between;
  width: 100%;
}
  
.navbar__items {
  display: flex;
  align-items: center;
  flex: 1 1 auto;
}
  
.navbar__items--right {
  justify-content: flex-end;
}

.navbar__item {
  display: inline-block;
  padding: .25rem 1rem;
}

.navbar__link, .navbar__brand, .menu__link {
  cursor: pointer;
}

.navbar__link:hover {
  color: salmon;
}

.navbar__brand {
  color: salmon;
  text-decoration: none;
  display: flex;
  align-items: center;
}

.navbar__brand img {
  margin-right: .5rem;
}

.navbar__toggle {
  cursor: pointer;
  fill: white;
  display: none;
}
  
.navbar-sidebar, .navbar-sidebar__backdrop {
  top: 0;
  bottom: 0;
  right: 0;
  display: none;
  position: fixed;
}

.navbar-sidebar__backdrop {
  background-color: rgba(0,0,0,0.6);
  left: 0;
}

.navbar-sidebar {
  background-color: #444;
  width: 70vw;
  transform: translateX(100%);
  transition: transform 0.3s ease;
}

.navbar-sidebar--shown .navbar-sidebar {
  transform: translateX(0%);
}

.navbar-sidebar__header {
  display: flex;
  align-items: center;
  padding: .5rem 1rem;
  height: 60px;
  border-bottom: 1px solid #333;
}

.navbar-sidebar__body {
  padding: .5rem;
}

.menu {
  overflow-x: hidden;
}

.menu__list {
  list-style-type: none;
  margin: 0;
  padding-left: 0;
}
  
.menu__list-item {
  margin: .25rem 0;
}

.menu__link {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border-radius: .25rem;
  padding: .4rem 1rem;
}

.menu__link:hover {
  background-color: #555;
}
  
@media screen and (max-width: 996px) {
  .navbar__toggle {
    display: inherit;
  }

  .navbar__item {
    display: none;
  }

  .navbar-sidebar {
    display: block;
  }

  .navbar-sidebar--shown .navbar-sidebar__backdrop {
    display: block;
  }
}
```

### JS (JQuery)

```js
$( document ).ready(function() {
  $( ".navbar__toggle" ).click(function() {
    $( ".navbar" ).toggleClass( "navbar-sidebar--shown" );
  });
  $( ".navbar-sidebar__backdrop" ).click(function() {
    $( ".navbar" ).toggleClass( "navbar-sidebar--shown" );
  });
});
```

## Customization

### Direction of sidebar
To make the sidebar come from the left, change the following rules

```css
.navbar-sidebar, .navbar-sidebar__backdrop {
  top: 0;
  bottom: 0;
  left: 0;
  display: none;
  position: fixed;
}

.navbar-sidebar__backdrop {
  background-color: rgba(0,0,0,0.6);
  right: 0;
}

.navbar-sidebar {
  transform: translateX(-100%);
}

.navbar-sidebar--shown .navbar-sidebar {
  transform: translateX(0%);
}
```
You can also move the sidebar toggle (hamburger button) into the left positioned nav items

```html
<div class="navbar__inner">
    <div class="navbar__items">
      <div class="navbar__toggle"> ... </div>
      <a class="navbar__brand" href="#"> ... </a>
    </div>
    <div class="navbar__items navbar__items--right">
      <a class="navbar__item navbar__link">link 1</a>
      ...
      <a class="navbar__item navbar__link">link 5</a>
    </div>
</div>
```