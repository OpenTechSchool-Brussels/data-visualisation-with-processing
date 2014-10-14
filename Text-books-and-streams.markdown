---
layout: default
title:  "Text, books & streams"
num: 4

---

One type of data that is too often forgotten is text data. A shame, since this is where processing filter are kings & queens. Using linguistic and semantics, you can push forward, mine text, and display them in a way you wouldn't have thought possible for a boring linear piece of text.

We have in mind to let you play with three kind of text: twitter streams, books and DNA sequences. Let's already start with twitter, we'll see if your lovely organizer had time to stuff the workshop material with more goodness (probably not this time...).

## a) Using libraries, again & Twitter dev stuff

Ah, easy pea, we already use a library! But this time ... it's not a Processing library. Oh my god! But then how can they communicate? Alien translator? Telepathy? Almost. While Processing is a language on its own, it's actually a over-set of another well known programming language: Java. Whatever you might know or will learn in Java,  you can reuse in Processing. This is doubly interesting: first, you have all the power of Java at your hands, all its structure, functions...; second, you can reuse any Java library, like the one we'll be using to feed on Twitter. Download it [here](http://twitter4j.org/archive/twitter4j-4.0.2.zip). In the *lib* folder, you will found the *twitter4j-core-4.0.2.jar* file. Extract it in safe place and then drag and drop the extracted file on your opened processing sketch. You should see at the bottom "one file added to the sketch".

Now, library is installed. Unfortunately, to be able to use it Twitter requests you to have some identification. For that, you need to register a twitter account. Then visit https://app.twitter.com/ and login. Click on *Create an app*, fill out the form (you can put random info) and agree to the developer terms. You should arrive at a page with among others the *Consumer key* and the *Consumer secret*. Click on *Generate my access Token* and you should get the two last info we need: the *Access Token* and the *Access Token Secret*. Good, now before reading those tweets, let's learn how they are stored in the library.

##b) A new data structure
While arrays are pretty nice, their size is hard defined at first, and can't change. It's both sad and not so much practical. Instead here we'll use an *ArrayList* which is working pretty much the same, but better. While we'll have to handle it, our future usage will be pretty simple, but let's first see a bit how it works.

```java

// Defining your variables
// Between < > is the datastructure that we'll feed the ArrayList.
ArrayList<Integer> myArrayList;
int[] myArray;

void setup() {
  
 // Instanciating your variables
 myArray = new int[3]; 
 myArrayList = new ArrayList<Integer>();
 
 // Adding values
 myArray[0] = 10;
 myArray[1] = 20;
 myArray[2] = 30;
  
 myArrayList.add(10); // Values are added on "top" of the previous ones
 myArrayList.add(20);
 myArrayList.add(30);
 
 // Access to values
 float midArray = myArray[1] / 2.0;
 float midArrayList = myArrayList.get(1) / 2.0;
 
 // size of the structure
 int sizeArray = myArray.length;
 int sizeArrayList = myArrayList.size();

 exit(); 
}

void draw() {
  
}
````
Pretty similar to the arrays right? But much more powerful! Now that we are armed and dangerous, let's use our newly acquired skills to tackle this twitter library!

##c) Reading some tweets

Now .... sometimes you care, sometimes you don't. While at OTS we pride ourselves on explaining each line of code, sometimes while using more heavy libraries, some part of code might appear that are extremely useful but might be a bit out of league as for assimilation. Not saying it's not important to understand it, but there is a safe margin between "getting it" and being able to recode the whole library... This will be the case here.

So, let's have an overfly of how connecting to twitter works.

```java
// Import twitter library
import twitter4j.*;
// Import for an inside java library (for using List)
import java.util.*;
 
// Here we'll be using List as an ArrayList.
// Status is a data structure specific to the twitter library
List<Status> listStatus;
// TwitterFactory allows us later to create twitter objects
TwitterFactory twitterFactory;
// What we will need later to connect to twitter
Twitter twitter;
 
void setup() {    
  size(displayWidth, displayHeight); 
  listStatus= new ArrayList<Status>();
  
  // 1) Connecting to twitter (use your own ids)
  // Don't over think the following lines. We create a new object
  // and then set inner variables to our keys and tokens.
  ConfigurationBuilder cb = new ConfigurationBuilder();
  cb.setOAuthConsumerKey("...");
  cb.setOAuthConsumerSecret("...");
  cb.setOAuthAccessToken("...");
  cb.setOAuthAccessTokenSecret("...");
 
  // We know use this knewly created object to create a twitterFactory
  twitterFactory = new TwitterFactory(cb.build());
  // And we use this factory to finaly create our twitter object.
  twitter = twitterFactory.getInstance();
  
} 
```

Soo ... when to care, and when not to? Well, if you're confident in a piece of code that is for now too specific for you to learn a lot, then you might want to use it, get a feel of it, but not dig deeper. Understanding is important, but exploring is too.

Now that we connected, let's launch a query on twitter, this works in the same way as the *search* would on twitter.

```java

  // Previous code
  // ...

void setup() {

  // Previous code
  // ...

  // 2) Launching a query
  // A query is an object that will provide us tweets.
  // You create it by providing the string you will be searching for
  Query query = new Query( "OpenTechSchool );
  QueryResult result;
  
 // Wouhou.... try catch... Don't dwell to much on that, let's just say
 // that whatever is in the try{ .. } will be checked for the "TwitterException" error.
 // If there is one then what is in catch() { ... } will be executed.
  try {
    // Launch the query and get the resulting tweets.
    listStatus= twitter.search(query).getTweets();
  } catch(TwitterException e) {        
    println("Error");
  }    
  
  // 3) Outputing tweets
  for (int i =0; i < statuses.size(); i++) {
    // .getText() is an inner function of Status and return the text of the tweet.
    println(statuses.get(i).getText());
  }

```

Alas, we got them! Cheery merry tweets! Now that we have the data, you can display them in any form you prefere. Don't hesitate to explore graphical ways to display them, would that be using text or not. You could for instance compare the number of tweets with love and hate and visualize it. Or your could link the color of the screen with upcoming tweets: when "cold" appear you go toward blue, when "hot" appear you go toward red. Many visualization are possible, the one we'll create in the following part of this section has been a basis for numerous digital art installations.

If you're not too much in a rush, you might want to create a `String` global variable that would be used for the query, it'll be much much easier to modify your program. And as a bonus, don't hesitate to put that code too in the `void keyPressed() { ... }` function so you can trigger it with your keyboard.

##d) Displaying text
Let's start with displaying those string on the screen and not anymore just as log. For that, we'll use previously discovered function `text(String, posX, posY)` with a few added bonuses. Let's already display it on screen and build from there.

```java
void draw() {
  background(0);
  for (int i =0; i < listStatus.size(); i++) {
    // We use 50 + 50*i for the y value to have each line on there own axis
    text(listStatus.get(i).getText(), 10, 50*i);
  }

}
```

Cute but ... text can be better looking. Let's try something simple already: center everything. For that you'll need to put `textAlign(CENTER);` in the `setup()` function. If you launch your code, you'll see that everything is centered but ... on the left borded! This is because you draw at *x=10* defined in the `text(String, posX, posY)` function. You need to change that value foe the middle of the screen. Remember how to do that? If not here is how: `width/2`.

Better looking (is it?) but the font and size is ... not as best as could be. Let's change that. When coding about font, you have to take of a few things before using one. Lucky us, Processing has a built-in tool that simplify the process. Click in the menu on *Tools* -> *Create Font...*. A new interface will pop up, allowing you to chose both the font you want and its size. Once you're done, copy the text of your font (the fileName) and press OK. If you don't remember the name of your font, you can check its file by clicking in the menu on *Sketch* -> *Show Sketch Folder*. In our case, I picked *AGaramondPro-BoldItalic-38.vlw*. Now that it's created, we need to use it. As for all global variable, we'll need to declare it at the root of our code, instantiate in the setup and use it somewhere.

```java
// A new object: PFont. Used to store fonts. (P is for Processing)
PFont font;
 
void setup() {    
  size(displayWidth, displayHeight);   
  // Loading our font
  font = loadFont("AGaramondPro-BoldItalic-38.vlw");
  
  //Stating that it's the one we'll use from now
  textFont(font);

}
```

Since the font is much bigger, you might want to change the layout a bit (or chose a smaller one than I did!).

We're having now filtered information, a peak at the tweets, which is already a visualization. There is never objective way to look at things, by focusing on one specific side of it (filtering), we always tell a specific story.

Speaking of a story, let's try to make one that speaks more to the mind.

##c) Love & Hate

The idea is simple. Let's outline what we filtered upon, center on the word, and make it in a specific color. For that we need to process a bit our strings. First we need to separate the string in three part. Before our word defining the query, our word, and then the rest. In order to center on our word, we also need to know the length of both our word. Let's do that!

In order to separate the string, we'll use the `split(text, separator)`. This function breaks a String into pieces using a character or string as the delimiter, returning those pieces as an array of strings. For instance "I want to eat and to love and to breath" split with delimiter "and" will return the array {"I want to eat ", " to love ", " to breath"}. We'll use that to separate our strings in three. We'll use the word defining the query as a delimiter and voilà!

Being a bit in a rush, here is a working code, explained. Be sure to ask if you're not sure how it works.

 ```java
void draw() {    
  background(0);
  
  // Your query as a variable. If not already done so, put your query instead of "love".
  String exp = "love";

for (int i =0; i < listStatus.size(); i++) { // For all tweets
   
    // Separate the tweet
    String[] list = split(listStatus.get(i).getText(), exp); // if love was your query
    // We're offsetting the text by the first string and half our query
    float offset=width/2 -textWidth(list[0]) -textWidth(exp)/2;
    
    // Before your expression
    fill(255);
    text(list[0], offset, 50+50*i);
    offset += textWidth(list[0]); // Adding as offset the width of the first text
    
    // Your expression
    fill(255,0,0);
    text(exp, offset, 50+50*i);
    offset += textWidth(exp); // Same with our query
    
    // After your expression
    fill(255);
    for(int j=1; j<list.length; j++) { // Display all the remaining strings.
      text(list[j], offset, 50+50*i);
      offset += textWidth(list[j]); 
      
    }
  }
  
} 
```

For next episode, we'll try to make it a stream.

By the way, while it often results in a big mash-up pot of incoherency, you migth want to mix visualizations. You know how to handle text, tweet, getting data from the web and display it on a map. Does that spawn any crazy idea? If so, try them out!

## b) Books
Speaking about next episodes... There aren't enough hours in a night (and even less in a day), so the next two parts are ideas rather than real material. Don't hesitate to voice your ideas on those!

Getting books from [project Guntenberg](http://www.gutenberg.org/)
Parsing lines.
Same than before can be tried.
Frequency of a word in a book
Study the evolution of usage of a word over time.
Tree of words: Which words follow which (N tuplets...)

## c) DNA
Getting Human Genome from [project Guntenberg](http://www.gutenberg.org/ebooks/author/856)

Absolutely no idea yet, but it'll be great! Maybe thanks to you if you have already an idea!
