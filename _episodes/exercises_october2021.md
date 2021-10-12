---
layout: page
title: "Exercises for October 2021"

---

### [Working with OpenRefine](../02-working-with-openrefine/)

> ## Using Facets (Exercise 1.1)
> 1. Using faceting, find out how many values the dataset contain in the column `location`.
>
> 2. What is the column format (text, date, or numbers)?
>
> 3. In the column `date`, use `Text Facet` to identify how many unique entries there are.
>
> 4. Use faceting to produce a timeline display for the column `date`. You will need to use `Edit cells` > `Common transforms` > `To date` to convert this column to dates.
>
> 5. During which day were most of the samples registered, and what happened to the data in cells not conforming to a proper date format?
>
> > ## Solution
> >
> > 1. For the column `location` do `Facet` > `Text facet`. A box will appear in the left panel showing 
> > that there are 7 unique entries in this column.
> > 2. The format is text, which is the default, otherwise `Text facet` would not have displayed any entries. If you want to check the format, click `edit` in a cell, the data type will show the current format. 
> > 3. For the column `date` do `Facet` > `Text facet`. A box will appear in the left panel showing that there are 17 unique entries in
> > this column.
> > 4. By default, the column `date` is formatted as Text. You can change the format by doing `Edit cells` > `Common transforms` >
> > `To date`.  Notice that the values in the columns possible to transform to a correct date format turn green, and also adds a timestamp after each date. Doing `Facet` > `Timeline facet` creates a box in the left panel that shows a histogram of the number of entries for each date. If we do not want the timestamp in the date format, we can edit it out, but more on that later.
> > 5. Most of the samples (43) were registered for the date `2020-03-31`. The  four dates that couldn't be transformed (`7 April`, `31 March`, `32 March` and `33 March`) are noted as Non-Time in the timeline histogram.
> {: .solution}
{: .challenge}

> ## Using undo/redo (exercise 1.2)
>
> 1. Click where it says `Undo / Redo` on the left side of the screen. All the changes you have made so far are listed here.
> 2. Click on the step that you want to go back to, in this case go back one step to before you had done the text to date transformation.
> 3. Visually confirm that the date column now only contains the original dates without timestamps.
> 3. Notice that you can still click on the later steps to `Redo` the actions. Redo the date transformation by clicking on this step.
{: .challenge}

> ## Splitting Columns (exercise 1.3)
>
> Try to change the name of the column `location 1` to `location 2`. Are you able to do this, or do you encounter a problem?
>
> Change the name of the first new column to `geographic location (country)`, the second to `geographic location (region and locality)` and the third to `geographic location (city)`. Then change all occurances of the city name `Torino` to `Turin`.
>
> > ## Solution
> >
> > 1. On the `location 1` column, click the down arrow and then `Edit column` > `Rename this column`.
> > 2. Type `geographic location (country)` into the box that appears. If you type anything that is already used as a column name elsewhere, a pop-up will appear that says `Another column already named [name]`. Note that column names are case sensitive. If you capitalize the initial (or any) letter, it will be recognized as a unique name.
> > You should now have three new columns called `geographic location (country)`, `geographic location (region and locality)`, and `geographic location (city)` 
> > 3. Hover the mouse over a cell in `geographic location (city)` named `Torino`. Notice the `edit` function becoming available. Click on `edit`, type in `Turin` and select `Apply to All Identical Cells`. All occurrences of `Torino` are now replaced with `Turin`. Also notice there might be leading whitespaces in most of the names for `geographic location (city)`. We will deal with those in the next section. 
> >
> {: .solution}
{: .challenge}

> ## Date issues (exercise 1.4)
>
> Did you notice that some of the dates in the `date` column looks eerily related? In the list we have both `2020-04-01` and > `2020-01-04`, `2020-04-07` and `2020-07-04`, and `2020-04-08` and `2020-08-04`. These might be correct, or they may be an artefact of when data was typed in, depending on which date format was used. 
> 
> Discuss when this could happen in a dataset, and what practises we can use to avoid such problems, particulary in larger research groups where members from different parts of the world collaborate. 
>
> > ## Solution
> > Before starting a project, make sure all collaborators have agreed to conform to a common standard. In particular, atypical date formats in spreadsheets can cause severe issues in downstream analyses. 
> >
> {: .solution}
{: .challenge}

### [Filtering and Sorting](../03-filter-sort/)

> ## Filtering (exercise 2.1)
>
> 1. How can you filter the data to instead only include persons with state `dead`?
> 2. How would you further restrict this to only include females or males?  
>
> > ## Solution
> > 1. In the `disease outcome` filter, type `dead` instead of recovered.   
> > 2. To restrict to only one of the sexes, in the `sex` column, run another `Text Filter`and type `female`. Notice that if you type `male` we also capture all expressions containing `male`, such as `female`. To filter only `male`, run the filter for `female` and then use the `invert` function.
> >
> {: .solution}
> Remove the filters before moving on so that you again have the full dataset of 91 records.
{: .challenge}

> ## Excluding entries (exercise 2.2)
>
> Use `include / exclude` in a `Text Facet` to make the same combination of `disease outcome` and `sex` as in the previous exercise.
>
> > ## Solution
> >
> > 1. In the facet (left margin), hover on `recovered`. Notice that there are entries to the right for `edit` and `include`.
> > 2. Click `include`. This will explicitly include those recovered, and exclude others that are not explicitly included. Notice that the
> option now changes to `exclude`.
> > 3. Another way to include entries is to click the name directly.
> > 4. Do the same thing with `sex` to limit your selection to a combination of the two states.
> > 4. Click `include` and `exclude` in both facets and notice how the selection in the data changes.
> {: .solution}
> Remove the selections before moving on, so that you again have the full dataset of 91 records, either by closing all facets or press `Reset All` button in top of the left margin.
{: .challenge}

> ## Sorting (exercise 2.3)
>
> Sort all samples by host age. How can you ensure that ages are in numerical order?
> > ## Solution
> > 1. Press the down arrow in the `age` column, select `Sort...`
> > 2. In the pop-up that appears, tick `numbers` and select `smallest first`.
> >
> {: .solution}
{: .challenge}

### [Examining Numbers in OpenRefine](../04-numbers/)
> ## Transform to number (exercise 3.1)
>
> Try to transform the column `ENA-CHECKLIST` from text to numbers. Can all columns be transformed to numbers?
>
> > ## Solution
> >
> > - Only observations that include only numerals (0-9) can be transformed to numbers. If you apply a number transformation to
> > a column where the observations don't meet this criteria a yellow square will appear at the top starting with `Text transform on 0 cells in column [...]`. If you click the `Undo / Redo` tab, you will see a step that starts with the same text, meaning
> > that the data in that column was not transformed.
Note that for some columns, some observations, but not all, can meet the criteria for being transformed into a number. This will result in a mix of transformed and non-transformed cells in the column.   
> Having several formats in the same column is not recommended.
> {: .solution}
{: .challenge}


> ## Numeric Facet (exercise 3.2)
> 1. For the column `age` you just transformed to numbers, edit one or two cells, replacing the numbers with text (such as `abc`) or blank (no number nor text). You can hover over the cell and click the blue `edit` that appears, and change the `Data type` to `text` at the top in the scroll-down window.
> 2. Use the column pulldown menu to apply a `Numeric facet` to the column you edited. The facet will appear in the left panel.
> 3. Notice that there are several checkboxes in this facet: `Numeric`, `Non-numeric`, `Blank`, and `Error`. Below these are counts of the number of cells in each category. You should see checks for `Non-numeric` and `Blank` if you changed some values.
> 4. Experiment with checking or unchecking these boxes to select subsets of your data.
{: .challenge}

> ## Missing values (exercise 3.3)
>
> Find, identify and transform missing data in all columns of the dataset. What formats for missing data are approriate in this dataset?
>
> > ## Solution
> >
> > - The only missing values in the dataset are found in the columns `health state`, `symptoms` and `disease outcome`. Since the values are not numerical a good choice could be to replace them with the option `NA` (Not available). Do this by using `edit` in a cell with missing value, type `NA` and then select `Apply To All Identical Cells`.
> {: .solution}
{: .challenge}


### [Transforming and Selecting a Subset of the Data](../07-subsetting-the-data)

> ## Create a column (exercise 6.1)
>
> Add a new column called `collecting entity`, and fill all cells with the input `Amedeo di Savoia`. Can you generate the column to the right of the column `collector name`?
>
> > ## Solution
> >
> > 1. On the `collector name` column, select `Edit column` > `Add column based on this column...`.
> > 2. Type `collecting entity` in `New column name`, provide the input `value` as `null` just as before.
> > 3. `edit` the contents of the cells to `Amedeo di Savoia` and select `Apply to All Identical Cells`.
> {: .solution}
{: .challenge}

> ## Join columns (exercise 6.2)
>
> Create a new column called `isolate`, and populate the cells with information for **[organism/host/location/isolate/date]** as defined by the ENA checklist. Notice that our column names are not (yet) aligned with the ontology of the checklist.
> > ## Solution
> >
> > 1. In the `virus_identifier` column, select `Edit column` > `Join columns...`.
> > 2. In the list, tick boxes for the columns:
- `organism` -> `virus identifier`
- `host` -> `host common name`
- `location` -> `geographic location (country)`
- `isolate` -> `sample_alias`
- `date` -> `collection date`.
> > 3. Add a slash `/` as `Separator between the content of each column:`
> > 4. Tick `Write result in new column named...` and type `isolate`. This will create a new column named `isolate` populated with the above information. 
> > 5. Make sure the box for `Delete joined columns` is not ticked. Once you are confident your selection is correct, make sure to drag-and-drop the columns to appear in the desired order.
> > 6. Select `OK`. All cells should now be populated with isolate information. 
> {: .solution}
{: .challenge}