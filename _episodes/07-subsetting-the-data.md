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

In the next lesson of the _Introduction to Data Management Practices Workshop_ we will 
act as a researcher who wants to submit a subset of the data to the repository [ENA](https://www.ebi.ac.uk/ena/browser/home) (European Nucleotide Archive).
To do so we need to prepare sample metadata to conform to the metadata standards
of the repository.

We need to consider the following questions:

- **Which of the existing columns are relevant for the submission?**
- **Are they named correctly?**
- **Are there additional columns that need to be added?**

<BR>
First, we know the data contain three samples per individual, i.e. every individual are represented by three rows in the data. Now, we want to extract one of those samples for submission, namely the ones produced by the Illumina NEBNext prep kit. We identify these as "NebNext" in the column `configuration`. 

1. Create a filter for the column `configuration` by clicking the down arrow in the column header and select `Text filter`.
2. A filter box will appear to the on the left side. Type `NEB` in the text field and press return. 29 matching rows will be displayed.
3. In the same box, press `invert` in the top right to select all the rows from researchers other than Sam. Note that the box header will turn orange to indicate inverted results.
4. Confirm that there are 62 matching rows.
5. Click the down arrow next to `All` in the left-most column header > `Edit rows` > `Remove matching rows`
6. Remove or reset the filter. Now, all remaining 29 rows should be `NEBNext` samples.

<!--

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
-->
<BR>
## Creating new columns

Sometimes a new variable needs to be added to a dataset, a new set of data input, or a transfer of information from another data source. So far we have only covered editing already existant columns and cells, but how do we create space for new data in an already open project?

For example, in our opened dataset we are missing a column for naming the institute responsible for collecting the listed samples. To create such a column, we select a column juxtaposed to where we want to create a new, and in that column select `Edit column` > `Add column based on this column...`. In the new window, in `New column name`, type `collector name`, but leave the input `value` unedited. Clicking `OK` now creates a new column to the right of the one we just used, with identical values in all rows. Repeating what we did earlier in the lesson, `edit` the contents to the input `Valeria Ghiselli` and select `Apply to All Identical Cells`.     
<BR>

> ## Exercise 6.1
>
> Add a new column called `collecting entity`, and fill all cells with the input `Amedeo di Savoia`. Can you generate the column to the left of the column `collector name`?
>
> > ## Solution
> >
> > 1. On the `Description` column, select `Edit column` > `Add column based on this column...`.
> > 2. Type `collecting entity` in `New column name`, keep the input `value` as before.
> > 3. `edit` the contents of the cells to `Amedeo di Savoia` and select `Apply to All Identical Cells`.
> > Note that the values of the new column can be previewed at the bottom
> {: .solution}
{: .challenge}
<BR>

**We made a mistake!** 
The column name `collecting entity` was an incorrect input. The ENA checklist suggests it as better named `collecting institution`. We need to rename the column, but how do we do it? 

To rename the column `collecting institution`
1. Click the down arrow next to `collecting entity` > `Edit column` > `Rename this column`. A pop-up window will appear on top.
2. Type in `collecting institution` and press return.
<BR>

## Join columns
We still lack working aliases for the samples. Aliases are only used as communicative references in a project, but can help in identify, separate, and cluster individual samples in downstream analyses.

To create aliases for our samples we can combine cell information from the columns `configuration` and `host subject id` to create unique combinations.

1. First we click the down arrow next to `configuration` and select `Edit column` > `Join columns...`. A pop-up window will appear. 
2. On the left side, choose which columns to join. Verify that `configuration` is already ticked and tick `host subject id` as well. (Notice that you can change the order of the information to combine by drag-and-drop the order of ticked columns in the list).
To the right, there are several options for the join.
3. In the separator field, enter an underscore `_`.
4. Click ` Write result in new column named… ` and enter `alias`
5. If ticked, untick the option `Delete joined columns.` (we wish to keep the originating columns) and click `OK`.
<BR>

#### Generate infomation by joining multiple columns
Our dataset still lack information for the mandatory ENA checklist field `isolate`, which is defined as the "individal isolate from which the sample was obtained". Such information can be generated in a number of formats, but here we will use [organism/host/location/isolate/date]. 

> ## Exercise 6.2
>
> Add a new column with empty cells called `isolate`, and populate the cells with information for **[organism/host/location/isolate/date]** present in other columns.
> > ## Solution
> >
> > 1. On the `host_subject_id` column, select `Edit column` > `Add column based on this column...`.
> > 2. Type `isolate` in `New column name`, but add the input `null`. This creates a new column named `isolate` populated with empty cells.
> > 3. Select `Edit column` > `Join columns...` and mark the corresponding column names for; 
- `organism` -> `virus identifier`
- `host` -> `host common name`
- `location` -> `geographic location (country)`
- `isolate` -> `alias`
- `date` -> `collection date`.  
> > 4. Add a slash `/` as separator, and make sure not to tick `Delete joined columns`. Once you are confident your selection is correct, make sure to drag-and-drop the columns to appear in the above order.
> > 5. Select `OK`. All cells should now be populated with isolate information. 
> {: .solution}
{: .challenge}
<!--

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
-->
<BR>

### Removing and reordering data
We have now identified and correctly named the columns we want to include for the ENA submission. The next step is to validate the dataset prior to submission, and that it conforms with a controlled vocabulary (ENA Checklist).

> ## Exercise
> 1. Using your knowledge from the previous exercises, make sure all required variables are in order and all eventual typos are corrected.
> 2. Export the dataset in `csv` format.
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
