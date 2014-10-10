---
layout: default
title:  "Here & There"
num: 3

---

Ah, maps, geolocalized information. It's a neat visualization because it speaks straight to the mind of the person, it builds up upon a classic but already deep spatial representation. You can show many things on a map, stream, localized information, region information...
In this section we'll see basic way to make such a visualization.

##a) Installing libraries.
A library is not just place to read books, but also the name for portion of code that somebody else created and made possible for you to reuse following a specific design.

Now we're entering a nice part of coding. When to code your own code and when to use code from somebody else. Using somebody else usually (not always...) makes your work faster and allow you to explore more complex ideas. But sometime, digging in the smaller gears allow you a deeper understanding of what's really happening under the hood. It's through experience that you will know what is best for you and when. In any case, you will learn a lot from both path.

In our case, we will install a library for map visualization in Processing. Installing new libraries is made easy in Processing. Click in the menu on *Sketch* -> *Import Library...* -> *Add Library...*. You will be shown a list of library (don't hesitate to explore them). In the upper left corner is the possibility to filter your search. Type in "unfolding", which should leave you with only one library: *Unfolding Maps*. Click  on it, and then on Install. Tadam, job's done.

##b) Running examples
Now, even better than using someone else's code is to look at some. One of the best way to learn. Luckily, both Processing and the libraries available through Processing provide examples. To access them, click in the menu on *File* -> *Examples...*. A new menu pops up with many folders. Each defines a specific topic, regrouping with many examples. Those that we care about now are at the bottom, in *Contributed Libraries*: *Unfolding Maps*. Try to open the "bikeObjectMaps" and navigate it. That's more or less what we'll try to do, but with our own data. Speaking of which... 

##c) Getting data from the net
Now we're getting serious! Not any more home made data. And even more, data straight from the web. Let's use some data from the magnificent city of Brussels, which nicely provide some [data](http://opendata.brussels.be/page/home/?flg=en). Click on *Explore* and then filter the datasets by  clicking *Map*. Then chose one that fits your particular desire (most will play nice). Let's use the [open wifi dataset](http://opendata.brussels.be/explore/dataset/wifi0/?tab=metas) as an example.

Unfortunately... depending on where you get the data, you might find not so good formatting, which makes you need to reformat it ... which was the case for the wifi data. You can download the new file [here](./assets/wifi.csv).
  
Process: Crunch it a bit .... bad bad data


##d) Ploting it
Plot: Maps.

##e) Making it better
