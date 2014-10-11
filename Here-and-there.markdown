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

Unfortunately... depending on where you get the data, you might find not so good formatting, which makes you need to reformat it ... which was the case for the wifi data. You can download the new file [here](./assets/wifi.csv) and put it in the data folder of your sketch folder (access the later by clicking in the menu *Sketch* -> *Show sketch folder*). Luckily, in Processing, using a file or downloading one from the net is the same thing, you put in both case the file location, would that be on your computer or over the web. 
  
Try to open your data file in a text editor. This data file is a CSV (Comma Separated Value) with a pretty self-explanatory name. Rows are instances and column correspond to fields (like in the wifi CSV file: *address*, *name", *longitude*...) which are separated by commas. Processing has a data structure that follow the same principle : the table. The following snippet of code both show how to load a CSV file in a table and basic table usage.

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

  for (TableRow row : dataWifi.rows()) {  
    // Each of the row's get function takes the field name as input.
    String name = row.getString("name");
    String street = row.getString("street");
    int nbr = row.getInt("number");
    float lat = row.getFloat("latitude");
    float lng = row.getFloat("longitude");
    
    println("Sweet sweet wifi at " + name +
            " of adress: " + nbr + ", " + street +
            ". [" + lng +", "+lat+"]." );
  }  
}
```

Now that we have the data, let's get our canvas ready for it.

##d) Displaying a map

First of all, let's get the map. We discover the table object provided by Processing, now let's discover the UnfoldingMap object. First of all, let's import the library and create an instance of UnfoldingMap.

```java
// To  be put at the root, above setup()
import de.fhpotsdam.unfolding.*;
import de.fhpotsdam.unfolding.geo.*;
import de.fhpotsdam.unfolding.utils.*;

UnfoldingMap map;
```

And now let's instantiate it in the `setup()` function:

```java
  // Instanciating our map
  map = new UnfoldingMap(this);

  // Defining where it points to, and the level of zoom
  map.zoomAndPanTo(13, new Location(50.841861, 4.352387));

  // For interactions
  MapUtils.createDefaultEventDispatcher(this, map);
  
  //For animated zooming
  map.setTweening(true);
```

And last, let's show it in the `draw()` function:

```java
  background(0);  
  map.draw(); // Easy !
```

And what about drawing our data you're asking me? Almost as easy! While this library is nice for zooming and navigating, what it's really great for is the fact that it talks nicely between screen position and longitude/latitude. All in all, here how it goes:

```java
void mapViz() {
  noStroke();
  fill(30, 30, 255, 100);
  
  background(0);  
  map.draw();

  for (TableRow row : tableWifi.rows()) {
    float lat = row.getFloat("latitude");
    float lng = row.getFloat("longitude");
    // this is the magic function.
    ScreenPosition pos = map.getScreenPosition( new Location(lat, lng) );
    // and this is how you use the resulting structure
    ellipse(pos.x, pos.y, 10, 10);
  } 
  
}
```

Try to play with the various data you have and try to push forward the visualization beyond simple dots displayed on a map. For instance you might make the size of the ellipse depending on the zoom level (you can use `map.getZoom()` for that).

##e) Markers
Great to have a broad view or where those free wifis are, but when close to one, it'll be even better to actually know the name of the place. Let's display them when hovering about the locations. For that, we'll just need to test if the position of the mouse is close enough to the center of the ellipses.

So much to learn here! First, you can access both coordinates of the mouse through `mouseX` and `mouseY`. Second, let's learn a new function that will be of much use in the next section: `text(String, posX, posY)` which display a string, at the indicated position. And last, a bit of math for those who wanted (and for the others too...). Did you ever wonder what the *absolute value* (symbol: `abs( val )` ) function does? Surely an amazing feat with such a grandiose name. Well guess, again, it is just the value without caring of the sign ( `abs(3)` -> `3`, `abs(-10.3)` -> `10.3`, ...). Not so grandiose but pretty useful, especially for calculating distances. All that plus a conditional test ends up in the following:

```java

void mapViz() {
  noStroke();
  fill(30, 30, 255, 200);
  
  background(0);  
  map.draw();

  for (TableRow row : tableWifi.rows()) {
    float lat = row.getFloat("latitude");
    float lng = row.getFloat("longitude");
    ScreenPosition pos = map.getScreenPosition( new Location(lat, lng) );
    ellipse(pos.x, pos.y, 10, 10);
    
    // Only two lines for adding markers! Yay for Processing!
    if( abs(mouseX - pos.x) < 10 && abs(mouseY - pos.y) < 10) {
      text(row.getString("name"), pos.x - 10, pos.y - 10); 
    }
    
  } 
  
}
```

Here you go, basic map visualization. You have already a lot of possibilities for visualization, from past section and this one, don't hesitate to take a little time to explore them. While our visualization are pretty basic, you can push them forward quite easily.



