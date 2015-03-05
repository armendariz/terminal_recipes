# Baby Names Example

Here's a fun example of a common problem. You download a zip archive with a bunch of files that need to be combined.
Then you want to quickly see what's in them.

Here's a quick way to do that all from the terminal. And since you're working under the hood of the computer it's pretty fast work.

We're going to work with the [Baby Names from Social Security Card Applications-National Level Data](http://catalog.data.gov/dataset/baby-names-from-social-security-card-applications-national-level-data) available on Data.gov.

First, let's make a folder where we want to put the data we're about to download:

```$ mkdir my_folder```

Then grab the data from Data.gov to your machine. (A quick footnote: wget is not installed on your machine by default. You may need to install it on your personal computer)

```$ wget http://www.ssa.gov/oact/babynames/names.zip```

Extract the data.

```$ unzip names.zip```

Check out the new files.

```$ ls```

How many rows we talkin in the first file?

```$ wc -l yob1880.txt```

How many rows we talkin in all the files in this folder?

```$ wc -l *.txt```

Let's look at the first few rows of one.

```$ head yob1880.txt```

And the last few rows.

```$ tail yob1880.txt```

Smush it all into one file quickly. We use the 'cat' command to read all the files in our folder ending in .txt and then send the output to a new file. (Here's a [more detailed explanation](http://www.linfo.org/cat.html))

```$ cat *.txt > baby_names_1880_2013.txt```

How many lines of data we got in the smushed file?

```$ wc -l baby_names_1880_2013.txt```

Smush it all together, but let's do it again and record what file each row came from. 

So kill the file we just created.

```$ rm baby_names_1880_2013.txt```

To smush it back together and record what file each row came from, we need to talk about a command called 'grep.' The grep command can search for a specific string. When you're searching across multiple files, it has the added benefit of telling you which file it found the string in.

A simple use of this command would be:

```$ grep "Agustin" *.txt```

Let's smush all files in our current directly that end in .txt

```$ grep "" *.txt > baby_names_1880_2013.txt```

Check out the new file.

```$ ls```

How many lines of data we got?

```$ wc -l baby_names_1880_2013.txt```

What do the first few rows look like?

```$ head baby_names_1880_2013.txt```

Maybe we want to export one of these slices to look at in excel:

```head baby_names_1880_2013.txt > baby_names_first_few_rows.csv```

Okay, but what's the baby name most often given? I gotta know!

Since the file is large, let's do a test on a smaller batch. The awk command is more flexible than grep, and makes it easy to within a specific column.

When you're combining two commands you use a pipe (|). Let's print the third column to the screen then sort it in ascending order. The -d, tells the cut command that the file is comma-sepparated. The -f3 tells it to look for the third column.

```$head baby_names_1880_2013.txt | cut -d, -f3```

And if we wanted to grab the third column from the whole file?

```cut -d, -f3 baby_names_1880_2013.txt``` 

And sort it too? The -n says 'sort by numerical value,' instead of treating these numbers a text. Try it without the -n if you want to see the result.

```cut -d, -f3 baby_names_1880_2013.txt | sort -n```

Okay, there's the biggest number, but what name is it associated with?

```$ egrep 99674 baby_names_1880_2013.txt```

Let's look at a few of the big names at once.

```$ egrep 90512\|90629\|90994\|91652\|92711\|94758\|96210\|99674 baby_names_1880_2013.txt```
