---
layout: post
title: Bloc Jams - Angular Refactor
feature-img: "img/sample_feature_img.png"
thumbnail-path: "https://d13yacurqjgara.cloudfront.net/users/3217/screenshots/2030974/bloctalk_1x.png"
short-description: Bloc Jams refactored into a single-page application architecture

---
# Bloc Jams refactored into a single-page application architecture

After creating Bloc Jams, I wanted to take the basic principles of that app and convert them to a single-page application, which would make the app have a snappier user interface and feel more like a native desktop application. To make this work, I knew I needed to convert my previous version of the app - which used vanilla JavaScript and jQuery - so that it could use a more dynamic JavaScript framework.  I found my solution in AngularJS.

## Background

Work on this project began on March 3, 2017 and was completed on March 27, 2017. The project utilizes AngularJS 1.5.7 and jQuery 2.1.4.

This was my second project in JavaScript and was largely derived from my initial project (Bloc Jams). I was the lead developer on this project, building most of the code while using assets provided in Bloc's Web Developer Track program.  My Bloc mentor, Kinsey Ann Durham, provide invaluable assistance and feedback throughout the project, especially when I found myself stuck on numerous occasions.

## Major Issues and Solutions

The album view of the original version of this application (using vanilla JavaScript) had a lot of the data populated manually. Most of the testing was done with a single album (though an additional album was added in case it was needed), so it was ok to just manually list some of the album data (like its title, artist, and release date) in the html code.


```{% highlight javascript %}
<div class="album-view-details column half">
 <h2 class="album-view-title">The Colors</h2>
 <h3 class="album-view-artist">Pablo Picasso</h3>
 <h5 class="album-view-release-info">1909 Spanish Records</h5>
</div>
{% endhighlight %}```

While the current version of the AngularJS version of Bloc Jams still primarily uses one album, I wanted to future-proof the app for a time when more albums might be added.  To do that, I needed to build functionality into my album controller that would allow the album data to be plugged in via Angular and JavaScript. I accomplished this goal as follows.

First, I created a `Fixtures` service that stored all of the album data in variables, then created a `getAlbum()` function that selected one of the albums.

```{% highlight javascript %}
        Fixtures.getAlbum = function() {
            return albumPicasso;
        };
{% endhighlight %}```

I then called that service in the Album controller and assigned its value to the controller's scope object.

```{% highlight javascript %}
  this.albumData = Fixtures.getAlbum();
{% endhighlight %}```

Finally, I updated the album template to access the scope object.

```{% highlight javascript %}
  <h2 class="album-view-title">{{ album.albumData.title }}</h2>
  <h3 class="album-view-artist">{{ album.albumData.artist }}</h3>
  <h5 class="album-view-release-info">{{ album.albumData.year }} {{album.albumData.label}}</h5>
{% endhighlight %}```

## Lessons Learned

I had my first major issues navigating Git and GitHub with this project.  This was my first time to clone another Git repository, so I had to figure out how to reconfigure my local and GitHub repositories for this project to speak to each other.

I also learned how on minor typo in your `app.js` file can cause hours of productivity to come to a screeching halt as you try to find it.

{:.center}
![]({{ site.baseurl }}/img/typo.png)

## Conclusion  

I was able to successfully convert my Bloc Jams app into a single-page AngularJS application.  In the process, I learned how to properly implement Angular into my applications and the value of the Model-View-Controller architecture, which I try to implement in all my projects now.
