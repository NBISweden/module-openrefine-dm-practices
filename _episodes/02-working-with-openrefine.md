---
title: "Working with OpenRefine"
teaching: 15
exercises: 20
questions:
- "How can we bring our data into OpenRefine?"
- "How can we sort and summarize our data?"
- "How can we find and correct errors in our raw data?"
objectives:
- "Create a new OpenRefine project from a CSV file."
- "Understand potential problems with file headers."
- "Use facets to summarize data from a column."
- "Use clustering to detect possible typing errors."
- "Understand that there are different clustering algorithms which might give different results."
- "Employ drop-downs to remove white spaces from cells."
- "Employ drop-downs to split values from one column into several columns."
- "Manipulate data using previous steps with undo/redo."
keypoints:
- "OpenRefine can import a variety of file types."
- "OpenRefine can be used to explore data using filters."
- "Clustering in OpenRefine can help to identify different values that might mean the same thing."
- "OpenRefine can transform the values of a column."
---

# Lesson

## Creating a new OpenRefine project

In Windows, you can start the OpenRefine program by double-clicking on the openrefine.exe file. Java services will start automatically on your machine, and OpenRefine will open in your browser. On a Mac, OpenRefine can be launched from your Applications folder. If you are using Linux, you will need to navigate to your OpenRefine directory in the command line and run `./refine`.

OpenRefine can import a variety of file types, including tab separated (`tsv`), comma separated (`csv`), Excel (`xls`, `xlsx`), JSON, XML, RDF as XML, and Google Spreadsheets. See the [OpenRefine Importers page](https://github.com/OpenRefine/OpenRefine/wiki/Importers) for more information.

In this first step, we'll browse our computer to the sample data file for this lesson.
In this case, we will be using data obtained from interviews of farmers in two countries in eastern sub-Saharan Africa (Mozambique and Tanzania).
Instructions on downloading the data are available
[here]({{site.baseurl}}/setup.html).

Once OpenRefine is launched in your browser, the left margin has options to `Create Project`, `Open Project`, or `Import Project`. Here we will create a new project:

1. Click `Create Project` and select `Get data from` `This Computer`.
2. Click `Choose Files` and select the file `SAFI_openrefine.csv` that you downloaded in the [setup step]({{site.baseurl}}/setup.html). Click `Open` or double-click on the filename.
3. Click `Next>>` under the browse button to upload the data into OpenRefine.
4. OpenRefine gives you a preview - a chance to show you it understood the file. If, for example, your file was really tab-delimited, the preview might look strange. You would then choose the correct separator in the box shown and click `Update Preview` (middle right). If this is the wrong file, click `<<Start Over` (upper left).  There are also options to indicate whether the dataset has column headers included and whether OpenRefine should skip a number of rows before reading the data.
![Parse Options](../fig/OR_01_parse_options.png)

5. If all looks well, click `Create Project>>` (upper right).

Note that at step 1, you could upload data in a standard form from a web address by selecting `Get data from` `Web Addresses (URLs)`. However, this won't work for all URLs.

## Using Facets

*Exploring data by applying multiple filters*

Facets are one of the most useful features of OpenRefine and can help both get an overview of the data in a project as well as helping you bring more consistency to the data. OpenRefine supports faceted browsing as a mechanism for

* seeing a big picture of your data, and
* filtering down to just the subset of rows that you want to change in bulk.

A 'Facet' groups all the like values that appear in a column, and then allow you to filter the data by these values and edit values across many records at the same time.

One type of Facet is called a 'Text facet'. This groups all the identical text values in a column and lists each value with the number of records it appears in. The facet information always appears in the left hand panel in the OpenRefine interface.

Here we will use faceting to look for potential errors in data entry in the `sex` column.

1. Scroll over to the `sex` column.
2. Click the down arrow and choose `Facet` > `Text facet`.
3. In the left panel, you'll now see a box containing every unique value in the `sex` column
along with a number representing how many times that value occurs in the column.
4. Try sorting this facet by name and by count. Do you notice any problems with the data? What are they?
5. Hover the mouse over one of the names in the `Facet` list. You should see that you have an `edit` function available.
6. You could use this to fix an error immediately, and OpenRefine will ask whether you want to make the same correction to every value it finds like that one. But OpenRefine offers even better ways to find and fix these errors, which we'll use instead. We'll learn about these when we talk about clustering.

> ## Solution
> - 23 entries are missing a value for sex.
> - `mael` is likely a mis-entry of `male`.
> - `F`, `f`, `female` and `Female` refer to the same sex. We will see how to correct these misspelled and mistyped entries in a later exercise.
{: .solution}

> ## Exercise 1.1
>
> 1. Using faceting, find out for how many `date` values more than one animal was registered.
>
> 2. Is the column formatted as Text or Date?
>
> 3. Use faceting to produce a timeline display for `date`. You will need to use `Edit cells` > `Common transforms` > `To date` to convert this column to dates.
>
> 4. During which month were most of the animals registered?
>
> > ## Solution
> >
> > For the column `date` do `Facet` > `Text facet`. A box will appear in the left panel showing that there are 95 unique entries in
> > this column.
> > By default, the column `date` is formatted as Text. You can change the format by doing `Edit cells` > `Common transforms` >
> > `To date`.  Notice the the values in the column turn green. Doing `Facet` > `Timeline facet` creates a box in the left panel that shows a histogram of the number of entries for each date.
> >
> > Five dates had more than one animal registered. Most of the animals were registered in January of 2019 (seen by the tallest bar in the timeline facet).
> {: .solution}
{: .challenge}

> ## More on Facets
> [OpenRefine Wiki: Faceting](https://github.com/OpenRefine/OpenRefine/wiki/Faceting)
>
> As well as 'Text facets' OpenRefine also supports a range of other types of facet. These include:
>
> * Numeric facets
> * Timeline facets (for dates)
> * Custom facets
> * Scatterplot facets
>
> **Numeric and Scatterplot facets** display graphs instead of lists of values. The numeric facet graph includes 'drag and drop' controls you can use to set a start and end range to filter the data displayed. These facets are explored further in [Examining Numbers in OpenRefine](http://www.datacarpentry.org/OpenRefine-ecology-lesson/03-numbers/)
>
> **Custom facets** are a range of different types of facets. Some of the default custom facets are:
>
> * Word facet - this breaks down text into words and counts the number of records each word appears in
> * Duplicates facet - this results in a binary facet of 'true' or 'false'. Rows appear in the 'true' facet if the value in the selected column is an exact match for a value in the same column in another row
> * Text length facet - creates a numeric facet based on the length (number of characters) of the text in each row for the selected column. This can be useful for spotting incorrect or unusual data in a field where specific lengths are expected (e.g. if the values are expected to be years, any row with a text length more than 4 for that column is likely to be incorrect)
> * Facet by blank - a binary facet of 'true' or 'false'. Rows appear in the 'true' facet if they have no data present in that column. This is useful when looking for rows missing key data.
{: .callout}

## Using undo and redo

It's common while exploring and cleaning a dataset to discover after you've made a change that you really should have done something else first. OpenRefine provides `Undo` and `Redo` operations to make this easy.

> ## Exercise 1.2
>
> 1. Click where it says `Undo / Redo` on the left side of the screen. All the changes you have made so far are listed here.
> 2. Click on the step that you want to go back to, in this case go back one step to before you had done the text to date transformation.
> 3. Visually confirm that the date column now only contains the date and no timestamp i.e. 2018-01-06
> 3. Notice that you can still click on the later steps to `Redo` the actions.
{: .challenge}


## Using clustering to detect possible typing errors

In OpenRefine, clustering means "finding groups of different values that might be alternative representations of the same thing". For example, the two strings `New York` and `new york` are very likely to refer to the same concept and just have capitalization differences. Likewise, `Gödel` and `Godel` probably refer to the same person. Clustering is a very powerful tool for cleaning datasets which contain misspelled or mistyped entries. OpenRefine has several clustering algorithms built in. Experiment with them, and learn more about these algorithms and how they work.

1. In the `sex` Text Facet we created in the step above, click the `Cluster` button.
2. In the resulting pop-up window, you can change the `Method` and the `Keying Function`. Try different combinations to
 see what different mergers of values are suggested.
3. Select the `key collision` method and `metaphone3` keying function. It should identify three clusters.
4. Tick the `Merge?` box beside each cluster, then click `Merge Selected and Re-cluster` to apply the corrections to the dataset.
4. Try selecting different `Methods` and `Keying Functions` again, to see what new merges are suggested.
5. You should find that using the default settings, no more clusters are found. (Note that the `key collision` method with `ngram-fingerprint` keying function will suggest to merge `F` and `M`, which is not desired.)
6. To merge the remaning values we would like to merge, we will hover over them in the sex text facet, select edit, and manually change the names. Change `M` to `male` and `F` to `female`. You should now have three clusters: `N/A`, `male`, and `female`.

Important: If you `Merge` using a different method or keying function, or more times than described in the instructions above,
your solutions for later exercises might not be the same as shown in those exercise solutions.

The technical details of how the different clustering algorithms work can be found at the link below.

[More on clustering](https://github.com/OpenRefine/OpenRefine/wiki/Clustering-In-Depth)

## Split


If data in a column needs to be split into multiple columns, and the parts are separated by a common separator (say a comma, or a space), you can use that separator to divide up the pieces into their own columns.


1. Let us suppose we want to split the `date` column into separate columns for year, month and day.
2. Click the down arrow at the top of the `date` column. Choose `Edit Column` > `Split into several columns...`
3. In the pop-up, in the `Separator` box, replace the comma with a hyphen (-).
4. Uncheck the box that says `Remove this column`.
5. Click `OK`. You'll get some new columns called `date 1`, `date 2`, and so on.
6. Note that the character on which the split is performed could be anything.  The default is a comma, and you changed
that to a hyphen in this case, but you could make it any letter, number or special character.  The only requirements
are that A) it appears in every row of the column, and B) it appears consistently in the place where you want the column
to be split.


> ## Exercise 1.3
>
>1. Try to change the name of the column "date 1" to "date". Are you able to do this?
Or do you encounter a problem?
> Change the name of the first new column to "year" instead, the second to "month" and the third to "day".
>
> > ## Solution
> >
> > On the `date 1` column, click the down arrow and then `Edit column` > `Rename this column`. Type "date into
> > the box that appears. A pop-up will appear that says `Another column already named date`. If you capitalize the D, it will work but in this case we choose "year" as the name instead. (Note: If the pop-up did not appear it means you forgot to uncheck the `Remove this column` box in step 4 above.)
You should now have the original column called "date", and 3 the new columns "year", "month", "day".  
> >
> {: .solution}
{: .challenge}


## Trim Leading and Trailing Whitespace

Words with spaces at the beginning or end are particularly hard for we humans to tell from strings without, but the blank characters will make a difference to the computer. We usually want to remove these. As of version 3.4 of OpenRefine, the option to trim leading and trailing whitespaces is present at the moment of importing the data (see image at the top of this page).

If you unchecked that box when importing data, or if leading or trailing whitespaces were introduced while splitting columns, or other operations, OpenRefine also provides a tool to remove blank characters from the beginning and end of any entries that have them.

1. Edit the `sex` on the first row to introduce a space at the end, set to `female `.
2. Create a new text facet for the `sex` column. You should now see two different entries for `female`, one of those has a trailing whitespace.
3. To remove the whitespace, choose `Edit cells` > `Common transforms` > `Trim leading and trailing whitespace`.
4. You should now see only three choices in your text facet again.

{% include links.md %}
