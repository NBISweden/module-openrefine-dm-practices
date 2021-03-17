---
layout: page
title: "Exercises for April 2021"

---

## Exercises

### [Working with OpenRefine](../02-working-with-openrefine/exercise 1.1)


> ## Using Facets (Exercise 1.1)
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
> > - Five dates had more than one animal registered.
> > - The `date` column was formatted as Text.
> > - Most of the animals were registered in January of 2019 (seen by narrowing the window around the tallest bar in the timeline facet).
> {: .solution}
{: .challenge}
>
>
>
> ## Splitting Columns (exercise 1.3)
>
> Try to change the name of the column `date 1` to `date`. Are you able to do this? Or do you encounter a problem?
>
> Change the name of the first new column to `year` instead, the second to `month` and the third to `day`.
>
> > ## Solution
> >
> > 1. On the `date 1` column, click the down arrow and then `Edit column` > `Rename this column`.
> > 2. Type `date` into the box that appears. A pop-up will appear that says `Another column already named date`. If you capitalize the D, it will work but in this case we choose `year` as the name instead.
(Note: If the pop-up did not appear it means you forgot to uncheck the `Remove this column` box in step 4 above.)
> >
> > You should now have the original column called `date`, and the 3 new columns `year`, `month`, `day`.  
> >
> {: .solution}
{: .challenge}

### [Filtering and Sorting](../03-filter-sort/)

> ## Filtering (exercise 2.1)
>
> 1. What mouse lines are selected by this procedure?  
> 2. How would you restrict this to only one of the mouse lines?  
>
> > ## Solution
> > 1. Do `Facet` > `Text facet` on the `mouse line` column after filtering. This will show that
> > two names match your filter criteria. They are `Alk3` and `alk6`.   
> > 2. To restrict to only one of these two mouse lines, you could include more letters in your filter.
> >
> {: .solution}
{: .challenge}


> ## Excluding entries (exercise 2.2)
>
> Use `include / exclude` to select only entries from one of these mouse lines.
>
> > ## Solution
> >
> > 1. In the facet (left margin), hover on one of the names, such as `Alk3`. Notice that there are entries to the right for `edit` and `include`.
> > 2. Click `include`. This will explicitly include this mouse line, and exclude others that are not explicitly included. Notice that the
> option now changes to `exclude`.
> > 3. Another way to include entries is to click the name directly.
> > 4. Click `include` and `exclude` to notice how the two entries appear and disappear
> >  from the table.
> >
> {: .solution}
{: .challenge}
>
>
> ## Sorting (exercise 2.4)
>
> Sort the data by `date`. What is the animal ID recorded on the most recent date in this dataset?
>
> > ## Solution
> > In the `date` column, select `Sort...` > `text` and select `z-a`.
> >
> > The animal ID for 2020-10-08 is 957895.
> >
> {: .solution}
{: .challenge}


> ## Sorting by multiple columns - optional (exercise 2.5)
>
> You might like to look for trends in your data by month of collection across years.     
> 1. How do you sort your data by month?   
> 2. How would you do this differently if you were instead trying to see all of your entries in chronological order?  
>
> > ## Solution
> >
> > 1. For the `month` column, click on `Sort...` and then `numbers`. This will group all entries made in, for example, January,
> > together, regardless of the year that entry was collected.  
> > 2. For the `year` column, click on `Sort` > `Sort...` > `numbers` and select `sort by this column alone`. This will undo the
> > sorting by month step. Once you've sorted by `year` you can then apply another sorting step to sort by month within year. To do this
> > for the `month` column, click on `Sort` > `numbers` but do not select `sort by this column alone`. To ensure that all entries are shown
> > chronologically, you will need to add a third sorting step by day within month.
> >
> {: .solution}  
{: .challenge}


> ## Sort - optional (exercise 2.6)
>
> Sort by `year`, `month` and `day` in some order. Be creative: try sorting as `numbers` or `text`, and in reverse order (`largest to smallest` or `z to a`).
>
> Use > `Sort` > `Remove sort` to remove the sort on the second of three columns. Notice how that changes the order.
{: .challenge}

### [Examining Numbers in OpenRefine](../04-numbers/)
> ## Transform to number (exercise 3.1)
>
> Try to transform the columns, `date` and `age`, from text to numbers. Can all columns be transformed to numbers?
>
> > ## Solution
> >
> > Only observations that include only numerals (0-9) can be transformed to numbers. If you apply a number transformation to
> > a column where the observations don't meet this criteria a yellow square will appear at the top starting with `Text transform on 0 cells`. If you click the `Undo / Redo` tab, you will see a step that starts with the same text, meaning
> > that the data in that column was not transformed. This is the case for the `date` column.
For the `age` column, some observations but not all, meet the criteria for being transformed into a number and will result in 43 cells being transformed.   
> Having several formats in the same column is not recommended.
> {: .solution}
{: .challenge}


> ## Numeric Facet (exercise 3.2)
> 1. For the column `animal ID` you just transformed to numbers, edit one or two cells, replacing the numbers with text (such as `abc`) or blank (no number or text). You can hover over the cell and click the blue `edit` that appears, change the `Data type` to `text` at the top of the pop-up window.
> 2. Use the column pulldown menu to apply a numeric facet to the column you edited. The facet will appear in the left panel.
> 3. Notice that there are several checkboxes in this facet: `Numeric`, `Non-numeric`, `Blank`, and `Error`. Below these are counts of the number of cells in each category. You should see checks for `Non-numeric` and `Blank` if you changed some values.
> 4. Experiment with checking or unchecking these boxes to select subsets of your data.
{: .challenge}


### Preparing for the next Lesson on repository submission
> ## Create a new project in OpenRefine (exercise 3.1)
>
> 1. Create a new project in OpenRefine named 'ENA sample metadata` by loading the same data as before `samples_openrefine_lesson.csv`
> 2. Open the file `ENA_sample_metadata_script.txt` found in the project folder. Copy the JSON script and apply it to the project.
> 3. Export the cleaned data as a tab separated file (.tsv)
> 4. Open the file in a text editor and add the following two lines at the beginning of the file:
> #checklist_accession  ERC000011  
> #unique_name_prefix
> Make sure that you have a tab between `#checklist_accession` and `ERC000011`
> 5. Save the file in your course folder.
>
> > ## Solution
> > 1. Click `Create Project` and select `Get data from` `This Computer`.
> > 2. Click `Choose Files` and select the file `samples_openrefine_lesson.csv` that you downloaded in the [setup step]({{site.baseurl}}/setup.html). Click `Open` or double-click on the filename.
> > 3. Click `Next>>` under the browse button to upload the data into OpenRefine.
> > 4. In the upper right, type 'ENA sample metadata` as the project name and click `Create Project>>`
> > 5. On the left, click the `Undo/Redo` tab > `Apply...` A pop-up will appear. Paste the content of the `ENA_sample_metadata_script.txt` file and click `Perform operations`
> > 6. On top right, click `Export` > `Tab-separated value`. A .tsv file will be exported to your default downloads folder.
> >
> {: .solution}
{: .challenge}
