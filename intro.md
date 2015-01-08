## Why use the command line?

Powerful, modular tools exist under the hood of Unix systems that will make your life so much easier.

We're talking hard core, old-schoool, neckbeard geekery.

And because you've opted to ditch the GUI these tools are fast.

These aren't some random CNET download that you pray isn't a virus and will actually work as advertised.

They are mature pieces of software designed and maintained by an army of open source software engineers.

God bless them.

I for one am eternally grateful for their expertise and generosity.



## Fine so where do I find the "command line?"

OS X, Ubuntu or other Unix systems all have a "terminal"

Open it up.

Say hi.

```$ echo Hi!```

Using OS X? Really say Hi!

```$ say Hi!```

That's cute, but I have to type everyting for the stupid computer to say. Boring.

Fine. You aren't impressed.

If you're using Mac (OS X) Have it recite poetry for you then.

```$ cat data/poe_the_raven.txt | say```

Okay, that's a weak gimmick, but it's a technique you'll want to employ often.

We use the "cat" command to print the text file. Then we pipe ("|") the text to the say command.

Chaining these modular commands together is a very powerful way to get work done.

To stop the poor computer hit control + c

It's too literal for poetry.




## A quick refresher on command line navigation

Quickly switch between screens (like this web page and the terminal).

OS X: command + tab

Seemingly everyone else: alt + tab

Find out where you are at.

```$ pwd```

See what's in the directory revealed when you printed your working directory "pwd."

```$ ls```

Move into a directory inside your current directory.

```$ cd data```

See what's in here.

```$ ls```

Move back to the directory you were just in.

```$ cd ..```

Don't forget about tab completion. If you type a portion of a directory or a command and hit tab, the terminal will write the rest.

Type "cd d" then hit tab. The terminal should then complete your comand like so: "cd data/"

For really long file or directory names, tab completion really saves time.

Open a file. Hint: use tab completion to finish the name of the text file.

```$ open data/poe_the_raven.txt```

On Ubuntu you'd use "xdg-open."

Move back to your home directory quickly.

```$ cd ~```

Close your terminal.

```$ exit```

That should be enough for you to be able to move around your 
