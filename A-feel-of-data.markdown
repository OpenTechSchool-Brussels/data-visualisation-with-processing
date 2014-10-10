---
layout: default
title:  "A feel of Data"
num: 2

---

This is the most important section, and might end up being the whole of the workshop. Here, the aim is not to study or learn classical instances of data visualizations (charts, graphs...) and neither to focus on specific tools that allow you to do a discrete finite set of things. Here, the aim is to get at the core of data visualization, having a feel of the data. What representing it means, and how we can give a more human meaning to those numbers, to enlighten a perspective, to open them for exploration.

In the following, we will see many simple examples, fitting both learning how to code and getting a feel of what data and its visualization can mean. 

##a) Basic structures of data
Before using data and visualizing it, we need to have some. In programming languages, we have many ways to store information, let's review the basic ones. See this part as getting your first feel of how data is stored, a basic inspiration on how to later use it.

The atomic information holder is called a variable. A variable is defined by three things. Its name, what kind of information it stores, and its value. You can store text, integers, float, colors, vectors ... many many things. A complete definition of a variable is as follow: `float myVariable = 20.45;`. We have in order the variable’s type (`float`), its name (`myVariable`), and the value it’ll be affected (`20.45`). The symbol `=` here doesn’t defines an equality but an affectation. It reads as “let’s calculate what is on the right side of the symbol, and affect the variable on the left with that value”. While there are many possible types, we'll be using manly three : `floats` for decimal values (like 19.53, 0.1, -45.1), `int` for integers (0, 10, -23) and `string` for text ("h", "hello", text is always between quote marks). 

Not getting into too much details, but variables have scopes. Where you define them define where you can use them. If you want to use them locally, define them at a specific place in your program, if you want to use them everywhere, then define them at the root, at the start of your program.

Variables are good for atom of information but usually in Data Visualization, we have a loooot of data or in more precise terms : a set of data. We need a way to store this set. We could define a load of variables, but it'd be very tiring and hard to handle. Instead, for this usage we have arrays. Arrays allow you to store a finite number of variables and access them one by one using an index.

```java
    float[] arrayOfFloats = new float[10]; // Defines an array of floats, of size 10.
    float rez = ArrayOfFloats[4]; // Access to the fifth value.
    ArrayOfFloats[5] = 4; // Modify one of its value.
```

No, there was no mistake in the writing (not this time at least), the arrays index start at `0`, not `1`. So if you call `arrayOfFloats[1]`, you will not get the first element, but the second. This is why to call the fifth value, we code `arrayOfFloats[4]`.

#b) Show me the numbers!

Great, we have ways to store data. Now, let's use that to create our first data set, and visualize it. Processing has a few ways to generate random process, let's generate a few data set and use this occasion to study and visualize them.

Let's have a look at the three process we'll be studying and already a first visualization.

```java
void setup() {
  size(600,500);
  fill(255);
  noStroke();
  
}

void draw() {
  background(0);
  float k;
  
  // 1) Uniform randomness
  k = random(0,100);
  ellipse(100,250,k,k);
 
  // 2) Gaussian randomness (mean=0, deviation=1)
  k = randomGaussian() * 30 + 50;
  ellipse(300,250,k,k);
 
  // 3) Perlin noise
  // frameCount contains the number of frames
  // that have been displayed since the program started
  k = noise(frameCount/100.0)*100;
  ellipse(500,250,k,k);  
}

```
Here we go, a basic visualization for the mother of data : noise. Take a step back, and don't underestimate your achievement, you have here the whole shebang. Getting data, using it, visualizing it. And not a so bad visualization since you can already decipher patterns in them. From this simple (but already dynamic!) visualization, you can already get a feeling of what all those random process are doing, but let's push it forward.

##c) Shapes & Colors
But wait what about the arrays? True, true, let's use and create those data set before anything else.

```java
float[] dataUniform;
float[] dataGaussian;
float[] dataPerlin;

void setup() {
  size(600,500);
  fill(255);
  noStroke();
  
  // Creating our data sets
  dataUniform = new float[100];
  dataGaussian = new float[100];
  dataPerlin = new float[100];

  for(int i=0; i<100; i++) {  
    // 1) Uniform randomness
    dataUniform[i] = random(0,100);
    // 2) Gaussian randomness
    dataGaussian[i] = randomGaussian() * 30 + 50;   
    // 3) Perlin noise
    dataPerlin[i] = noise(frameCount/100.0)*100;
  }
  
}

void draw() {
  background(0);
  // Nothing :(
}
```
It's always nice to have a strong feeling of what data is, nothing better than creating your own data set from scratch! This part will be the basis of what we'll do now. Unless said otherwise, I'll only add code to the `draw` function now. On a side note, we have only one data set by random process. You're invited to review our previous code and create a few per random process to understand the variations inside a same process (and for much coolness, because rendering many of them looks kinda cool).

Display shapes & size (rectangle) : random data
    Display many sets of data
Display shapes & color (ellipse) : random data

##d) Placing shapes
placing your object in space : random -> bubble graphs

Display Bar charts (frequency): random data

Heat Maps


##e) Making sense of it
Parsing, filtering ...
DNA, Fisher's Iris Data set, Text
Tree (for text, words that follow ...)
Something about ADN ?

earthobservatory.nasa.gov/blogs/elegantfigures/2013/08/05/subtleties-of-color-part-1-of-6
blog.blprnt.com/blog/blprnt/your-random-numbers-getting-started-with-processing-and-data-visualization
blog.visual.ly/45-ways-to-communicate-two-quantities
github.com/mbostock/d3/wiki/Gallery
