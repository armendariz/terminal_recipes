# Baby Names Example

Here's a fun example of a common problem. You download a zip archive with a bunch of files that need to be combined.
Then you want to quickly see what's in them.

Here's a quick way to do that all from the terminal. And since you're working under the hood of the computer it's pretty fast work.

We're going to work with the [Baby Names from Social Security Card Applications-National Level Data](http://catalog.data.gov/dataset/baby-names-from-social-security-card-applications-national-level-data) available on Data.gov.

First, grab the data from Data.gov to your machine.

```$ wget http://www.ssa.gov/oact/babynames/names.zip```

Extract the data.

```$ unzip names.zip```

Smush it all into one file quickly.

```$ cat *.txt > baby_names_1880_2013.txt```

Check out the new file.

```$ ls```

How many lines of data we got?

```$ wc -l baby_names_1880_2013.txt```

Smush it all together, but this time record what file each row came from.
So kill the file we just created, then use grep to smush them back together.

```$ rm baby_names_1880_2013.txt```

```$ grep "" *.txt > baby_names_1880_2013.txt```

Check out the new file.

```$ ls```

How many lines of data we got?

```$ wc -l baby_names_1880_2013.txt```

Check out the first few rows.

```$ head baby_names_1880_2013.txt```

Okay, but what's the baby name most often given? I gotta know!
Let's print the third column to the screen then sort it in ascending order.

```$ awk -F "," '{print $3}' baby_names_1880_2013.txt | sort -n```

Okay, there's the biggest number, but what name is it associated with?

```$ egrep 99674 baby_names_1880_2013.txt```

Let's look at a few of the big names at once.

```$ egrep 90512\|90629\|90994\|91652\|92711\|94758\|96210\|99674 baby_names_1880_2013.txt```