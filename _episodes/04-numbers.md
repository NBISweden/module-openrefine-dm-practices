---
title: "Examining Numbers in OpenRefine"
teaching: 10
exercises: 10
questions:
- "How can we convert a column from one data type to another?"
- "How can we visualize relationships among columns?"
objectives:
- "Transform a text column into a number column."
- "Identify and modify non-numeric values in a column using facets."
keypoints:
- "OpenRefine also provides ways to get overviews of numerical data."
---

# Lesson

## Numbers

When a table is imported into OpenRefine, all columns are treated as having text values. We saw earlier how we can sort column values as numbers, but this does not change the cells in a column from text to numbers. Rather, this interprets the values as numbers for the purposes of sorting but keeps the underlying data type as is. We can, however, transform columns to other data types (e.g. number or date) using the `Edit cells` > `Common transforms` feature, like we did previously with the `date` column. Here we will experiment changing columns to numbers and see what additional capabilities that grants us.

Be sure to remove any `Text filter` facets you have enabled from the left panel so that we can examine our whole dataset. You can remove an existing facet by clicking the `x` in the upper left of that facet window.

To transform cells in the `age` column to numbers, click the down arrow for that column, then `Edit cells` > `Common transforms…` > `To number`. You will notice the `age` values change from left-justified to right-justified, and from black to green in color.

> ## Exercise 3.1
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
<BR> 
## Numeric facet
Sometimes there are non-number values or blanks in a column which may represent errors in data entry and we want to find them.
We can do that with a `Numeric facet`.

> ## Exercise 3.2
> 1. For the column `age` you just transformed to numbers, edit one or two cells, replacing the numbers with text (such as `abc`) or blank (no number nor text). You can hover over the cell and click the blue `edit` that appears, and change the `Data type` to `text` at the top in the scroll-down window.
> 2. Use the column pulldown menu to apply a `Numeric facet` to the column you edited. The facet will appear in the left panel.
> 3. Notice that there are several checkboxes in this facet: `Numeric`, `Non-numeric`, `Blank`, and `Error`. Below these are counts of the number of cells in each category. You should see checks for `Non-numeric` and `Blank` if you changed some values.
> 4. Experiment with checking or unchecking these boxes to select subsets of your data.
{: .challenge}

When done examining the numeric data, remove this facet by clicking the `x` in the upper left corner of its panel. Note that this does not undo the edits you made to the cells in this column. Use the `Undo / Redo` function to reverse these changes.
<BR>
<BR>
## Missing values
More than often we lack certain data for a variable. It may be an unknown origin of a sample, lacking information on age and sex, missing part of a date (only YYMM), or even encountering a value going to infinity. Regardless of origin we need to consider how we code them to avoid downstream analyses issues.

A rule of thumb is to never replace missing values with a zero (0). Even if a zero may be a representation of something not present, it is per definition not a missing value, but a zero value. Using zero for missing value may cause severe issues and should be avoided.

Different software may be equipped with different interpretors for missing values. For example, valid input in R include `NULL`, `NA`, `NaN`, `Inf` and `-Inf`, while MatLab uses more context dependent options, e.g. `missing`, or `NaN`. The main point is that you need to consider how to code missing values in your data depending on what kind of software you plan on using. Also, for projects where more than one person is involved in managing the data, make sure you agree on a single format and stick to it.

> ## Exercise 3.3
>
> Find, identify and transform missing data in all columns of the dataset. What formats for missing data are approriate in this dataset?
>
> > ## Solution
> >
> > - The only missing values in the dataset are found in the columns `health state`, `symptoms` and `disease outcome`. Since the values are not numerical a good choice could be to replace them with the option `NA` (Not available). Do this by using `edit` in a cell with missing value, type `NA` and then select `Apply To All Identical Cells`.
> {: .solution}
{: .challenge}



{% include links.md %}
