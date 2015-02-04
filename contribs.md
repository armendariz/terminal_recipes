## Let's clean up some data and get it into a database

For this excersice we'll use some political contributions.

First let's see how many lines we have in our csv file

```$ wc -l data/contribs.csv```

Now let's take a peek at the data.

```head data/contribs.csv```

Looks like we'll have to clean up the date and amount fields for them to be valid date and amount fields in a database.

```cut -f9,10,11 data/contribs.csv```

There's a very useful set of tools for working with data that come as part of the [csvkit](https://csvkit.readthedocs.org/en/0.9.0/) package maintained by Christopher Groskopf.

You'll need to install it yourself but it's well worth your time and effort to get it up and running.

There's a utility called in2csv that is part of the package and it's great at cleaning up things like date fields. Take a look.

```cut -f9,10,11 data/contribs.csv | in2csv -f csv```

in2csv cleans up the dates great, but we'll need to clean up the amounts ourselves.

Something like this should work. We use the sed utility to search for dollar signs and commas and replace them with nothing.

```cut -f9,10,11 data/contribs.csv | sed 's/[\$,\,,\)]//g'```

Now lets pass that to in2csv and see what we get back.

```cut -f9,10,11 data/contribs.csv | sed 's/[\$,\,,\)]//g' | in2csv -f csv```

Looks pretty good to me. Let's string it all together to get a clean csv for import into our database.

```cat data/contribs.csv | sed 's/[\$,\,,\)]//g' | in2csv -f csv```

Now let's shove it all into a sqlite database. Another cool csvkit tool is csvsql. Let's use that to write our create table statement in the sqlite dialect of sql.

```cat data/contribs.csv | sed 's/[\$,\,,\)]//g' | in2csv -f csv | csvsql --tabs -i sqlite --table contribs```

Better yet, let's create the table and insert the data too using csvsql.

```cat data/contribs.csv | sed 's/[\$,\,,\)]//g' | in2csv -f csv | csvsql --tabs -i sqlite --table contribs --db sqlite:///contribs.sqlite --insert```

Let's check it out.

```sqlite3 contribs.sqlite```

We'll query the master table list to see if our table is indeed there.

```sqlite> SELECT * FROM sqlite_master;```

How many records got inserted?

```sqlite> SELECT COUNT(*) FROM contribs```

How much money we talkin?

```sqlite> SELECT SUM(Amount) FROM contribs;```

To get out of the sqlite3 shell

```sqlite> .exit```