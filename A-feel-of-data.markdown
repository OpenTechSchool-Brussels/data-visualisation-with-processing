---
layout: default
title:  "A feel of Data"
num: 2

---

This is the most important section, and might end up being the whole of the workshop. Here, the aim is not to study or learn classical instances of data visualizations (charts, graphs...) and neither to focus on specific tools that allow you to do a discrete finite set of things. Here, the aim is to get at the core of data visualization, having a feel of the data. What representing it means, and how we can give a more human meaning to those numbers, to enlighten a perspective, to open them for exploration.

In the following, we will see many simple examples, fitting both learning how to code and getting a feel of what data and its visualization can mean. 

##a) Basic structures of data
Before using data and visualizing it, we need to have some. In programming languages, we have many ways to store information, let's review the basic ones. See this part as getting your first feel of how data is stored, a basic inspiration on how to later use it.

The atomic information holder is called a variable. A variable is defined by three things. Its name, what kind of information it stores, and its value. You can store text, integers, float, colors, vectors ... many many things. A complete definition of a variable is as follow: `float myVariable = 20.45;`.

We have in order the variable’s type (`float`), its name (`myVariable`), and the value it’ll be affected (`20.45`). The symbol `=` here doesn’t defines an equality but an affectation. It reads as “let’s calculate what is on the right side of the symbol, and affect the variable on the left with that value”.

While there are many possible types, we'll be using manly three : `floats` for decimal values (like 19.53, 0.1, -45.1), `int` for integers (0, 10, -23) and `string` for text ("h", "hello", text is always between quote marks). 

Not getting into too much details, but variables have scopes. Where you define them define where you can use them. If you want to use them locally, define them at a specific place in your program, if you want to use them everywhere, then define them at the root, at the start of your program.

Variables are good for atom of information but usually in Data Visualization, we have a loooot of data or in more precise terms : a set of data. We need a way to store this set. We could define a load of variables, but it'd be very tiring and hard to handle. Instead, for this usage we have arrays. Arrays allow you to store a finite number of variables and access them one by one using an index.

```java
    float[] arrayOfFloats = new float[10]; // Defines an array of floats, of size 10.
    float rez = ArrayOfFloats[4]; // Access to the fifth value.
    ArrayOfFloats[5] = 4; // Modify one of its value.
```

Two comments here. First, what about the gray comments after the `//`? Well they are what they are: comments. Whatever you write after `//` will be discarded by your program. Why using them then? They can be very handy for describing part of your program, explaining stuff, or just taking notes! We'll be seeing a lot of them.

Second, No, there was no mistake in the writing (not this time at least), the arrays index start at `0`, not `1`. So if you call `arrayOfFloats[1]`, you will not get the first element, but the second. This is why to call the fifth value, we code `arrayOfFloats[4]`.

#b) Show me the numbers!

Great, we have ways to store data. Now, let's use that to create our first data set, and visualize it. Processing has a few ways to generate random process, let's generate a few data set and use this occasion to study and visualize them.

Let's have a look at the three process we'll be studying. And let's have a basic feel of them with `println` a function that

```java
//randomness in Processing
// To generate a random value between min & max
float min = 0; float max = 10;
println( random(min,max);

// To generate value from a Gaussian with mean 0 and deviation1.
randomGaussian();
// What's a Gaussian? We'll try to understand when visualizing it!

// To generate Perlin noise
float offset = 0.1;
noise(offset);
// Same thing here, we'll have to visualize it to understand it!
```

You can imagine that if we had to fit one by one those values in an array, that would be again quite tiresome. Since computers are made to automate repetitive task, there must be a way to avoid doing that! And indeed there is, we will need in our case to loop over a simple process (storing data in the array) and just change one little thing at each step (where to store it, using a counter). For that we will use what is called a for loop.

```java


```
So, what is such block of code doing? A for loop will repeat a block of code until a condition is met. It can be understood in english as: "First do something (the initialisation). Then repeatedly execute code (the block of code) until I decide you’re finished (the condition). Each time you have finished executing the code between braces, do one thing in particular (usually an iteration over a counter)".

To be more precise, a for loop is defined by 4 components:

* First the *initialisation*, here `int i = 0;`. We define and instantiate here a new variable. Not a float, but an integer. We saw this type earlier with relation to colors. An integer is defined by its type: int, it is a variable with no fractional part, no numbers after the coma.

* Then you have the *condition*, here `i < 100`. A condition is something that is true or false. In our case, we use the mathematical symbol < to check if a value is inferior to another one. Other symbol allow for different test (such as > for superior to, or == to test the equality. Not to be confused with = for affection, a classic mistake.)

* Then you have the *update*, here (as often) an iteration over an index: `i = i + 1;`.

* Last,  you have the *block of code*, located between braces `{ }`, that is executed by the for loop.


FOR LOOP
Display text numbers : random data
    Display many sets of data

##c) Shapes & Colors
Display shapes & size (rectangle) : random data
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
