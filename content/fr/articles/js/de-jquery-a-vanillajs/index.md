---
date: "2013-12-05"
title: De jQuery à Vanilla JS
tags:
  - javascript
  - jquery
  - vanillajs
authors:
  - kud
header:
  image: jquery-die.jpg
  linearGradient: 160deg, rgb(204, 51, 51), rgba(204, 51, 51, .6)
---

Oui alors jQuery, c'est sûrement très bien, ça simplifie pas mal de choses et le
_chaining_ est intéressant mais eeeest-ce que vous connaissez l'équivalent en
_pur_ JavaScript ? Pas sûr hein.

Ce petit article vous propose de quoi peut-être vous faire changer d'avis sur la
bibliothèque qui pèse tout de même environ ~80ko.

_Note : [Vanilla JS](http://vanilla-js.com/) n'est pas un framework mais veut
simplement dire "à nu", c'est du JavaScript sans bibliothèque._

C'est parti !

## Table des matières

1.  [Évènements](#-v-nements)
2.  [Sélecteurs](#s-lecteurs)
3.  [Attributs](#attributs)
4.  [Classes](#classes)
5.  [Manipulation](#manipulation)
6.  [Navigation](#navigation)
7.  [AJAX](#ajax)
8.  [JSONP](#jsonp)

## Évènements

```javascript
// jQuery
$(document).ready(function() {
  // code
});

// Vanilla
document.addEventListener("DOMContentLoaded", function() {
  // code
});
```

```javascript
// jQuery
$('a').click(function() {
  // code…
})

// Vanilla
[].forEach.call(document.querySelectorAll('a'), function(el) {
  el.addEventListener('click', function() {
    // code…
  })
})
```

## Sélecteurs

```javascript
// jQuery
var divs = $("div");

// Vanilla
var divs = document.querySelectorAll("div");
```

```javascript
// jQuery
var newDiv = $("<div/>");

// Vanilla
var newDiv = document.createElement("div");
```

## Attributs

```javascript
// jQuery
$("img")
  .filter(":first")
  .attr("alt", "My image");

// Vanilla
document.querySelector("img").setAttribute("alt", "My image");
```

## Classes

```javascript
// jQuery
newDiv.addClass("foo");

// Vanilla
newDiv.classList.add("foo");
```

```javascript
// jQuery
newDiv.toggleClass("foo");

// Vanilla
newDiv.classList.toggle("foo");
```

## Manipulation

```javascript
// jQuery
$("body").append($("<p/>"));

// Vanilla
document.body.appendChild(document.createElement("p"));
```

```javascript
// jQuery
var clonedElement = $("#about").clone();

// Vanilla
var clonedElement = document.getElementById("about").cloneNode(true);
```

```javascript
// jQuery
$("#wrap").empty();

// Vanilla
document.getElementById("wrap").innerHTML='';
// or since ie 12
document.getElementById("wrap").remove;
```

## Navigation

```javascript
// jQuery
var parent = $("#about").parent();

// Vanilla
var parent = document.getElementById("about").parentNode;
```

```javascript
// jQuery
if($('#wrap').is(':empty'))

// Vanilla
if(!document.getElementById('wrap').hasChildNodes())
```

```javascript
// jQuery
var nextElement = $("#wrap").next();

// Vanilla
var nextElement = document.getElementById("wrap").nextSibling;
```

## AJAX

### GET

```javascript
// jQuery
$.get("//example.com", function(data) {
  // code
});

// Vanilla
var httpRequest = new XMLHttpRequest();
httpRequest.onreadystatechange = function(data) {
  // code
};
httpRequest.open("GET", url);
httpRequest.send();
```

### POST

```javascript
// jQuery
$.post("//example.com", { username: username }, function(data) {
  // code
});

// Vanilla
var httpRequest = new XMLHttpRequest();
httpRequest.onreadystatechange = function(data) {
  // code
};
httpRequest.setRequestHeader(
  "Content-Type",
  "application/x-www-form-urlencoded",
);
httpRequest.open("POST", url);
httpRequest.send("username=" + encodeURIComponent(username));
```

### JSONP

```javascript
// jQuery
$.getJSON("//openexchangerates.org/latest.json?callback=?", function(data) {
  // code
});

// Vanilla
function formatCurrency(data) {
  // code
}
var scr = document.createElement("script");
scr.src = "//openexchangerates.org/latest.json?callback=formatCurrency";
document.body.appendChild(scr);
```

Cela vous parait-il encore difficile de vous passer de jQuery ? :)

Un grand merci à [@deaxon](http://playground.deaxon.com/js/vanilla-js/) qui est
à l'origine de cet éclaircissement.

## À creuser

Il existe une version minimaliste de jQuery basée sur la même API mais beaucoup
plus légère s'appelant [Zepto](http://zeptojs.com/). Il est actuellement utilisé
en production sur le site mobile de ma boite.
