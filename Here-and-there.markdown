---
layout: default
title:  "Here & There"
num: 2

---

Ah... maps. Geo-localized information. It's a neat visualization because it speaks straight to the mind of the person, it builds up upon a classic but already deep spatial representation. You can show many things on a map, stream, localized information, region information...

In this section we'll see basic way to make such a visualization.

##a) Installing libraries.
A library is not just place to read books, but also the name for portions of code that somebody else created and made possible for you to reuse following a specific design.

Now we're entering a nice part of coding. When to code your own code and when to use code from somebody else. Using somebody else usually (not always...) makes your work faster and allow you to explore more complex ideas. But sometime, digging in the smaller gears allow you a deeper understanding of what's really happening under the hood. It's through experience that you will know what is best for you and when. In any case, you will learn a lot from both path.

In our case, we will install a library for map visualization in Processing. Installing new libraries is made easy in Processing. Click in the menu on *Sketch* -> *Import Library...* -> *Add Library...*. You will be shown a list of library (don't hesitate to explore them). In the upper left corner is the possibility to filter your search. Type in "unfolding", which should leave you with only one library: *Unfolding Maps*. Click  on it, and then on Install. Tadam, job's done.

Processing libraries has the neat little habit of not only being easy to use, but also coming with examples of usage of the code. This is a very good way to learn both about the library and about coding. To access the examples, click in the menu on *File* -> *Examples...*. A new menu pops up with many folders. Each defines a specific topic, regrouping with many examples. Those that we care about now are at the bottom, in *Contributed Libraries*: *Unfolding Maps*. Try to open a few of the examples in order to get inspiration.

##b) Getting data from the net
Now we're getting serious! Not any more home made data. And even more, data straight from the web. Let's use some data from the magnificent city of Brussels, which nicely provide some [data](http://opendata.brussels.be/page/home/?flg=en). Click on *Explore* and then filter the data sets by  clicking *Map*. Then chose one that fits your particular desire (most will play nice). Let's use the [open WiFi dataset](http://opendata.brussels.be/explore/dataset/wifi0/?tab=metas) as an example.

Unfortunately... depending on where you get the data, you might find not so good formatting, which makes you need to reformat it ... which was the case for the WiFi data. You can download the new file [here](./assets/wifi.csv) and put it in the data folder of your sketch folder (access the later by clicking in the menu *Sketch* -> *Show sketch folder*). Luckily, in Processing, using a file or downloading one from the net is the same thing, you put in both case the file location, would that be on your computer or over the web. 
  
Try to open your data file in a text editor. This data file is a CSV (Comma Separated Value) with a pretty self-explanatory name. Rows are instances and column correspond to fields (like in the WiFi CSV file: *address*, *name*, *longitude*...) which are separated by commas. Processing has a data structure that follow the same principle: the table. The following snippet of code both show how to load a CSV file in a table and basic table usage.

````java

Table dataWifi;

void setup() {
  size(800, 600);
  
  // 1) Retrieving data
  dataWifi = loadTable( "wifi.csv", "header, csv");

  // 2) Reading a table

  // println allow to display a string
  // concatenating strings is done with +
  println(dataWifi.getRowCount() + " total rows in table"); 

  for (TableRow row : dataWifi.rows()) { // Allow to navigate the table
  
    // Each of the row's get function takes the field name as input.
    String name   = row.getString("name");
    String street = row.getString("street");
    int nbr       = row.getInt("number");
    float lat     = row.getFloat("latitude");
    float lng     = row.getFloat("longitude");
    
    println("Sweet sweet wifi at " + name +
            " of address: " + nbr + ", " + street +
            ". [" + lng +", "+lat+"]." );
  }  
}
```

OK, that was some work to do. Be sure to review again this code, be sure you understand each line because we will build upon it. Now that we have the data, let's get our canvas ready for it.

##c) Displaying a map

First of all, let's get the map. We discover the table object provided by Processing, now let's discover the UnfoldingMap object. First of all, let's import the library and create an instance of UnfoldingMap.

```java
// To  be put at the root of your code
import de.fhpotsdam.unfolding.*;
import de.fhpotsdam.unfolding.geo.*;
import de.fhpotsdam.unfolding.utils.*;

UnfoldingMap map;
```

And now let's instantiate it in the `setup()` function:

```java
  // In setup

  // Instantiating our map
  map = new UnfoldingMap(this);

  // Defining the zoom level and latitude / longitude
  map.zoomAndPanTo(13, new Location(50.841861, 4.352387));

  // For interactions
  MapUtils.createDefaultEventDispatcher(this, map);
  
  //For animated zooming
  map.setTweening(true);
```

Last but certainly not least, let's display the map in the `draw()` function:

```java
  // In the draw function
  background(0);  
  map.draw(); // Easy !
```

##d) Drawing over maps

And what about drawing our data you're asking me? Almost as easy! While this library is nice for zooming and navigating, what it's really great for is the fact that it talks nicely between screen position and longitude / latitude with its *map.getScreenPosition* function. You feed it with a location (longitude, latitude) and it will return a screen position (x,y).

Curious to see it in action? Well, you should have all you need to test it out by yourself. If you don't know what to try it on, below is an example:

```java
void draw() {
  noStroke();
  fill(30, 30, 255, 100);
  
  background(0);  
  map.draw();

  for (TableRow row : dataWifi.rows()) {
    float lat = row.getFloat("latitude");
    float lng = row.getFloat("longitude");
    // this is the magic function.
    ScreenPosition pos = map.getScreenPosition( new Location(lat, lng) );
    // and this is how you use the resulting structure
    ellipse(pos.x, pos.y, 10, 10);
  } 
  
}
```

All you know about graphics in Processing (drawing, images, fonts...) can be used to display any kind of data over a map. Step back a little and try to imagine what you could do with data from the previous section. You can explore too other data set from the online data bank.

##e) Markers
It's great to have a broad view or where those free wifis are, but when close to one, it'll be even better to actually know the name of the place. Let's display them when hovering about the locations. For that, we'll just need to test if the position of the mouse is close enough to the center of the ellipses.

If you don't remember, access of both mouse's coordinates is done through `mouseX` and `mouseY`. And if you've never displayed any text, it goes through the `text(String, posX, posY)` function, which display a string, at the indicated position. Last, a bit of math for those who wanted (and for the others too...). Did you ever wonder what the *absolute value* (symbol: `abs( val )` ) function does? Surely an amazing feat with such a grandiose name. Well guess, again, it is just the value without caring of the sign ( `abs(3)` -> `3`, `abs(-10.3)` -> `10.3`, ...). Not so grandiose but pretty useful.

All that plus a conditional test ends up in the following:

```java
  // In the draw function

  background(0);  
  map.draw();

  for (TableRow row : dataWifi.rows()) {
    float lat = row.getFloat("latitude");
    float lng = row.getFloat("longitude");
    ScreenPosition pos = map.getScreenPosition( new Location(lat, lng) );
    ellipse(pos.x, pos.y, 10, 10);
    
    // Only two lines for adding markers! Yay for Processing!
    if( abs(mouseX - pos.x) < 10 && abs(mouseY - pos.y) < 10) {
      text(row.getString("name"), pos.x - 10, pos.y - 10); 
    }
    
  } 
```

Here you go, basic map visualization. While our visualizations are pretty basic, you can push them forward quite easily. You might want to study the comic book rout [data set](https://bruxellesdata.opendatasoft.com/explore/dataset/comic-book-route/?tab=metas&location=17,50.84773,4.31135). Many façade are painted with comic books figure in Brussels. Why not find the shortest path with most? Why not generating routes over random positions? Not only can you display a set of data, but you can also filter it to only select the one you want an make an emphasis on it.
