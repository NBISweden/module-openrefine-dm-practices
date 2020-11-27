---
title: "Other Resources in OpenRefine"
teaching: 5
exercises: 5
questions:
- "What other resources are available for working with OpenRefine?"
objectives:
- "Understand that there are many online resources available for more information on OpenRefine."
- "Identify other resources about OpenRefine."
keypoints:
- "Other examples and resources online are good for learning more about OpenRefine"
---

# Lesson

## Using online resources to get help with OpenRefine

OpenRefine is more than a simple data cleaning tool. People are using it for all sorts of activities. Here are some other resources that might prove useful.

## Transforming data

The data in the `items_owned` column is a set of items in a list. The list is in square brackets and each item is in single quotes. Before we split the list into individual items in the next section, we first want to remove the brackets and the quotes.

1. Click the down arrow at the top of the `items_owned` column. Choose `Edit Cells` > `Transform...`
2. This will open up a window into which you can type a GREL expression. GREL stands for General Refine Expression Language.
![OR_Transform](../fig/OR_02_Transform.png)

3. First we will remove all of the left square brackets (`[`). In the Expression box type `value.replace("[", "")` and click `OK`.

4. What the expression means is this: Take the `value` in each cell in the selected column and replace all of the "[" with "" (i.e. nothing - delete).

5. Click `OK`. You should see in the `items_owned` column that there are no longer any left square brackets.

> ## Exercise
>
> Use this same strategy to remove the single quote marks (`'`), the
> right square brackets (`]`), and spaces from the `items_owned` column.
>
> > ## Solution
> > 1. `value.replace("'", "")`
> > 2. `value.replace("]", "")`
> > 3. `value.replace(" ", "")`
> > You should now have a list of items separated by semi-colons (`;`).
> {: .solution}
{: .challenge}

Now that we have cleaned out extraneous characters from our `items_owned` column, we can use a text facet to see which items
were commonly owned or rarely owned by the interview respondents.

1. Click the down arrow at the top of the `items_owned` column. Choose `Facet` > `Custom text facet...`
2. In the `Expression` box, type `value.split(";")`.
3. Click `OK`.

You should now see a new text facet box in the left-hand pane.

> ## Exercise
> Which two items are the most commonly owned? Which are the two
> least commonly owned?
>
> > ## Solution
> > Select `Sort by:` `count`. The most commonly owned items are
> > mobile phone and radio, the least commonly owned are cars and computers.
> {: .solution}
{: .challenge}

> ## Exercise
> Perform the same clean up steps and customized text faceting for
> the `months_lack_food` column. Which month(s) were farmers
> more likely to lack food?
>
> > ## Solution
> > All four cleaning steps can be performed by combining `.replace`
> > statements. The command is:
> > `value.replace("[", "").replace("]", "").replace(" ", "").replace("'", "")`
> > This can also be done in four separate steps if preferred.
> > November was the most common month for respondents to lack food.
> {: .solution}
{: .challenge}

> ## Exercise
> Perform the same clean up steps for the `months_no_water`, `liv_owned`, `res_change`, and `no_food_mitigation` columns.
> Hint: To reuse a GREL command, click the `History` tab and then
> click `Reuse` next to the command you would like to apply to that
> column.
{: .challenge}

OpenRefine has its own web site with documentation and a book:

* [OpenRefine web site](http://openrefine.org/)
* [OpenRefine Documentation for Users](https://github.com/OpenRefine/OpenRefine/wiki/Documentation-For-Users)
* [OpenRefine documentation Wiki site](https://github.com/OpenRefine/OpenRefine/wiki/Documentation-For-Users)
* [Using OpenRefine](http://www.worldcat.org/title/using-openrefine-the-essential-openrefine-guide-that-takes-you-from-data-analysis-and-error-fixing-to-linking-your-dataset-to-the-web/oclc/889271264) book by Ruben Verborgh, Max De Wilde and Aniket Sawant
* [OpenRefine history from Wikipedia](https://en.wikipedia.org/wiki/OpenRefine)

In addition, see these other useful resources:

* [Grateful Data](https://github.com/scottythered/gratefuldata/wiki) is a fun sight with many resources devoted to OpenRefine, including a nice tutorial.
* [Margaret Heller](http://www.gloriousgeneralist.com/) shows how she uses OpenRefine for [Measuring and Counting Impact in Repositories](http://www.gloriousgeneralist.com/2014/12/notes-on-measuring-and-calculating-impact-in-institutional-repositories/).

There are more advanced uses of OpenRefine, such as bringing in column or cell data using web locators (URLs or APIs). The links above can give you a start on your journey.

> ## Exercise
>
> Visit one of these sites and share what you find with another person.
{: .challenge}

{% include links.md %}
