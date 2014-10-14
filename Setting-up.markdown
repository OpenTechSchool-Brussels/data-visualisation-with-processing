---
layout: default
title:  "Setting up"
num: 0

---

Let’s get it started.

##a) What is Processing?##
Processing (or P5) is a programming environment, made by artist, with art creation in mind. It is a set of tools, including a programming language, designed to facilitate the use of software within the visual arts, and to promote visual representations within technology. Processing is focused on making digital creation simple and fun, with an emphasis on visuals and interactions. This makes it particularly fitted for makers, designers and visual artists.

There are many solution for creating visuals, some more or less close to classical programming language. One of the interesting point of Processing is that it’s a classic programing language. What learn here will help you dwell deeper (if you want) into any other language. Even more, Processing is actually a subset of Java (a classic programing language) so whatever you learn from Java, you can use straight in Processing to buff your creations.

Further more, Processing is an open source language. This means that you have access to the code, and you can do pretty much whatever you want with it. This open source mind is all about sharing, and building together. If you create with Processing, think about releasing your creation in open source so that other people can learn from your work!


##b) Setting up Processing##
To set up processing, just download it : https://www.processing.org/download/

*   Windows: Extract the .zip file you just download anywhere you want (a classic is the Program Files folder, but your desktop will do). Enter the newly extracted folder, and double click on “processing.exe” to start.
*   Mac OS X: Unzip your download file, and drag the Processing icon to the Applications folder (or your desktop if you don’t have the right to the Applications folder). Double-click the Processing icon to start.
*   Linux: Untar your downloaded .tar.gz file and enter the directory you just created. Run processing with the command ./processing.

You should have now in front of you the Processing environment open. It’s similar on all system, so if you share your code, people should have no issue making it run.


##c) Running your first program##
Okay, you’re in front of your command center, now what?
Well, you can see three main zone. On top, the menu. On the bottom, some place for Processing to give you feedback, especially useful when you’ve messed up something (you will, and part of learning how to code is to learn to enjoy that!). In the center, the main stage where you shine, where you write your code. A processing file is called a sketch.
The menu allow you basic control you can explore by yourself (new, save, open, exit…) sometimes redundant in the icons you can see. Some controls are more specific to Processing, and the two main that will be interested in are run (Triangle shape for the icon, and keyboard shortcut Ctrl/Cmd + R) and stop (Square shape for the icon).

Now that you’re super at ease in this new jungle, let’s actually write something. As mentioned before (maybe), even if you can copy paste the code from this material to your sketch, you shouldn’t. Not only because we love to torture you, but also because you will learn way more this way. You’ll not only remember reading, but remember writing. And you always remember more by doing.

One of the classic first programs one writes is called “hello world”, which basically outputs the text `“hello world”` on your screen. We could do that (`println(“hello world”);`) but the basic output of Processing is graphic not text. So let’s write:

```java
rect(25,25,50,50);    
```

What did it do? If you run that (pressing the icon, “run” in the menu or with your keyboard shortcut), you should see your canvas, with a square in the middle. Kudos, say the size of the rectangle correspond to world population and you're already making data visualization! All the next steps are just details. But before you leave full of pride, let us analyze this line.

What you called is a function, and you fed it with parameters, four to be precise. The function is `rect` and you feed it with parameters in between parenthesis, separated by a comma. So if the function had no parameters, it should be written as `rect()`. You can try to run such a function, Processing will shout at you (gently, but in red) telling you that no, you can’t do that in this house, and that `rect` is patiently waiting for four parameters. At the end of the line lie a quiet `;`. Its function is to say that this particular command has finished. A common mistake is to forget to put it at the end of commands.


##d) Data Visualization

Data visualisation is a field where data is not just states but visualy shared, using a medium that is more human. This way, humans can make more of the data set, get more of the information and single out the salient point more easily.

Before anything else, Data Visualisation is Design, and hence is about sharing something, an information. It's not about data decoration but about a story, a focus on what the reader will get. Data Visualisation is just one tool (among many) to share information. Use it accordingly, with a focus on the message.

You can single out two kind of content/story, either you have a message you want to share through the data and how you display it, or you want to allow the user to explore your visualisation for him/her to make his/her own story. You're never completly on one or the other side, but both extreme are good to keep in mind while giving a direction to your work.

All in all, Data Visualisation is a powerfull tool for reasoning and communicating about data in a more human friendly way.

Last, be aware of the limitation of the tool. When sharing a message through Data visualisation, you're dependent on the data, its quality and potential bias. Beside, how you use the data might heavily mislead the reading of it. Always be clear and concise, but keep in mind that the mere fact that you have a story in mind might end up as manipulation.


##e) Data (input)
Data is what you will feed your system, what you will use to display.

DataSet / DataBase
Kind of data (stream, text, graphs network/trees, tables, CSV, JSON, XML)
Variety of data, and of data type, and of info you can get from it. 
as an inspiration
Get data, filter data, process data, organise it, visualise it



##f) Medium (output)
Static Vs Dynamic Vs Interactive
Print, website, tablet/smartphone, computer screen, projections...
To each medium its specificity

SENSIBILITY TO ADD IN INDEX

On a side note, it is important to see code as what it is: a medium that allow for multiple kind of creation, art & design among others. Having a good grasp of what code is allow you to better understand its possibilities and precise your sensibility. Code is a language, a medium, with which you can do many things. You can draw, write poems or sign contracts with a pen. Same with code. And it’s by its practice, its knowledge and the culture you will create that will emerge interesting digital art, design, prototypes... Many thing can be said of the nature of code, and while that would be very interesting to develop, that is out of the scope of this workshop. While that is true, I hope this workshop will make you see how poetic code can be, even if it’s sometimes frustrating: as any deep and complex language is when you are learning it.

