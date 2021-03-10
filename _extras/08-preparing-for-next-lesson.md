---
title: "Preparing for the next lesson"
teaching: 5
exercises: 10
questions:
- "How do I create a metadata file compatible with the repository of choice?"
objectives:
- "Export a file from OpenRefine with a subset of columns needed for submitting the data to the repository ENA."
- ""
keypoints:
- ""
---

# Lesson

## Transforming and Selecting a Subset of the Data
Sometimes you would like to export a file that only contains a subset of the data in your project that conforms to a specific standard.  

In the next module of this course we will submit sequencing data to the repository ENA and we need to prepare sample metadata to conform to the metadata standards of the repository.

We need to consider the following questions:

- Which of the existing columns are relevant for the submission?
- Are they named correctly?
- Are there additional columns that need to be added?

You already did some of this work when creating the data dictionary in the metadata lesson where you identified ENA variables based on the default checklist.
We will come back to these in a while but first we will look at the mandatory metadata for all samples submitted to ENA regardless of the checklist chosen.  

**Basic details:**

sample_alias  - _The unique name is a submitter provided unique identifier._

sample_title - _The sample title is a short, preferably a single sentence, description of the sample._

**Organism details:**

tax_id - _The NCBI taxonomy id_

scientific_name - _based on tax_id_


> ## Exercise
>Can any of the existing columns be used for `sample_alias`, `sample_title`, `tax_id` and `scientific_name`?
>
> > ## Solution
> > 1. `experiment reference` could be used as `sample_alias` since it is a unique ID
> > 2. No existing column could be used as `sample_title` but could be created by combining the information in `sample` and `genotype` and     
> > 3. A column `tax_id` already exists
> > 4. A column `scientific_name` needs to be added
> {: .solution}
{: .challenge}

##Renaming and adding columns
To rename the column `experiment reference`
1. Click the down arrow next to `experiment reference` > `Edit column` > `Rename this column`. A pop-up window will appear on top.
2. Type in `sample_alias` and press return.

##Join columns
First we want to add some more information to the `genotype` column.
1. Hover the first cell containing `wild type genotype` and click `edit`. A pop-window will appear.
2. Type `Lung tissue from adult wildtype mouse.` and then click `Apply to all identical cells`. Three cells should have been edited.
3. Repeat the steps for a cell containig the value `Kdr Y949F/Y949F` but type `Lung tissue from adult Kdr(Y949F/Y949F) mouse.` in the pop-up window.

To join the sample column with the genotype column
1. Click the down arrow next to `sample` > `Edit column` > `Join columns...`. A pop-up window will appear.
2. On the left side, choose which columns to join. Verify that `sample` is already ticked and tick `genotype` as well.
To the right, there are several options for the join.
3. In the separator field, enter a blank space.
4. Click ` Write result in new column named… ` and enter `sample_title`
5. Tick the option `Delete joined columns.`


## Exporting Cleaned Data

You can also export just your cleaned data, rather than the entire project.

1. Click `Export` in the top right and select the file type you want to export the data in. In this case we will choose `Comma-separated values` (`csv`).
2. That file will be exported to your default `Download` directory. That file can then be opened in a spreadsheet program or imported
into programs like RStudio which we'll be discussing later in our workshop.

Remember from our lesson on data organisation that using widely-supported, non-proprietary file formats like `tsv` or `csv` improves the ability of yourself and others to use your data.

> ## Exercise
>
>
{: .challenge}

{% include links.md %}
