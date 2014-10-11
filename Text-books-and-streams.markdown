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

Better looking (is it?) but the font and size is ... not as best as could be. Let's change that.
text()
centered text
PFont

##c) Filtering your text
simple display with red
split
textWidth



 
Process: filter with start of sentences
Plot: Organised text (potentialy dynamic)

I am...
I have ....

... loves ...
... hates ...

... then ...

Even better : stream (for next episode...)

## b) Books
 Getting books from project Guntenberg (and DNA). (Better downloading it than taking it form the web straight from application)
 Parsing lines.
 
 Same than previously can be done.
 
 Frequency of a word in a book
 Study the evolution of usage of a word over time (biggggg data base).
 
 Tree: following of words (N tuplets...)


## c) DNA

Something about ADN ?



        Data: Twitter feed
            http://blog.blprnt.com/blog/blprnt/quick-tutorial-twitter-processing
            http://blog.blprnt.com/blog/blprnt/updated-quick-tutorial-processing-twitter
            http://codigogenerativo.com/twitter-para-processing-2-0/


