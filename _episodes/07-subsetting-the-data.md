---
title: "Transforming and Selecting a Subset of the Data"
teaching: 10
exercises: 15
questions:
- "How do I create a metadata file compatible with the repository of choice?"
objectives:
- "Export a file from OpenRefine with a subset of columns needed for submitting the data to the repository ENA."
keypoints:
- "OpenRefine can be used to structure your data into a file suitable for a repository submission."
---

# Lesson

Sometimes you would like to export a file that only contains a subset of the data in your project that conforms to a specific standard.  

In the next lesson of the _Introduction to Data Management Practices Workshop_ we will act as the researcher **Sam**
who wants to submit data to the repository [ENA](https://www.ebi.ac.uk/ena/browser/home) (European Nucleotide Archive).
To do so we need to prepare sample metadata to conform to the metadata standards
of the repository.

We need to consider the following questions:

- **Which of the existing columns are relevant for the submission?**
- **Are they named correctly?**
- **Are there additional columns that need to be added?**

<BR>
First, we will only keep samples registered by `Sam`

1. Create a filter for the column `researcher` by clicking the down arrow in the column header and select `Text filter`.
2. A researcher filter box will appear to the on the left side. Type `Sam` in the text field and press return. 29 matching rows will be displayed.
3. In the same box, press `invert` in the top right to select all the rows from researchers other than Sam. Note that the box header will turn orange to indicate inverted results.
4. Confirm that there are 71 matching rows.
5. Click the down arrow next to `All` in the left-most column header > `Edit rows` > `Remove matching rows`
6. Remove or reset the filter. Now, all remaining 29 rows should be Sam's.

## ENA sample metadata
ENA sample metadata can be divided in three groups.
- Mandatory metadata
- Checklist-based metadata
- User defined metadata

In a previous lesson in this workshop around [metadata](https://nbisweden.github.io/module-metadata-dm-practices/05-finding-ontologies/index.html) you already came across the ENA checklists. When creating a data dictionary you identified ENA variables based on the default checklist and ontologies to identify allowed values. We will come back to these in a while but first we will look at the mandatory fields.

### Mandatory fields
Some metadata are mandatory for all samples submitted to ENA regardless of the checklist chosen. We will try to map the existing columns to these variables.

**Basic details**  
sample_alias  - _The unique name is a submitter provided unique identifier._  
sample_title - _The sample title is a short, preferably a single sentence, description of the sample._

**Organism details**  
tax_id - _The NCBI taxonomy id_  
scientific_name - _based on tax_id_


> ## Exercise
>Can any of the existing columns be used as `sample_alias`, `sample_title`, `tax_id` and `scientific_name`?
>
> > ## Solution
> > 1. `experiment reference` could be used as `sample_alias` since it is a unique ID
> > 2. No existing column could be used as `sample_title` but could be created by combining the information in `sample` and `genotype`     
> > 3. A column `tax_id` already exists
> > 4. A column `scientific_name` needs to be added
> {: .solution}
{: .challenge}


### Renaming and creating new columns
To rename the column `experiment reference`
1. Click the down arrow next to `experiment reference` > `Edit column` > `Rename this column`. A pop-up window will appear on top.
2. Type in `sample_alias` and press return.
<BR>
#### Join columns
First we want to edit the information in the `genotype` column.
1. Hover the first cell containing `wild type genotype` and click `edit`. A pop-window will appear.
2. Type `Lung tissue from adult wildtype mouse.` and then click `Apply to all identical cells`. Three cells should have been edited.
3. Repeat the steps for a cell containig the value `Kdr Y949F/Y949F`  (note the space between Kdr and Y949...) but type `Lung tissue from adult Kdr(Y949F/Y949F) mouse.` in the pop-up window.

Now we will join the sample column with the genotype column
1. Click the down arrow next to `sample` > `Edit column` > `Join columns...`. A pop-up window will appear.
2. On the left side, choose which columns to join. Verify that `sample` is already ticked and tick `genotype` as well.
To the right, there are several options for the join.
3. In the separator field, enter a blank space.
4. Click ` Write result in new column named… ` and enter `sample_title`
5. Tick the option `Delete joined columns.` and click `OK`.
<BR>
#### Add a new column
To add a column `scientific_name`
1. Click the down arrow next to `tax_id` > `Edit column` > `Add column based on this column...`. A pop-up window will appear.
2. On top, type `scientific_name` in the `New column name` field
3. In the big text field where it now says `value` type `"Mus musculus"`. Make sure to include the quotation marks (`"`).
Note that the values of the new column can be previewed at the bottom.

### Checklist-based and user defined metadata
Now let's have a look at the data dictionary from the metadata lesson. Which variables did you identify an ENA variable name for based on the ENA checklist? Rename the columns where necessary.

> > ## Solution
> > #### Data dictionary:
> >
> > | Current variable name | ENA Variable name | Measurement unit | Allowed values | Definition | Description |
> > |-|-|-|-|-|-|
> > | animal ID |  |  |  |  |  |
> > | date |  |  | format: YYYY-MM-DD, >=proj_start_date & <=today | Date of experiment ??? |  |
> > | mouse line | sub_strain |  |  |  |  |
> > | strain | strain |  | NCIT ontology:<br> C56BL/6 Mouse (NCIT:C14424),<br> BALB/cJ Mouse (NCIT:C14657) | The mouse strain of the animal |  |
> > | age |  | days,weeks (?) |  | Age of animal |  |
> > | developmental stage | dev_stage |  | BTO ontology:<br> pup (BTO:0004377),<br> adult (BTO:0001043),<br> embryo (BTO:0000379) |  |  |
> > | sex | sex |  | male, female, unknown | Sex of the animal |  |
> > | organism part | tissue_type |  | MA ontology:<br> lung (MA:0000415),<br> brain (MA:0000168) |  |  |
> > | genotype |  |  |  |  |  |
> > | experiment type |  |  |  |  |  |
> > | experiment reference |  |  |  |  |  |
> > | researcher |  |  |  |  |  |
> >
> > 5 ENA variables have been identified `sub_strain`, `strain`, `dev_stage`, `sex` and `tissue_type`. 3 of the columns need to be renamed to match the ENA variable name.  
> >
> > Renaming columns:
> > 1. Click the down arrow next to `mouse line` > `Edit column` > `Rename this column`. A pop-up window will appear on top.
> > 2. Type in `sub_strain` and press return.  
> > 3. Repeat the steps to rename `developmental stage` to `dev_stage` and `organism part` to `tissue_type`
> {: .solution}
{: .challenge}


The data dictionary has a column for `allowed values` which contains ontology IDs for  `strain`, `dev_stage` and `tissue_type`. ENA provides an option to add custom fields. We will use this to add the ontology-IDs you identified in the metadata module. We need to create 3 new columns based on the ENA variables that you identified ontology-IDs for and add `_ID` to the end.  
**User fields:**
- strain_ID
- dev_stage_ID
- tissue_type_ID


First we will add a `tissue_type_ID` column. There are two allowed values `brain` and  `lung`. For each cell in the `tissue_type` column with the value `brain` we want the corresponding cell in the new column to contain the ID `MA:0000168` and the corresponding value for `lung` is `MA:0000415`. We can specify this with an if-expression using General Refine Expression Language (GREL).

1. Click the down arrow next to `tissue_type` > `Edit column` > `Add column based on this column...`. A pop-up window will appear.
2. On top, type `tissue_type_ID` in the `New column name` field
3. In the big text field where it now says `value` copy and paste
`if(value == 'lung', 'MA:0000415',
    if(value == 'brain', 'MA:0000168',
null)))`
4. In the preview at the bottom, verify that everything looks correct and press `OK`.  
A new column called `tissue_type_ID` should have been added to the table.

> ## Exercise
> Use the same strategy to add new columns for `strain_ID` and `dev_stage_ID`.
>
> > ## Solution
> > #### strain_ID
> > 1. Click the down arrow next to `strain` > `Edit column` > `Add column based on this column...`. A pop-up window will appear.
> > 2. On top, type `strain_ID` in the `New column name` field
> > 3. In the big text field where it now says `value` copy and paste
`if(value == 'C57BL/6', 'NCIT:C14424',
    if(value == 'BALB/cJ', 'NCIT:C14657',
null)))`
> > 4. In the preview at the bottom, verify that everything looks correct and press `OK`
> > A new column called `strain_ID` should have been added to the table.
> >
> >#### dev_stage_ID
> > 1. Click the down arrow next to `dev_stage` > `Edit column` > `Add column based on this column...`. A pop-up window will
> > appear.
> > 2. On top, type `dev_stage_ID` in the `New column name` field
> > 3. In the big text field where it now says `value` copy and paste
`if(value == 'adult', 'BTO:0001043',
    if(value == 'pup', 'BTO:0004377',
    if(value == 'embryo', 'BTO:0000379',
null)))`
> > 4. In the preview at the bottom, verify that everything looks correct and press `OK`
> >A new column called `dev_stage_ID` should have been added to the table.
> {: .solution}
{: .challenge}

### Removing and reordering data
We have identified and correctly named the columns we want to include for the ENA submission. The next step is to remove all of the remaining data that is not needed.

> ## Exercise
> 1. Use the same strategy as above to only keep samples used for sequencing experiments.
> 2. Remove all irrelevant columns by clicking the down arrow next to `All` > `Edit columns` > `Re-order / remove columns...`
>
> > ## Solution
> >To exclude all rows from other experiment types than `sequencing`
1. Create a filter for the column `experiment type` by clicking the down arrow in
the column header > `Text filter`
2. Type `sequencing` in the text field and press return. 6 matching rows will be displayed.
3. In the same box, press `invert` in the top right.
4. Click the down arrow next to `All` in the left-most column header > `Edit rows` > `Remove matching rows`
5. Remove or reset the filter. Now, all remaining 6 rows should be of experiment type sequencing.
>>
6. Remove all but the following columns:
- sample_alias  
- sample_title
- tax_id
- scientific_name
- strain
- sub_strain
- dev_stage
- tissue_type
- strain_ID
- dev_stage_ID
- tissue_type_ID
> {: .solution}
{: .challenge}


### Creating a tsv-file compatible with the ENA

1. Click `Export` in the top right and select the file type you want to export the data in. In this case we will choose `Tab-separated values` (`tsv`).
2. The file will be saved in your default downloads folder. Move the file to your course folder and save it as `ENA_samples_openrefine_lesson.tsv`
3. Open the file in a text editor such as NotePad or TextEdit.
4. Add the two following lines at the beginning of the file and `save`. Make sure that you have a tab between `#checklist_accession` and `ERC000011`

#checklist_accession  ERC000011  
#unique_name_prefix



{% include links.md %}
