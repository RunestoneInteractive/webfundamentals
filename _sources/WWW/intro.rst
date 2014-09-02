.. This work is licensed under a Creative Commons Attribution 4.0 License
   Brad Miller, Luther College


Introduction
============

You are reading this introduction, probably in a browser of some kind. Maybe on your tablet, maybe on your smartphone, or maybe on a regular old desktop computer.  The key question we want to answer in this chapter is how does this page get to your screen?  It turns out there is an awful lot of computer science involved.  We won't go very deep, this is only the first chapter, in a book that is meant to be introductory in nature after all.


For now we'll start out with a very high level overview and move down a little deeper later in the chapter.   The page you are seeing is the result of a **web browser** communicating with a **web server**.  A number of important things happen during the comversation.

* The browser and the server "talk" to each other using a relatively simple **protocol** called **HTTP**, which stands for the Hyper Text Transfer Protocol.
* If we break down HTTP into its two components we get a little more detail:

  * Hyper Text - The idea of hyper text is that it links you from one page to another (we used to call the links (hyperlinks) but that has been shortened to just links.  However, the concept of Hyper Text is central to this course in that the specific text that is transferred follows a standard called the **Hyper Text Markup Language** (HTML).

  * Transfer Protocol - when two programs want to talk to each other both programs have to "speak the same language."  A protocol is a very specific description of a series of messages that two programs use to communicate.

* The web server sends the HTML to the browser over the internet and the browser **renders** the HTML into the nicely formatted page that you see on your screen.

At the beginning of the World Wide Web there was only HTML, and web pages were a bit drab compared to what we are used to seeing today.  Now modern web pages rely on three technologies, which will be the main focus of this book.

* HTML -- Hyper Text Markup Language -- HTML describes the content of the page, giving the page some sctructure including common things like headings, and sections, and lists of things.
* CSS -- Cascading Style Sheets -- CSS desribes the "look" of the page, the colors, the fonts, the margins, etc.
* Javascript is used to change the behavior of the page.  What happens when  you click on a button, or scroll a scrollbar, or hover over something with your mouse.








