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

#b) Show me the numbers!

Great, we have a fitting way to store data. Now, let's see what kind of data set we can generate. Most of the data set you might get will be from nature, and as such will bear meaning in that they are a description of events. They might appear random from afar, but an understanding of the underlying mechanism will explain you what's happening. Alas, these underlying mechanism are usually hidden to the eye, it's through the study and representation of data that we can actually get a hold on them.

We will now use this method to study not data set, but data set generator, and more precisely randomness function. Randomness is a topic that could have its own workshop (any takers?!), but right now we'll focus on 4 kind of noises: White noise, Gaussian noise, Perlin noise and Pareto noise. While other [colors of noise](https://en.wikipedia.org/wiki/Colors_of_noise) are out of scope of this workshop, a bit of culture never hurt anyone.

Let's first generate our data set and have a quick look at them, we will then try to understand them from what is displayed.

```java
void setup() {
  size(displayWidth, displayHeight);
  fill(255);
  noStroke();
}

void draw() {
  background(0);
  float k;
  
  // 1) Uniform randomness, white noise
  int limit = 100;
  k = random(0,limit);
  ellipse(100,250,k,k);
 
  // 2) Gaussian randomness
  int mean = 70;
  int deviation = 30;
  k = deviation * randomGaussian() + mean;
  ellipse(300,250,k,k);
 
  // 3) Perlin noise
  float x = frameCount/100.0;
  k = 100 * noise(x);
  ellipse(500,250,k,k);

  // 4) Pareto noise
  int ym = 1;
  int a = 3;
  float y = ym + random(10);
  k = 100 * ( a * pow(ym, a) / pow(y, a+1) );
  ellipse(700,250,k,k);

}
```

Hmm, a lot to look at, both in how they are created (not our main job here) and on what to understand of their behavior from what is displayed. But first of all, take a step back and don't underestimate your achievement: you have here the whole shebang here, getting data, using it, visualizing it. And not a so bad visualization since you can already decipher patterns in them. From this simple (but already dynamic!) visualization, you can already get a feeling of what all those random process are doing. First one is chaotic, the next one bears less bounds, but is more centered on a value, the following one is more of an evolution over time and the last one can have pretty unexpected bursts!

// EXPLANATION ABOUT THE CODE AND FORMULA

//Boundaries => some time you're out of visualisation, hard to find the good scale (other exist than linear SOURCE, for another time, enough of maths alredy).

In the rest of this section, we'll use arrays of such random values, called dataUniform, dataGaussian, dataPerlin and dataPareto. Don't forget to create them and fill them with value in the setup function!

On a side note, we have only one data set by random process. You're invited to modify our previous code and make it possible to create multiple data set per random process to study the variations inside a same process (and for much coolness, because rendering many of them looks kinda neat).

##c) 1D, 2D and the rest...

##d) Shapes & Colours

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
