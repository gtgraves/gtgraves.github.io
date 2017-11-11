---
layout: post
title: Bloc Jams
feature-img: "img/blur_bg_3.jpg"
thumbnail-path: "img/album.png"
short-description: A web-based music player utilizing JavaScript and jQuery

---
# A web-based music player utilizing JavaScript and jQuery

Bloc Jams was my first ever attempt at developing a web app while I was learning the ins and outs of basic JavaScript. Inspired by (much more) well-known digital music players like Spotify, I wanted to create an app that was simple to use, allowed me to access song lists and play those songs with only a few clicks, and utilized the principles of responsive web development in order for the app to function on multiple screen sizes.

{:.center}
![]({{ site.baseurl }}/img/landing.png)

## Background


Work on this project began on approximately December 28, 2016, with the first relatively functional version completed on February 18, 2017.  The project was refactored to use the jQuery helper library shortly thereafter, with full implementation finished on February 26, 2017.

At the time I started working on this project, I had some basic experience with HTML and CSS based on prior websites I had helped maintain in high school and law school.  I had also completed Code School's Frontend Foundations course to shore up my HTML and CSS concepts along with Code School's three JavaScript Road Trip courses to get an introduction to basic JavaScript.  However, until this project, I had not implemented JavaScript directly into a website or web app.

{:.center}
![]({{ site.baseurl }}/img/collection.png)

I was the lead developer on this project, building most of the code while following the lessons and using assets provided in Bloc's Web Developer Track program.  My Bloc mentor, Kinsey Ann Durham, provide invaluable assistance and feedback throughout the project, especially when I found myself stuck on numerous occasions.

## Major Issues and Solutions

### Reveal Points

One of the first major issues I encountered was animating elements on the landing page of my app.  Early on in the project, I had created a series of selling points for the app that always displayed at the bottom of the landing page. To make the page a bit more dynamic, I wanted to add some animation to the page that caused those elements to fade in when the page first loaded (and, later, when a user scrolled down the page).

{:.center}
![]({{ site.baseurl }}/img/landing_animation.gif)

Getting the animation itself to work was relatively simple.  I created an `animatePoints()` function that used a `getElementsByClassName()` selector to grab all the selling points and transform their default opacity from `0` to `1`. However, the code itself was cluttered.  I was calling the animation on each separate selling point, which was creating an extensive amount of repetition in my code.

{% highlight javascript %}
var animatePoints = function() {

    var points = document.getElementsByClassName('point');

    var revealFirstPoint = function() {
        points[0].style.opacity = 1;
        points[0].style.transform = "scaleX(1) translateY(0)";
        points[0].style.msTransform = "scaleX(1) translateY(0)";
        points[0].style.WebkitTransform = "scaleX(1) translateY(0)";
    };

    var revealSecondPoint = function() {
        points[1].style.opacity = 1;
        points[1].style.transform = "scaleX(1) translateY(0)";
        points[1].style.msTransform = "scaleX(1) translateY(0)";
        points[1].style.WebkitTransform = "scaleX(1) translateY(0)";
    };

    ...

    revealFirstPoint();
    revealSecondPoint();
    revealThirdPoint();

};
{% endhighlight %}

I realized that if I used a `for` loop to cycle through each of the selling points, I could make my code much simpler.  At first, I tried to build my `revealPoint()` function within the loop itself, but found that the animation worked much better if I placed the function outside of the loop and merely called it inside.

{% highlight javascript %}
var animatePoints = function () {

    var points = document.getElementsByClassName('point');

    function revealPoint(className) {
        className[i].style.opacity = 1;
        className[i].style.transform = "scaleX(1) translateY(0)";
        className[i].style.msTransform = "scaleX(1) translateY(0)";
        className[i].style.WebkitTransform = "scaleX(1) translateY(0)";
    }

    for (var i = 0; i < points.length; i++) {
        revealPoint(points);
    }

};
{% endhighlight %}

This code became even simpler once I refactored the app to use jQuery and utilized its `$.each()` function.

### Class Selectors in Album View

One of the trickier issues I had with the app arose in the album view.  I wanted users to be able to hover over a song in the album view and have a play button appear where the track number originally was.  If the user started playing that song, the play button would change into a pause button.  If the song was changed, the pause button would shift to the new song.

{:.center}
![]({{ site.baseurl }}/img/play.gif)

I knew that the solution to this problem would require creating a series of functions that would grab the necessary elements in the DOM, then linking those class selector functions to event listeners.  Crafting the event listeners wasn't too difficult, but I struggled substantially with the class selectors, primarily with using JavaScript's `querySelector()` function  and `parentElement` properties to identify the proper elements.  Implementing jQuery's `find()` method simplified the code and made it much easier to pick out the specific elements that needed to be manipulated on the DOM.

## Lessons Learned

This was my first attempt at creating a fully functional web app, so it's not surprising that I hit significant snags along the way.  This project became a crash course in debugging and spotting typos in my code, which would sometimes halt my process for hours while I was trying to figure out why my JavaScript logic was not working, only to later find out I had misspelled a variable somewhere along the line.

{:.center}
![]({{ site.baseurl }}/img/album.png)

This project also showed me that I still have a lot to learn about DOM manipulation and element selection in JavaScript.  Most of my issues arose from trying to identify and isolate the correct DOM element that needed manipulating.  Utilizing jQuery's helpers made this process much simpler, but it's still a skill that I will continue to polish in the future.

## Conclusion  

Bloc Jams is a simple, straight-forward media player with plenty of room to grow.  There are still issues to fix (the play/pause button in the player bar still needs functionality), and there is plenty of ways to add new features, but my original goal to create an app to practice and show off my frontend programming skills has been achieved.
