---
title: "Filtering and Sorting with OpenRefine"
teaching: 10
exercises: 10
questions:
- "How can we select only a subset of our data to work with?"
- "How can we sort our data?"
objectives:
- "Filter to a subset of rows by text filter or include/exclude."
- "Sort table by a column."
- "Sort by multiple columns."
keypoints:
- "OpenRefine provides a way to sort and filter data without affecting the raw data."
---

# Lesson

## Filtering

There are many entries in our data table, we can filter it to work on a subset of the data:

1. Click the down arrow next to `disease outcome` and select `Text filter`. A `disease outcome` filter will appear on the left margin.
2. Type in `recovered`. There are 33 matching rows of the original 91 rows (and these rows are selected for the subsequent steps).
3. At the top, change the view to `Show` 50 rows. This way you will see all of the matching rows.

> ## Exercise 2.1
>
> 1. How can you filter the data to instead only include persons with state `dead`?
> 2. How would you further restrict this to only include females or males?  
>
> > ## Solution
> > 1. In the `disease outcome` filter, type `dead` instead of recovered.   
> > 2. To restrict to only one of the sexes, in the `sex` column, run another `Text Filter`and type `female`. Notice that if you type `male` we also capture all expressions containing `male`, such as `female`. To filter only `male`, run the filter for `female` and then use the `invert` function.
> >
> {: .solution}
{: .challenge}

Remove the filters before moving on so that you again have the full dataset of 91 records.

### Excluding entries

In addition to the simple text filtering we used above, another way to narrow our filter is to `include` and/or `exclude` entries in a facet. If you still have your facet for `disease outcome`, you can use it. If not, use drop-down menu > `Facet` > `Text facet` to create a new facet. You will see the `include` or `exclude` options if you hover over the name in the facet window.


Faceting and filtering look very similar. A good distinction is that faceting gives you an overview description of all of the data that
is currently selected, while filtering allows you to select a subset of your data for analysis.

> ## Exercise 2.2
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
> >  
> >
> {: .solution}
{: .challenge}

Remove the selections before moving on, so that you again have the full dataset of 91 records, either by closing all facets or press `Reset All` button in top of the left margin.

## Sort

You can sort the data in a column by using the drop-down menu available in that column.
There you can sort by `text`, `numbers`, `dates` or `booleans` (`TRUE` or `FALSE` values). You can also specify what order to put `Blanks` and `Errors` in the sorted results.

If this is your first time sorting this table, then the drop-down menu for the selected column shows `Sort...`. Select what you would like to sort by (such as `numbers`). Additional options will then appear for you to fine-tune your sorting.


> ## Exercise 2.3
>
> Sort all samples by host age. How can you ensure that ages are in numerical order?
> > ## Solution
> > 1. Press the down arrow in the `age` column, select `Sort...`
> > 2. In the pop-up that appears, tick `numbers` and select `smallest first`.
> >
> {: .solution}
{: .challenge}

If you try to re-sort a column that you have already used, the drop-down menu changes slightly, to > `Sort` without the `...`, to remind you that you have already sorted this column. It will give you additional options:

* > `Sort` > `Sort...` - This option enables you to modify your original sort.
* > `Sort` > `Reverse` - This option allows you to reverse the order of the sort.
* > `Sort` > `Remove sort` - This option allows you to undo your sort.

### Sorting by multiple columns

You can sort by multiple columns by performing sort on additional columns. The sort will depend on the order in which you select columns to sort. To restart the sorting process with a particular column, check the `sort by this column alone` box in the `Sort` pop-up menu.

If you go back to one of the already sorted columns and select > `Sort` > `Remove sort`, that column is removed from your multiple sort. If it is the only column sorted, then data reverts to its original order.
