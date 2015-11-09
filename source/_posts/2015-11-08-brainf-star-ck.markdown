---
layout: post
title: "Brainfuck"
date: 2015-11-08 23:26:01 -0500
comments: true
categories: 
---
I was doing some reading on different programming languages, and I wondered to myself, what is the smallest programming language out there? After a quick search, I came accross the esoteric programming language that is Brainfuck.

Brainfuck was created by this guy (Urban Müller) in 1993 (coincidentally the same year that Matz created Ruby):

![Urban Müller](/images/110815/urban.jpg)

The language is limited to just 8 (!) commands. The compiler Müller built was a mere 240 bytes in size, and apparently people have succeeded in building a compiler that is under 200 bytes.

|__Character__|__Meaning__|__C Equiv__|
|:-------:|:-------:|:-----:|
| >       |increment the data pointer (to point to the next cell to the right).|++p;|
| <       |decrement the data pointer (to point to the next cell to the left).|--p;|
| +       |increment (increase by one) the byte at the data pointer.|++*p;|
| -       |decrement (decrease by one) the byte at the data pointer.|--*p;|
| .       |output the byte at the data pointer.|putchar(p);|
| ,       |accept one byte of input, storing its value in the byte at the data pointer.|*p=getchar();|
| [       |if the byte at the data pointer is zero, then instead of moving the instruction pointer forward to the next command, jump it forward to the command after the matching ] command.|while(*p) {|
| ]       |if the byte at the data pointer is nonzero, then instead of moving the instruction pointer forward to the next command, jump it back to the command after the matching [ command.|}|

.

Being unfamiliar with C, I didn't know what pointers were. Bill Karwin gives a good explanation on his blog [here](http://karwin.blogspot.com/2012/11/c-pointers-explained-really.html). Pointers basically allow a programmer to  access memory directly. From Wikipedia:

>A pointer is a programming language object, whose value refers to (or "points to") another value stored elsewhere in the computer memory using its address. A pointer references a location in memory, and obtaining the value stored at that location is known as dereferencing the pointer. As an analogy, a page number in a book's index could be considered a pointer to the corresponding page; dereferencing such a pointer would be done by flipping to the page with the given page number.


So Brainfuck uses an array of at least 30,000 byte-sized cells initialized to zero and uses a movable data pointer to reference these cells.

Here is what "Hello World!" looks like:

```
++++++++++[>+++++++>++++++++++>+++>+<<<<-] >++.>+.+++++++..+++.>++.<<+++++++++++++++.>.+++.------.--------.>+.>.
```

Here it is with some comments to get a better understanding of what is going on:

```
[ This program prints "Hello World!" and a newline to the screen, its
  length is 106 active command characters. [It is not the shortest.]

  This loop is a "comment loop", a simple way of adding a comment
  to a BF program such that you don't have to worry about any command
  characters. Any ".", ",", "+", "-", "<" and ">" characters are simply
  ignored, the "[" and "]" characters just have to be balanced. This
  loop and the commands it contains are ignored because the current cell
  defaults to a value of 0; the 0 value causes this loop to be skipped.
]

 +++++ +++++            initialize counter (cell #0) to 10
[                       set the next four cells to 70, 100, 30 and 10
  > +++++ ++            add  7 to cell #1
  > +++++ +++++         add 10 to cell #2
  > +++                 add  3 to cell #3
  > +                   add  1 to cell #4
  <<<< -                decrement counter (cell #0)
]                 

The result of this is:
Cell No :   0   1   2   3   4
Contents:   0   70  100 30  10
Pointer :   ^

> ++ .                print 'H'  (H = ASC (72))
> + .                 print 'e'  (e = ASC (101))
+++++ ++ .            print 'l'  (l = ASC (108))
.                     print 'l'  (l = ASC (108))
+++ .                 print 'o'  (o = ASC (111))

> ++ .                print ' '   ( = ASC (32))

<< +++++ +++++ +++++ .  print 'W' (W = ASC (87))
> .                   print 'o'   (o = ASC (111))
+++ .                 print 'r'   (r = ASC (114))
----- - .             print 'l'   (l = ASC (108))
----- --- .           print 'd'   (d = ASC (100))
> + .                 print '!'   (! = ASC (33))
> .                   print '\n'  
```

There is a great walkthrough of the code in a source I found called [Brainfuck for Dummies](https://docs.google.com/document/d/1M51AYmDR1Q9UBsoTrGysvuzar2_Hx69Hz14tsQXWV6M/edit#) (no author given on the document):

```
The program starts at the first command and also at the first memory location, which will be called a[0]. The next memory location will be called a[1], the one after that a[2], etc. 
As you may recall, all memory cells have the value zero at the start of the program.

1. The first line sets a[0] to 10 by simply incrementing the contents of the cell ten times.

2. On the 2nd line the [ character starts a loop. The loop would end immediately if the value of the current memory cell was zero. The value is ten, so the program continues.

3. The loop sets the values for the four cells: 
a[1] = 70 (close to 72, the ASCII code for the character 'H'), 
a[2] = 100 (close to 101 or 'e'), 
a[3] = 30 (close to 32, the code for space) and 
a[4] = 10 (newline). 

4. Each pass of the loop, the following things happen:
First the cursor is moved one place to the right (a[1]).
Then the value of the current cell (a[1]) is incremented by seven.
a[2] is incremented by ten
a[3] is incremented by three and lastly
a[4] is incremented by one.

5. The seventh line moves the cursor all the way back to the first position a[0] and then decreases the value of this cell by one. Thus the loop will be executed ten times[5]. After the loop is finished, a[0] is zero.

6. >++. then moves the pointer to a[1] which holds 70, adds two to it (72 is the ASCII character code of a capital H), and outputs it with the "." command.

7. The next line moves the array pointer to a[2] and adds one to it, producing 101, a lower-case 'e', which is then output.

8. Since 'l' is the seventh letter after 'e', to output 'll' another seven are added (+++++++) to a[2] and the result is output twice.

9. 'o' is the third letter after 'l', so a[2] is incremented three more times. Then the contents of the cell is written to the screen.

10. For the space and capital letters, different array cells are selected and incremented or decremented as needed.
```

ASCII table for reference:

![ASCII table](/images/110815/ascii.png)

Brainfuck is a Turing-complete language, meaning it theoretically can solve any computational problem (with enough time and memory), although why anyone would want to use it for anything but amusement is beyond me. It seems to have been based off of a predecessor called P'', created by Corrado Böhm in 1964, which uses the equivalent of 6 Brainfuck characters (no input or output). 

There are quite a few other esoteric languages out there; languages that were created without real practical purpose, usually as a joke. Malbolge, for example, was designed to be as difficult to program in as possible. Ook! is a variation of Brainfuck meant for Orangutangs where all of Brainfuck's 8 characters have been replaced with some combination of "Ook!", "Ook?", and "Ook.". Here is "Hello World!":

```
 Ook. Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook.
 Ook. Ook. Ook. Ook. Ook! Ook? Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook.
 Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook? Ook! Ook! Ook? Ook! Ook? Ook.
 Ook! Ook. Ook. Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook.
 Ook. Ook. Ook! Ook? Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook?
 Ook! Ook! Ook? Ook! Ook? Ook. Ook. Ook. Ook! Ook. Ook. Ook. Ook. Ook. Ook. Ook.
 Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook! Ook. Ook! Ook. Ook. Ook. Ook. Ook.
 Ook. Ook. Ook! Ook. Ook. Ook? Ook. Ook? Ook. Ook? Ook. Ook. Ook. Ook. Ook. Ook.
 Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook! Ook? Ook? Ook. Ook. Ook.
 Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook? Ook! Ook! Ook? Ook! Ook? Ook. Ook! Ook.
 Ook. Ook? Ook. Ook? Ook. Ook? Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook.
 Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook! Ook? Ook? Ook. Ook. Ook.
 Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook. Ook.
 Ook. Ook? Ook! Ook! Ook? Ook! Ook? Ook. Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook.
 Ook? Ook. Ook? Ook. Ook? Ook. Ook? Ook. Ook! Ook. Ook. Ook. Ook. Ook. Ook. Ook.
 Ook! Ook. Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook.
 Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook! Ook!
 Ook! Ook. Ook. Ook? Ook. Ook? Ook. Ook. Ook! Ook.
```

Another one, ArnoldC, replaces all basic keywords with quotes from different Arnold Schwarzenegger movies. "Hello World!", for example:

```
IT'S SHOWTIME
TALK TO THE HAND "hello world"
YOU HAVE BEEN TERMINATED
```

Check [Wikipedia](https://en.wikipedia.org/wiki/Esoteric_programming_language) or [Esolang](http://esolangs.org/wiki/Main_Page) for some other fun esoteric languages.