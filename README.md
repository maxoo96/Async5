# async-session-files

Welcome to this async session.  Today you'll going to learn more about how to
read and write files in Python.

You can follow the video here:

https://www.youtube.com/watch?v=_8bKuFa2CEE

## Reading files

We use the `open()` function to read a file in the given path, for example:

```python
open("hola.txt")
```

Will allow you to read the contents of `hola.txt`.  If we want to read the
contents of the file, we can do the following:

```python
file = open("hola.txt")

for line in file:
    print(line)

file.close()
```

Notice the `file.close()` line we have right there?  we must always close files
after using them, otherwise we may introduce some bugs in our program.

However, there is a way for Python to handle the opening and closing for us,
using the `with` keyword:

```python
with open("hola.txt") as file:
    for line in file:
        print(line)
```

using the `with` is handy because Python will automatically close the file for
us after we've finished using it.  Notice that all parts of code that need
access to the `file` vairable need to go inside the `with` block (we put them
inside indenting them).

## writing files

Writing files is not that different to reading them, we just need to tell `open`
the mode in which we'll open the file, in read or write mode.

```python
names = ["Johhny", "Joey", "Markee", "Dee-dee"]

with open("names", "w") as file:
    for name in names:
        file.write(name + "\n") # the \n string means add a new line
```

## CSV

### Reading CSV

Finally, now that we know how to open a file, we'll see how to deal with CSV
data.  In the root of the repository there's `records.csv`, a file containing some
CSV data.

we can read CSV data using the `csv` library:

```python
import csv

with open("records.csv") as file:
    reader = csv.reader(file)
    for row in reader:
        println(row[2] + " " + row[5])
```

Also, if the CSV file has a header (a first line indicating the column names), we can read rows as if they were dictionaries.

```python
import csv

with open('records.csv') as file:
    reader = csv.DictReader(file)
    for row in reader:
        print(row['first_name'], row['last_name']) # See we're now accessing values by 
                                                   # key, not index
```

### Writing CSV

Once again, for writing CSV we'll just change a couple of details


```python
import csv

beatles = [
    {"name": "John Lennon", "role": "singer"},
    {"name": "Paul McCartney", "role": "bass"},
    {"name": "George Harrison", "role": "guitar"},
    {"name": "Ringo Starr", "role": "drums"},
]

with open("records.csv", "w") as file:
    header = ["name", "role"]
    writer = csv.DictWriter(file)
    writer.writeheader()
    for beatle in beatles:
        writer.writerow(beatle)
```