terminal_recipes
================

NICAR 2015 class to introduce reporters to the power of the terminal. Nothing fancy, just the fundamentals. Contributions welcome! Share your knowledge.

This is designed to be Part 2 of a beginners' class: lightly touching on the basics and then getting into more interesting tools (fetching from the web, intermediate data wrangling, etc.)

Possible areas this course will cover:

Reviewing the basics:

* Navigation
    * cd = changing directories
    * cd .. = move up one directory
      * cd ../.. = move up two directories
    * ls = listing files/folders
    * pwd = print working directory (for when you get lost)
    * mkdir = make a new folder 
    * ctrl + a = move to beginning of line
    * ctrl + e = move to end of line
    * ctrl + c = stop process

* Basic data wrangling
    * head = looking at the first few rows of a spreadsheet
    * tail = looking at the last few rows of a spreadsheet
    * head original_filename.csv > firstfewrows.csv = exporting the first few rows of a big spreadsheet
    * wc -l = counting the total number of rows
    * vim = powerful if hard to learn file editor
      * You'll want to know this, but we won't be able to get to the details.
      * Your Mac comes with a good built in tutorial. Go to your terminal and type 'vimtutor'
    * egrep = powerful tool to search files
    * uniq = file inspection for obvious duplicate records
      * uniq -d filename = print only duplicate repeated lines in file

Intermediate stuff: 

* Fetch things from the interwebs
    * wget
    * cURL

* Intermediate data wrangling
    * csvkit
    * sqlite (from commandline)

And an important P.S.:

Why you need to learn Git:
* [Chapters 1-3 of the Pro Git book will give you a good, relatively quick overview](http://git-scm.com/book/en/v2/Getting-Started-About-Version-Control)

If you end up spending any amount of time on the terminal on a regular basis get this book:

[Linux Pocket Guide, 2nd Edition](http://shop.oreilly.com/product/0636920023029.do?green=B78D23C2-6E87-58C8-BAE1-0090A206787F&intcmp=af-mybuy-0636920023029.IP)

Where else to get help (TK)
