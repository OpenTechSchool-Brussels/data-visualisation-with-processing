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
    float[] ArrayOfFloats = new float[10]; // Defines an array of floats, of size 10.
    float rez = ArrayOfFloats[4]; // Access to the fifth value.
    ArrayOfFloats[5] = 4; // Modify one of its value.
    int size = ArrayOfFloats.length; // Size of the array
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

But wait what about the arrays? True, true, let's use and create those data set before anything else.

```java
float[] dataUniform;
float[] dataGaussian;
float[] dataPerlin;

int k;

void setup() {
  size(600,500);
  fill(255);
  noStroke();
  
  k = 100000;

  // Creating our data sets
  dataUniform = new float[k];
  dataGaussian = new float[k];
  dataPerlin = new float[k];

  for(int i=0; i<k; i++) {  
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


##c) Shapes & Colours

Display shapes & size (rectangle) : random data
Let's display series of that data. We'll display rectangles in series, of which height depends on the value of the data set. If you remember well, we draw rectangles from the upper left corner. If we want to align them not on that corner, but on a lower one, then we need to make a little maths operation. Curious about which one? Lucky you below is a code with the answer:

```java

void draw() {
  background(0);

  for(int i=0; i<200; i++) {  
    // 1) Uniform randomness
    rect( 100+i*4, 150 - dataUniform[i], 3, dataUniform[i]);

    // 2) Gaussian randomness
    rect( 100+i*4, 300 - dataGaussian[i], 3, dataGaussian[i]);

    // 3) Perlin noise
    rect( 100+i*4, 450 - dataPerlin[i], 3, dataPerlin[i]);
  }

}
```

As a little bonus, here is a way to generate new data on the fly:

```java

void keyPressed() {
    
  // We need an offset to have different Perlin noise values
  float offset = random(0,10000);
    
  for(int i=0; i<k; i++) {  
    // 1) Uniform randomness
    dataUniform[i] = random(0,100);
    // 2) Gaussian randomness
    dataGaussian[i] = randomGaussian() * 30 + 50;   
    // 3) Perlin noise
    dataPerlin[i] = noise(offset + i/100.0)*100;
  }
  
}

```

Let's use this time colour to get a feel of the data. This time, we won't display dynamically all data, we will display them statically at once. For that let's display them over many lines, as a array. We will vary two counters, defining both axis offset and the value to display:

```java
void draw() {
  background(0);
  for(int j=0; j<20; j++) { // characterising yOffset in "ellipse" 
  for(int i=0; i<100; i++) { // characterising xOffset in "ellipse"
    // 1) Uniform randomness
    fill(dataUniform[j*100+i]/100 * 255);
    ellipse( 50 +i*5, 50 +j*5, 5, 5);
    
    // 2) Gaussian randomness
    fill(dataGaussian[j*100+i]/100 * 255);
    ellipse( 50 +i*5, 200 +j*5, 5, 5);

    // 3) Perlin noise
    fill(dataPerlin[j*100+i]/100 * 255);
    ellipse( 50 +i*5, 350 +j*5, 5, 5);

  }
  }

}
```

Choosing the right colour is often a pretty complex process, and would require a whole workshop for it. Try to play with other shades, cold to warm (avoid the rainbow), gray to saturate... You might want to go check out this great resource from Nasa : [link](http://www.earthobservatory.nasa.gov/blogs/elegantfigures/2013/08/05/subtleties-of-color-part-1-of-6)

Second, up until now we used one dimension data sets. It's not the case for all data set. The dimension of a data set is defined by the number of variable in input, in our case there is only the index, so only one dimension. 

Third, in our case we had a simple way of displaying our data set. Many many more displays can be created, although not as simply. 

--next iteration of workshop, heat maps and bubble graph?--

Last, we have to keep in mind that we displayed all instances of data here, with no specific processing. This is what we're going to look right now.

##d) Making sense of it

Visualizing data is never an end in itself (or at least shouldn't...). It's one of the tools used to make sense of data, one of many, and barely ever to be used alone. In our case, we can process a bit our data to try to make more sense of it. But how to process data? It depends on the data you have. How to know the data you have? Process and visualize it. You might start seeing there is a little issue somewhere... It's not an impossible process, just an iterative one. There are no direct answer, it's more of an exploration. Then again, with experience you will learn to recognize both patterns in data before hand and associated first tools of exploration. Beside, different processes and visualizations will show data under different angle.

In our case we have a lot of data, mostly between 0 and 100. We might want to study them not case by case, but more their repartition. Let's study how many times those random variable are spread among that 0 and 100, aka their frequency.

To do that, let's create three arrays as global variables (like the preceding ones):

```java
float[] freqUniform;
float[] freqGaussian;
float[] freqPerlin;

void setup() {
//Previous code
// .....

  freqUniform = new float[100];
  freqGaussian = new float[100];
  freqPerlin = new float[100];
}
```

And then process the information. How? We'll just read the data, and for instance, when a value is between 9 and 10, we add one to the frequency array, at index 9. We do that for all data, and all possible values, and tada! Step back a little, and try to do that on your own. Even if you don't manage to do it, it's good to try your brain on it a little. Experience don't only come from coding, but on thinking how you'd code something.

```java
void setup() {
    // Previous code
    // ...

  // Parsing for frequency
  // Reset to zero
  for (int i=0; i<100; i++) {
    freqUniform[i] = 0;
    freqGaussian[i] = 0;
    freqPerlin[i] = 0;
  }
  
  // Calculate frequency
  for (int i=0; i<k; i++) {
      freqUniform[int(dataUniform[i])] ++;
      // No Gaussian yet...
      // freqGaussian[int(dataGaussian[i])] ++;
      freqPerlin[int(dataPerlin[i])] ++;
  }
}
```
If you want to reset this data by pressing a key, don't forget to update the `keyPressed()` function with that new code.

Now let's display it. Same stuff than before. Just remember that we need to loop over an array of size 100, not k.

```java
void draw() {
  background(0);
  for (int j=0; j<20; j++) {
    for (int i=0; i<100; i++) {  
      // 1) Uniform randomness
      rect( 100+i*4, 150 - freqUniform[i]/2, 3, freqUniform[i]/2);
      
      // 2) Gaussian randomness
      // No Gaussian yet...
//      rect( 100+i*4, 300 - freqGaussian[i]/2, 3, freqGaussian[i]/2);

      // 3) Perlin noise
      rect( 100+i*4, 450 - freqPerlin[i]/2, 3, freqPerlin[i]/2);
         
    }
  }
 
} 
```

Neat isn't it? Yes it is. But wait, we lost something along the lines... indeed, we had to comment out the calculus about the Gaussian randomness. Why is that so? Well, there are some times value getting outside of the [0;100] interval, messing with the indexing of the array. What to do then? Well, we need to filter the data. For that, we need to test it, the basic way to do so is called a conditional test. In lay man terms, it means "If a condition is met, then do something (and sometimes: else do something else)". We need a value between 0 and 100, so we need to test for it to be superior than 0 and inferior to 100.

```java

  for (int i=0; i<k; i++) {
    //...
    if (dataGaussian[i] > 0) {
      if (dataGaussian[i] < 100) {
        freqGaussian[int(dataGaussian[i])] ++;
      }
    }
  //...
  }
```
While not entering with both feet in the (amazing and useful) realm of logic, we can simplify our previous code using basic logic connector `and` and `or`. They work same as you would expect in real life, which for us ends up : `if (dataGaussian[i] > 0 && dataGaussian[i] < 100) { .... }`. What lies between the parenthesis is called a condition, resulting as true or false. All you can imagine using logic applies here. Try that new piece of code to display frequency information about Gaussian randomness.


Actually... more than filtering, we've been biasing the data... Bad bad us: we lied! For those who didn't realize while we were doing so, we decided to discard data based on the way we wanted to represent it. Not good. If we want to keep similar visualization, one might want to add one last rectangle at start and finish in order to show outliers.
 
So, here close our section on data discovery. I hope through such simple piece of code you manage to get both a hand on what data can mean, how visualize it can help you understand it, and the basics of chain of process of data. We will see in the upcoming sections different kind of data. Text, DNA, localized information... impossible to go through all of them, but the importance is not to get a master of all of them, but to awaken your sensibility to data and its visualization as a discipline.
