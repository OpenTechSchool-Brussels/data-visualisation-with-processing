---
layout: default
title:  "A feel of Data"
num: 1

---

While pretty rough, this section is the most important, and might end up being the whole of the workshop. Here, the aim is not to study or learn classical instances of data visualizations (charts, graphs...) and neither to focus on specific tools that allow you to do a discrete finite set of things. Here, the aim is to get at the core of data visualization: trying to get a feel of what data can be (numerical data in this case), what representing it means, and how we can give a more human aspect to those numbers. All that to enlighten a perspective, to open the data for exploration.

In the following, we will see many simple examples. Some good for getting back in gear about coding in processing, some for getting a feel of what data and its visualization can mean. 

##a) Basic data structures
In order to play with data, you first need to have an inner representation f it. Classic programming languages allows many ways to store information. At first one might think that all ways are more or less the same, just sometimes making for a quicker and easier handling. While all can actually be done with simple variable, our aim here to make sense of data. How you organize your data is already a way to make sense of it, and hence will help your inner representation. Not only a representation, it can also quickly become an inspiration in the way you visualize it since it's actually how the computer is storing it.

More over, variables are good for atom of information but usually in Data Visualization, we have a loooot of data or in more precise terms : a set of data. We need an accurate way to store, access and process them. While we could define a load of variables, (complex to name and hard to handle) we can use a basic data structure: the arrays. Arrays allow you to store a finite number of variables and access them one by one using an index.

If you're not already used to arrays (or just unsure on how they are used in Processing), the following code might help you refresh your memory.

```java
// Defined at the root of the code for global purpose
float[] grades;

void setup() {
  size(displayWidth, displayHeight);
  strokeWeight(5);

  // Could be instantiated before, but feels better in setup
  grades = new float[30];
  
  // Let's give fill with random grades
  for( int i = 0; i < grades.length; i++)
    grades[i] = int( random(20) );
}

void draw() {
  background(20);
  
  // Let's have basic flow chart of how our random students did  
  stroke(200);
  for( int i = 0; i < grades.length; i++)
    line(50, 50 + i*20, 50 + grades[i] * 50, 50 + i*20);
    
  // Let's check how many passed the year == got over 12
  stroke(200, 0, 0);
  line(50 + 12 * 50, 25,
       50 + 12 * 50, 25 + grades.length*20 + 25);
}

void keyPressed() {
  // Let's reroll the dices
  for( int i = 0; i < grades.length; i++)
    grades[i] = int( random(20) );
}
```

Without much, we already have a lot to talk and experiment about here. First the usage of the array (creating the array, access of its data -reading & writing-, getting its length, parsing it), then how to create our own little data set (randomness to the rescue), and last we created the mother of all visualization: a bar chart.

Last and most important, we wanted to see how many student passed (grade over twelve). Series of number would have made that hard to read. So would have been a classic bar chart. Adding a line already help with the visualization. Try already to imagine on this simple example how to better the visualization, and what message you could share. You will see that it's through practice of very simple examples that you will understand key principles (because there is nothing else to cloud the mind).

##b) Show me the numbers!

Great, we have a fitting way to store data. Now, let's see what kind of data set we can generate. Most of the data set you might get will be from nature, and as such will bear meaning in that they are a description of events. They might appear random from afar, but an understanding of the underlying mechanism will explain you what's happening. Alas, these underlying mechanism are usually hidden to the eye, it's through the study and representation of data that we can actually get a hold on them.

We will now use this method to study not data set, but data set generator, and more precisely randomness function. Randomness is a topic that could have its own workshop (any takers?!), but right now we'll focus on 4 kind of noises: White noise, Gaussian noise, Perlin noise and Pareto noise. While other [colors of noise](https://en.wikipedia.org/wiki/Colors_of_noise) are out of scope of this workshop, a bit of culture never hurt anyone.

All the following code is meant to be tested in the draw function, which will repeat it very quickly over time, hence giving the impression of showing multiple value of a data set and a graphical appreciation of it. For better graphics, put *noStroke();* in the setup function.

##### i) Uniform randomness
Otherwise called *white noise*. You can try to generate different kind of noises by feeding uniform noise in complex functions (logarithm, cosines, square root, mash up those ...).

```java
  int limit = 100; // Defines the span of random values
  float k = random(0,limit);
  ellipse(100,250,k,k);
```

We see here a *classic* random. There is no link between values and the chance to end up with one value is the same all over the scope.

##### ii) Gaussian randomness
If you've heard of the normal distribution, that's the same thing. If you haven't, well, you're going to discover it now! It's a distribution that is centered over a mean, and the further you are from the mean, the less likely the value is to be picked at random. How fast this chance drop is characterized by the deviation. By default, the mean is 0 and the deviation is 1.

```java
  int mean = 70;
  int deviation = 30;
  k = deviation * randomGaussian() + mean;
  ellipse(300,250,k,k);
```
Similar behavior than previously, but we see already that the randomness appear as centered.

##### iii) Perlin noise
A very famous noise in computer graphic (among others, for procedural texture). In order to use that evolution, we need values that follow each other. For that, we'll use as a counter the frame count which can be referred to as .... frameCount. Who would have guessed? You might want to explore feeding it with counters of different steps, or even sightly random counters.

```java
  float x = frameCount/100.0;
  k = 100 * noise(x);
  ellipse(500,250,k,k);
```

While still random, the process here is more alike of an evolution. This is why it's so appreciate in computer graphic: for its natural vibes. 

##### iv) Pareto noise
Ok, this one is a bit hardcore, a distribution from the power law family of distribution. Yep, they have families. This one is pretty cool because of the repartition it creates. Spread, but with groups. Alas, it's sometimes hard to get a fitting zoom around the values, so you need sometimes to play with the parameters... On top of a bit complex math (no need to understand it, but you might want to write the expression on paper to realize what you're doing), we're using a new function: *pow(a,b)* which takes *a* and makes it to the power of *b*, its better known representation is a^b.

```java
  int xm = 1;
  int a = 3;
  float x = xm + random(10);
  k = 100 * ( a * pow(xm, a) / pow(x, a+1) );
  ellipse(700,250,k,k);
```

Ok, that's a lot to process. Thankfully it is not your task but that of the machine. Work machine! An interesting result. Pretty small in average, but with sudden burst at occasions, usually in the same spans of length.

As said, it's hard sometimes to lock on the fitting range of output. The notion of boundaries is particularly important in data visualization. Sometimes your data set reach far, but it's a specific part you want to show. If you get the far values of, you might be lying about the size relations of your inner data set. If you include the far values, it means you're on a bigger scale, which might make the rest of your data set super dense and not very legible. While sometimes you can change for instance your scale (from linear to logarithmic for instance), there are no definite answer. Don't try to lie about or hide data, don't force a message, just try to use it for what it is.

##### v) Data set
Well, firstly, time to take a step back and to not underestimate your achievement: you have here the whole shebang here, getting data, using it, visualizing it. And that over multiple sources of information. Moreover, a not so bad visualization since we already managed to decipher a few patterns and understand the underlying information. From this simple (but already dynamic!) visualization, you can already get a feeling of what all those random process are doing.

In the rest of this section we won't use isolated values but set of those. Inspire yourself of the first part of this section where we fed an array to create similar data set for each random processes. We will refer later on to them as *dataUniform*, *dataGaussian*, *dataPerlin* and *dataPareto*. We will define there size as *k*. If you're a bit lost, just use the following pattern:

```java
// At the root
int k;
float[] dataSetTest;
```

```java
// In setup
  dataSetTest = new float[k];
  for( int i = 0; i < k; i++)
    dataSetTest[i] = 0; // replace with the corresponding formula
```

You might want to code a way to generate new data by the press of a button as we did at the start of the workshop. Very (read very very) useful.

On a side note, we have only one data set by random process. You're invited to modify our previous code and make it possible to create multiple data set per random process to study the variations inside a same process and also to be able to use many of them at once, like we will see in a later paragraph.

##c) Back to Shapes, and some Colors

Ok, so, we are getting an interesting idea of the variations of the data set, but haven't yet displayed it as a whole. I'm sure this new point of view will help us get a better understanding of our data set, and hence our random processes. First, let's look at series of our data set as a whole. For that, we'll get back to our first visualization: bar charts. Let's make them vertical charts so that we can have a line per random process, and display many data. Only issue here: how to align well the rectangles? Try to do that by yourself, but if you're stuck, below is a possible answer (for centered behaviors, with span of 100).

```java
  // In draw
  for(int i=0; i<k; i++) {  
    rect( 20+i*4, 150 - dataUniform[i], 3, dataUniform[i]);
    rect( 20+i*4, 275 - dataGaussian[i], 3, dataGaussian[i]);
    rect( 20+i*4, 450 - dataPerlin[i], 3, dataPerlin[i]);
    rect( 20+i*4, 600 - dataPareto[i], 3, dataPareto[i]);
  }
```

We mostly shapes & size to reflect the quality of a data set, let's try exploring what can be done with color, and more precisely shade of grey.

```java
  // In draw
  for(int i=0; i<k; i++) {      
    fill(dataUniform[i]/100 * 255);
    rect( 20+i*4, 150 - 3, 3, 3);
    
    fill(dataGaussian[i]/100 * 255);
    rect( 20+i*4, 275 - 3, 3, 3);
    
    fill(dataPerlin[i]/100 * 255);
    rect( 20+i*4, 450 - 3, 3, 3);
    
    fill(dataPareto[i]/100 * 255);
    rect( 20+i*4, 600 - 3, 3, 3);
  }
```

Variations in color are actually pretty hard to grasp for the human eye. Colors should usually be restricted to either show big variation over big distances, or to highlight specific part of a data set. Choosing the right colour is often a pretty complex process, and would require a whole workshop for it. Try to play with other shades, cold to warm (avoid the rainbow), gray to saturate... You might want to go check out this great resource from Nasa: [link](http://www.earthobservatory.nasa.gov/blogs/elegantfigures/2013/08/05/subtleties-of-color-part-1-of-6).

By the way, the line of data was pretty long, way to long to be displayed on one line, that could almost call for the usage of other lines, paving the way for other dimensions...

##d) 1D, 2D and the rest...
Ok, that was cheating for transitional purpose. 2D or nD data set are not just 1D data set cut, but information over two variables (like latitude and longitude for global positioning on earth).

Still, let's already how that would play for our data set, as a way to learn to display multiple dimensional set.

```java
  // In the draw function
  background(0);
  for(int i=0; i<k/50; i++) {    
  for(int j=0; j<50; j++) {      
    fill(dataUniform[j*k/50+i]/100 * 255);
    ellipse( 20+i*4, 200 - j*4, 4, 4);
    
    fill(dataGaussian[j*k/50+i]/100 * 255);
    ellipse( 20+i*4, 450 - j*4, 4, 4);
    
    fill(dataPerlin[j*k/50+i]/100 * 255);
    ellipse( 20+i*4, 650 - j*4, 4, 4);
    
    fill(dataPareto[j*k/50+i]/100 * 255);
    ellipse( 20+i*4, 800 - j*4, 4, 4);
  }
  }
```

Neat way to display and organize data. But ... there is one data set that can actually really be two dimensional (or even n dimensional), it's the Perlin noise which can take two variables as input. Try it with i and j as inputs.

Since you've come this far, a little present. Try to explore by modifying the behavior and parameters.

```java
  // In draw function
  background(0);

  float offsetI = random(0,10000);
  float offsetJ = random(0,10000);
  
  float varI = 0.05;
  float varJ = 0.05;
  
  for(int i=0; i<width/4; i++) {    
  for(int j=0; j<height/4; j++) {      
    fill(noise(offsetI + i * varI, offsetJ + j * varJ) * 255);
    ellipse( i*4, j*4, 4, 4);
  }
  }
```

Yep, classy as hell. And this is data you're visualizing. Not the classic kind of data, but data none the less, and pretty important and useful one, you'd be surprise how many software and studies are based on them. For added glory, try to have different value of *varI* *varJ*. Oh, and try to not reset each offset at each loop iteration but rather make those value evolve... Eerie results, digital design is never too far from digital art.

##e) Making sense of it

Visualizing data is never an end in itself. It's one of the tools used to make sense of data, one of many, and barely ever to be used alone. In our case, we can process a bit our data to try to make more sense of it. But how to process data? It depends on the data you have. How to know the data you have? Process and visualize it. You might start seeing there is a little issue somewhere...

It's not an impossible process, just an iterative one. There are no direct answer, it's more of an exploration. Then again, with experience you will learn to recognize both patterns in data before hand and associated first tools of exploration. Beside, different processes and visualizations will show data under different angle.

We've seen up to know data one by one, then as a set. Now let's study this set. A classic paradigm shift is to not study occurrences of values but their frequency. This means recording how many times some data occur, and plot not the data but that new information: their repartition.

To do that, let's create four arrays as global variables (hence defined at the root of your code) named *freqUniform*, *freqGaussian*, *freqPerlin* and *freqPareto*.

Let's now fill them. How? We'll just read the data bits by bits, as a stream, and log there value. For instance, when a value is between 9 and 10, we add one to the frequency array at index 9. We do that for the complete data set and tada! While this might still be a bit fuzzy, step back a little and try to do that on your own. Even if you don't manage to do it, it's good to try your brain on it a little. Experience don't only come from coding but also from thinking how you'd code something.

```java
  // In setup (after having creating them at the root)

  // Reset to zero
  for (int i=0; i<100; i++) {
    freqUniform[i] = 0;
    freqGaussian[i] = 0;
    freqPerlin[i] = 0;
    freqPareto[i] = 0;
  }

  // Calculate frequency
  for (int i=0; i<k; i++) {
    freqUniform[int(dataUniform[i])] ++;
    if (dataGaussian[i] > 0 && dataGaussian[i] < 100)
        freqGaussian[int(dataGaussian[i])] ++;
    freqPerlin[int(dataPerlin[i])] ++;
    freqPerlin[int(dataPareto[i])] ++;
  }
}
```

If you want to reset this data by pressing a key, don't forget to update the `keyPressed()` function with that new code.

Now let's display it:

```java
// meh
```

Actually ... nope, no code given this time. You have already all the tools to do it. If lost, you might want to first try the same bar chart you already used twice. Try that with small data set (and check over a few iterations) and then with bigger data set. You should see a rule of thumb appearing bits by bits and even the outline of functions of distribution. You're getting to the root of what describe the random processes. Here not only did you display existent data, but you formalized in a new way. While we came from distributions function to set of data to visuals, it's actually those visuals that helped finding the mathematical functions associated with some natural random processes in life (the normal distribution of the Gaussian for instance modelise among other stuff flipping of coins, always good to know if you want to gamble!)

Feel proud? You should! But wait... we lost something somewhere... Did you see it? Indeed, we had to filter Gaussian and Pareto values getting outside of the [0;100] range (if not, they would have been messing with the indexing of the array). Actually... more than filtering, we've been biasing the data... Bad bad us: we lied! For those who didn't realize while we were doing so, we decided to discard data based on the way we wanted to represent it. Not good. If we want to keep similar visualization, one might want to add one last rectangle at start and finish in order to show outliers.
 
So, here close our section on data discovery. I hope through such simple piece of code you manage to get both a hand on what data can mean, how visualize it can help you understand it, and the basics of chain of process of data. You will have the occasion to test or reflect about different kind of data in the following sections, text, DNA, localized information... impossible to go through all of them. The importance is not to become a master of all of them but to awaken your sensibility to data and its visualization as a discipline.
