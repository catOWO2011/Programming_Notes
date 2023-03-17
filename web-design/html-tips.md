# HTML

# Content

* [HTML Structure](#html-structure)
* [Metadata](#metadata)
* [User Inputs and Forms]

## HTML Structure
**Basic HTML page structure**
```html
<!DOCTYPE html>
<html> 
  <head>
  </head>
  <body>
  </body>
</html>
```
**HTML Tags**
```html
<!DOCTYPE html>
<html>
  <head>
  </head>
  <body>
    <header>
    </header>
    <main>
    </main>
    <footer>
    </footer>
  </body>
</html>
```
**HTML Main Links**
```html
<!DOCTYPE html>
<html>
  <head>
  </head>
  <body>
    <header>
      <nav>
        <ul>
          <li><a href="#home">Home</a></li>
          <li><a href="#about">About</a></li>
          <li><a href="#contact">Contact</a></li>
        </ul>
      </nav>
    </header>
    <main>
    </main>
  </body>
</html>
```
**Article element**
```html
<!DOCTYPE html>
<html>
  <head>
  </head>
  <body>
    <header>
    </header>
    <main>
      <article>
        <h2>My summer holiday</h2>
        <p>This summer are some good releases</p>
      </article>
    </main>
    <footer>
    </footer>
  </body>
</html>
```
**Example of a simple page**
```html
<!DOCTYPE html>
<html>
  <head>
    <title>Aqua Meal</title>
    <link rel="stylesheet" href="styels.css">
  </head>
  <body>
    <header>
      <img src="logo.png">
    </header>
    <nav>
      <ul>
        <li><a href="index.html">Home</a></li>
        <li><a href="location.html">Location</a></li>
        <li><a href="blog.html">Blog</a></li>
      </ul>
    </nav>
    <main>
      <h1>Blog</h1>
      <article>
        <h2>10% off this month</h2>
        <p>Visit us!</p>
      </article>
      <article>
        <h2>Our best meals</h2>
        <p>We've updated our menu with new recipes!</p>
      </article>
    </main>
    <footer>
      <p>Copyright Aqua Meal</p>
    </footer>
  </body>
</html>
```
## Metadata
**Viewport metadata**
It's important when designing responsive web pages.
```html
<!DOCTYPE html>
<html>
  <head>
    <meta name="viewport" content="width=device-with, initial-scale=1.0">
  </head>
  <body>
  </body>
</html>
```

## User Inputs and Forms
We use forms to capture input from the user.
**Form Validation**
It's a process that ensures that data is valid and conforms to defined rules.There are two methods of form validation:
* Client-side validation
* Server-side validation