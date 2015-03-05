## Let's clean up some data and get it into a database

For this excersice we'll use some political contributions.

First let's see how many lines we have in our csv file

```$ wc -l data/contribs.csv```

Now let's take a peek at the data.

```head data/contribs.csv```

Looks like we'll have to clean up the date and amount fields for them to be valid date and amount fields in a database.

```cut -f9,10,11 data/contribs.csv```

There's a very useful set of tools for working with data that come as part of the [csvkit](https://csvkit.readthedocs.org/en/0.9.0/) package maintained by Christopher Groskopf.

You'll need to [install](http://csvkit.readthedocs.org/en/latest/install.html) it yourself but it's well worth your time and effort to get it up and running.

There's a utility called in2csv that is part of the package and it's great at cleaning up things like date fields. Take a look.

```cut -f9,10,11 data/contribs.csv | in2csv -f csv```

in2csv cleans up the dates great, but we'll need to clean up the amounts ourselves.

Something like this should work. We use the sed utility to search for dollar signs and commas and replace them with nothing. (Don't worry too much about the syntax we use with the sed command right now. It's easy to pick up if you decide it'll be helpful).

```cut -f9,10,11 data/contribs.csv | sed 's/[\$,\,,\)]//g'```

Now lets pass that to in2csv and see what we get back.

```cut -f9,10,11 data/contribs.csv | sed 's/[\$,\,,\)]//g' | in2csv -f csv```

Looks pretty good to me. Let's string it all together to get a clean csv for import into our database.

```cat data/contribs.csv | sed 's/[\$,\,,\)]//g' | in2csv -f csv```

Now let's shove it all into a sqlite database. Another cool csvkit tool is csvsql. Let's use that to write our create table statement in the sqlite dialect of sql.

```cat data/contribs.csv | sed 's/[\$,\,,\)]//g' | in2csv -f csv | csvsql -i sqlite --table contribs```

Better yet, let's create the table and insert the data too using csvsql. 

```cat data/contribs.csv | sed 's/[\$,\,,\)]//g' | in2csv -f csv | csvsql --table contribs --db sqlite:///contribs.sqlite```

Can you guess which part of the command we need to take out based on the error?

Instead, try:

```cat data/contribs.csv | sed 's/[\$,\,,\)]//g' | in2csv -f csv | csvsql --table contribs --db sqlite:///contribs.sqlite --insert```

If the table already exists then we need to delete the contribs table first.

```sqlite3 contribs.sqlite```

```sqlite> DROP TABLE contribs;```

```sqlite> SELECT * FROM contribs;```

To get out of the sqlite3 shell

```sqlite> .exit``

Now this should work:

```cat data/contribs.csv | sed 's/[\$,\,,\)]//g' | in2csv -f csv | csvsql --table contribs --db sqlite:///contribs.sqlite --insert```

We'll query the master table list to see if our table is indeed there.

```sqlite3 contribs.sqlite```

```sqlite> SELECT * FROM sqlite_master;```

How many records got inserted?

```sqlite> SELECT COUNT(*) FROM contribs;```

How much money we talkin?

```sqlite> SELECT SUM(Amount) FROM contribs;```

And remember, to get out of the sqlite3 shell

```sqlite> .exit```

There are [lots of other useful tools](https://source.opennews.org/en-US/articles/eleven-awesome-things-you-can-do-csvkit/) in csvkit to explore. Here are a couple examples:

Execute sql queries directly on a file to limit and export a limited slice just for your state

```csvsql --query "SELECT * FROM contribs WHERE STATE = 'GA'" data/contribs.csv > contribs_ga.csv```

Check it out.

```$ cat contribs_ga.csv```

Get summary statistics

```csvstat data/contribs.csv```

