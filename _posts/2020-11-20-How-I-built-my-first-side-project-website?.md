# Why to build a side project?

So this was the time of April 2018, when I began learning Angular. I started with the cliche official docs tutorial ‘tour of heroes’ and got familiar with the basics of angular. However, it was more like a tutorial that gives you the code of everything and you just copy it.

Though, not gaining much confidence after that I continued the official docs and learned many things. The initial ones were not so difficult like interpolation, event binding, directives but as I proceeded the learning curve got steeper and steeper. Observables, HTTP modules, dependency injection all just started to blow my mind. So, I realized that only reading or learning from the docs isn’t going to help much so I rushed to google for searching project ideas. I got a few tutorials on youtube including the [BookMarker](https://www.youtube.com/watch?v=DIVfDZZeGxM) app, however, Brad sir built it without any frameworks but I tried to build it with angular, so it was a bit of learning. But still, there were tons of features of Angular that weren’t covered.

So, the next thing was to realize that I had to develop a project completely on my own i.e. without any reference to any tutorial, and trust me building a project completely from a scratch is on a whole different level than building a project according to some tutorial.

I began searching for ideas and came up with the idea of building a site that will show videos on search. I decided to use [Dailymotion’s API](https://developer.dailymotion.com/api) for the task.


<img alt="Image for post" class="t u v gt aj" src="https://miro.medium.com/max/2200/0*oTJWPp8BXR4aR-8r" width="1100" height="586" srcSet="https://miro.medium.com/max/552/0*oTJWPp8BXR4aR-8r 276w, https://miro.medium.com/max/1104/0*oTJWPp8BXR4aR-8r 552w, https://miro.medium.com/max/1280/0*oTJWPp8BXR4aR-8r 640w, https://miro.medium.com/max/1400/0*oTJWPp8BXR4aR-8r 700w" sizes="700px"/>

> This is the final landing page of my project.

# The Project

So, I am not going to give any sort of tutorial on building this project as the central idea of this blog post is to build projects on your own from scratch. This will include just an overview of the project so that you can give it a shot on your own.

1.The first feature to include was to make the search bar functional, for which I used:

```
“https://api.dailymotion.com/videos?fields=id,thumbnail_url%2Ctitle&search="+str+"&limit="+this.limit
```

The str variable was equal to the value I got by the search bar. I used [reactive forms](https://malcoded.com/posts/angular-fundamentals-reactive-forms) for smooth data transferring.

The result was this:

<img alt="Image for post" class="t u v gt aj" src="https://miro.medium.com/max/2200/0*KghHlB0Kir6Hkkqq" width="1100" height="586" srcSet="https://miro.medium.com/max/552/0*KghHlB0Kir6Hkkqq 276w, https://miro.medium.com/max/1104/0*KghHlB0Kir6Hkkqq 552w, https://miro.medium.com/max/1280/0*KghHlB0Kir6Hkkqq 640w, https://miro.medium.com/max/1400/0*KghHlB0Kir6Hkkqq 700w" sizes="700px"/>

The good looking ‘+’ icon and the stream video online button was all with the help of [Angular Material](https://material.angular.io/components/categories).


2.Now it was easy to just give the URL of the video from Dailymotion and redirect every time to Dailymotion when we hit the stream button. But, I decided to stream the video on my own site.

Now, when we click on the button a smooth-looking [modal](https://material.angular.io/components/dialog/overview) will open up containing the video embed and a few of its details.

The embed video API I used was 
[this](https://api.dailymotion.com/embed/videos?fields=id,thumbnail_url%2Ctitle&search=%22+str).

After all this the button was working :

<img alt="Image for post" class="t u v gt aj" src="https://miro.medium.com/max/2200/0*G4l2mjSdWWo2IkIb" width="1100" height="585" srcSet="https://miro.medium.com/max/552/0*G4l2mjSdWWo2IkIb 276w, https://miro.medium.com/max/1104/0*G4l2mjSdWWo2IkIb 552w, https://miro.medium.com/max/1280/0*G4l2mjSdWWo2IkIb 640w, https://miro.medium.com/max/1400/0*G4l2mjSdWWo2IkIb 700w" sizes="700px"/>


> 
The modal shows the embed video

At this time my project was about to complete. But I gave myself one more challenge i.e. to include a favorites tab in the navigation bar.

The challenge for me was that I didn’t have any knowledge of backend at that time so I searched about it and got to know about local storage. However, even after that, there were a whole lot of difficulties I overcame to include this functionality. While doing the project I was constantly struggling with the new bugs and errors I found and googling helped me every time.

<img alt="Image for post" class="t u v gt aj" src="https://miro.medium.com/max/2200/0*k0PhlrM30QoKx0bK" width="1100" height="581" srcSet="https://miro.medium.com/max/552/0*k0PhlrM30QoKx0bK 276w, https://miro.medium.com/max/1104/0*k0PhlrM30QoKx0bK 552w, https://miro.medium.com/max/1280/0*k0PhlrM30QoKx0bK 640w, https://miro.medium.com/max/1400/0*k0PhlrM30QoKx0bK 700w" sizes="700px"/>


> 
The favorites section


# CONCLUSION

After doing this project, I felt much more confident in my development skills. Some extra features are:

1.Routing. I used it in the navigation bar.

> 
<img alt="Image for post" class="t u v gt aj" src="https://miro.medium.com/max/1760/0*dYYvbnO_c9Ge6YmY" width="880" height="81" srcSet="https://miro.medium.com/max/552/0*dYYvbnO_c9Ge6YmY 276w, https://miro.medium.com/max/1104/0*dYYvbnO_c9Ge6YmY 552w, https://miro.medium.com/max/1280/0*dYYvbnO_c9Ge6YmY 640w, https://miro.medium.com/max/1400/0*dYYvbnO_c9Ge6YmY 700w" sizes="700px"/>

2.For various design features like raised-buttons, input, and the modal itself I used angular-material.

3.The search results come in an animated piling up manner which I implemented with the help of [Angular Animations](https://angular.io/guide/animations).

4.I made two services one for favorites and the others for the videos. That made me learn about sharing data between the components and the dependency injection in angular.

5.LocalStorage for saving favorite videos.

I hope this was of some help to you guys. Like this, you can create a movie search app, weather forecast app, etc.

You can contribute to this [project](https://github.com/SarthakSri98/ngVideoz) too as there are many functionalities that can be added here like there is no backend support right now.

The site is hosted on firebase [here](https://ngmuzic-d1010.firebaseapp.com).