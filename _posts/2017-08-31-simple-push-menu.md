---
layout: post
title: A Simple Push Menu
---

This is a post meant to hash out a simple way to accomplish a slide in push menu for navigation.

I was working on a small project recently and wanted to gain some real estate on my screen so I decide to make a push menu. At the end I was really happy with how it worked and looked. It also made me realize how handy dandy they are. To summarize this [post](http://www.freshform.com/blog/popular-ux-navigation-patterns/), push menus are great for saving space like I said, they feel good, look good, and I believe they would be great for large menus.

<h3 class="text-center"><a href="https://codepen.io/Brayn/pen/eEbZbr?editors=1010">simple push menu demo</a></h3>

Here is what I did...

# The HTML

## Scaffolding

I figured I would have a main div with two children in it. One for the menu itself and the other for my content.

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Simple Push Menu</title>
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-beta/css/bootstrap.min.css" integrity="sha384-/Y6pD6FV/Vv2HJnA6t+vslU6fwYXjCFtcEpHbNJ0lyAFsXTsjBbfaDjzALeQsN6M" crossorigin="anonymous">
  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css">
  <link rel="stylesheet" href="./style.css">
</head>
<body>
  <div id="main-container">
    <div class="nav-wrapper d-inline-block text-center">
    <!-- menu -->
    </div>
      
    <div class="wrapper">
      <!-- content -->
    </div>
  </div>
</body>
</html>
```
note: I used Bootstrap 4 just to make my life easier which you can take it or leave it.

In the menu area I knew I wanted a place for a logo/brand and some menu items

## Menu Content

```
<div class="brand mt-3">
      <h2>Brand</h2>
</div>
    <ul class="nav flex-column mt-4">
      <li class="nav-item">
        <a class="nav-link active" href="#section_1">Section 1</a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="#section_2">Section 2</a>
      </li>
      <li class="nav-item">
        <a class="nav-link" href="#section_3">Section 3</a>
      </li>
    </ul>
```
note: I basically copy pasted the ul nav from the [bootstrap 4 website](https://getbootstrap.com/docs/4.0/components/navs/)

Now I know I want a menu button, an overlay and some content.
So in the .wrapper div where my content is going I put...

## Menu Button

my menu button...

```
<button id="menu-btn" class="nav-btn btn btn-sm btn-outline-primary m-2 ml-2 border-0">
      <i class="fa fa-bars" aria-hidden="true"></i>
</button>
``` 
note: menu icon is from [font-awesome](http://fontawesome.io/).

## Overlay

here is a hard one...the overlay.

```
<div class="overlay"></div>
```

## Content

Let's pop some content in the and spice it up with [Star Trek Ipsum](http://vlad-saling.github.io/star-trek-ipsum/)

```
<div class="container-fluid col-10 mx-auto">
      <div class="row">
      <div class="col my-4">
        <h1 class="display-4">Simple Push Menu</h1>
      </div>
    </div>
    <div id="section_1" class="row">
      <div class="col">
        <h2>Section 1</h2>
          <p>
              I have reset the sensors to scan for frequencies outside the usual range. By emitting harmonic vibrations to shatter the lattices. We will monitor and adjust the frequency of the resonators. He has this ability of instantly interpreting and extrapolating any verbal communication he hears. It may be due to the envelope over the structure, causing hydrogen-carbon helix patterns throughout. I'm comparing the molecular integrity of that bubble against our phasers.
        </p>
      </div>    
    </div>
    <div id="section_2" class="row">
      <div class="col">
        <h2>Section 2</h2>
          <p>
              Sensors indicate no shuttle or other ships in this sector. According to coordinates, we have travelled 7,000 light years and are located near the system J-25. Tractor beam released, sir. Force field maintaining our hull integrity. Damage report? Sections 27, 28 and 29 on decks four, five and six destroyed. Without our shields, at this range it is probable a photon detonation could destroy the Enterprise.

        </p>
      </div>    
    </div>
    <div id="section_3" class="row">
      <div class="col">
        <h2>Section 3</h2>
          <p>
             These are the voyages of the Starship Enterprise. Its continuing mission, to explore strange new worlds, to seek out new life and new civilizations, to boldly go where no one has gone before. We need to neutralize the homing signal. Each unit has total environmental control, gravity, temperature, atmosphere, light, in a protective field. Sensors show energy readings in your area. We had a forced chamber explosion in the resonator coil. Field strength has increased by 3,000 percent.
         </p>
        </div>    
      </div>
    </div>
```

# The CSS (Sass)

## Menu Styles

Let's Get That Menu off the screen!

```
.nav-wrapper {
  width: 220px; // 220px seems to be a good size from other examples I have looked at.
  background: #333;
  color: white;
  height: 100%;
  position: fixed; // this is important for positioning
  left: -220px; // this pushes the menu off the screen equal to its width
  transition: left 1s; // this transitions the menu back off the screen when closing
  } // .nav-wrapper
```

You should have the menu off the screen. You could go to the inspector and give the .nav-wrapper left: 0; and see it pop in.

Now lets style the list a little bit. 

```
.nav-wrapper {
  width: 220px;
  background: #333;
  color: white;
  height: 100%;
  position: fixed;
  left: -220px;
  transition: left 1s;
  
  ul {
    
    li {
      padding: 1em; // give the items some meat for people to click on and for background color later.
      transition: background .5s;
      // adding a hover effect with sass is super nice and easy ;)
      &:hover { 
        cursor: pointer;
        background: #007bff;
        transition: background .5s;
      }
    }// end li
    
    a {
      padding: 0 !important; // overwritting some bootstrap here
      color: white;
    } // end a
    
  } // end ul
  
} // .nav-wrapper
```
note: I am using sass and one nice thing sass lets you do is nest you css selectors. See how I have my ul inside my .nav-wrapper, and my li inside my ul. 

## .wrapper Styling

fairly straight forward

```
.wrapper {
  position: relative; // you need this for transition
  left: 0; // and this too
  transition: left 1s;

  // nav btn style to keep it top left of content container
  .nav-btn {
    position: fixed;
    top: 0px;
    z-index: 2000;
  }// end .nav-btn
}
```

## PUSH!

we will add the push class to the body with javascript and then all this will fall into place.

```
// css to push the nav and content over
.push {
  
  overflow:hidden;
  
  .nav-wrapper {
    left: 0px; // move nav in 220px
    transition: left 1s;
  } 
  
  .wrapper {
    width: 100%;
    position: absolute;
    left: 220px; // move wrapper over 220px
    overflow: hidden; // lock up the scrolling
    transition: left 1s;

    // now put a subtle overlay that spans the whole of the content
    .overlay {
      position: absolute;
      width: 100%;
      height: 100%;
      background: rgba(229, 224, 222, 0.5);
      z-index: 1000;
      transition: 1s;
    }
  }
  
}
```

# The Javascript

Here is the super simple part.
Just get the button with the id name and add a event listener to it.
Then we use a ternary ((condition) ? /* what happens if condition is true */ : /* what happens if condition is false */) to add the class 'push' to the body if it dosn't already have it, and remove 'push' if does.

```
// on click add and remove class from body.
document.getElementById('menu-btn').addEventListener('click', (()=>{
  let $body = document.body;
  // if body has the class push then remove it, otherwise add it
  $body.getAttribute('class') === "push" ? $body.classList.remove('push') : $body.classList.add('push');
}));
```

That's it hope you find this handy.







