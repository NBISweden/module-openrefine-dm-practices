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

In the this lesson of the _Introduction to Data Management Practices Workshop_ we will 
act as a researcher who wants to submit a subset of the data to the repository [ENA](https://www.ebi.ac.uk/ena/browser/home) (European Nucleotide Archive).
To do so we need to prepare sample metadata to conform to the metadata standards
of the repository.

We need to consider the following questions:

- **Which of the existing columns are relevant for the submission?**
- **Are they named correctly?**
- **Are there additional columns that need to be added?**

<BR>
First, we know the data contain three samples per individual, i.e. every individual is represented by three rows in the data. Now, we might want to extract one of those samples for submission, namely the ones produced by the Illumina NEBNext prep kit. We identify these as "NEBNext" in the column `configuration`. 

1. Create a filter for the column `configuration` by clicking the down arrow in the column header and select `Text filter`.
2. A filter box will appear to the on the left side. Type `NEB` in the text field and press return. 29 matching rows will be displayed.
3. In the same box, press `invert` in the top right to select all the rows which *do not* have the configuration NEBNext. Note that the box header will turn orange to indicate inverted results.
4. Confirm that there are 62 matching rows.
5. Click the down arrow next to `All` in the left-most column header > `Edit rows` > `Remove matching rows`
6. Remove or reset the filter. Now, all remaining 29 rows should be `NEBNext` samples. This subsection of the data can be saved using the `Export` drop down menu as `comma-separated values`, to be imported into other software like `R`. 
<BR>

## ENA sample metadata
ENA sample metadata can be divided in three groups.
- Mandatory metadata
- Checklist-based metadata
- User defined metadata

In a previous lesson in this workshop around [metadata](https://nbisweden.github.io/module-metadata-dm-practices/05-finding-ontologies/index.html) you already came across the ENA checklists. When creating a data dictionary you identified ENA variables based on the default checklist and ontologies to identify allowed values. We will come back to these in a while but first we will look at the mandatory fields.

### Mandatory fields
Some metadata are mandatory for all samples submitted to ENA regardless of the checklist chosen. We will try to map the existing columns to these variables.

**Basic details**  
sample_alias - _The unique name is a submitter provided unique identifier_  

**Organism details**  
tax_id - _The NCBI taxonomy id_  
scientific_name - _based on tax_id_


> ## Exercise
> Can any of the existing columns be used as `sample_alias`, `tax_id` and `scientific_name`?
>
> > ## Solution
> > 1. `sample_alias` needs to be created. We will do that under the header "Join columns". 
> > 2. A column `tax_id` already exists
> > 3. A column `scientific_name` already exists
> {: .solution}
{: .challenge}

<BR>
## Creating new columns

Sometimes a new variable needs to be added to a dataset, a new set of data input, or a transfer of information from another data source. So far we have only covered editing already existing columns and cells, but how do we create space for new data in an already open project?

For example, in our dataset we are missing a column for naming the institute responsible for collecting the listed samples. To create such a column, we select a column to the left of where we want to create a new, and in that column select `Edit column` > `Add column based on this column...`. In the new window, in `New column name`, type `collector name`, and enter `null` as `value`. Clicking `OK` now creates a new column to the right of the one we just used, without cell values. Repeating what we did earlier in the lesson, `edit` the contents to the input `Valeria Ghiselli` and select `Apply to All Identical Cells`.     
<BR>

> ## Exercise 6.1
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
<BR>

**We made a mistake!** 
The column name `collecting entity` was an incorrect input. The ENA checklist suggests it as better named `collecting institution`. We need to rename the column, but how do we do it? 

To rename the column `collecting institution`
1. Click the down arrow next to `collecting entity` > `Edit column` > `Rename this column`. A pop-up window will appear on top.
2. Type in `collecting institution` and press return.
<BR>

## Join columns
As we noted in the metadata module, there was a column in the data for `sample_alias`. In this dataset we have lost that information and need to re-enter it. Aliases are only used as communicative references in a project, but can help in identify, separate, and cluster individual samples in downstream analyses.

To create aliases for our samples we can combine cell information from the columns `configuration` and `host subject id` to create unique combinations.

1. First we click the down arrow next to `configuration` and select `Edit column` > `Join columns...`. A pop-up window will appear. 
2. On the left side, choose which columns to join. Verify that `configuration` is already ticked and tick `host subject id` as well. (Notice that you can change the order of the information to combine by drag-and-drop the order of ticked columns in the list).
To the right, there are several options for the join.
3. In the separator field, enter an underscore `_`.
4. Click ` Write result in new column named… ` and enter `sample_alias`.
5. If ticked, untick the option `Delete joined columns.` (we wish to keep the originating columns) and click `OK`.
6. Move the new `sample_alias` column to the beginning by selecting `Edit column` > `Move column to beginning`.
<BR>

#### Generate infomation by joining multiple columns
Our dataset still lack information for the mandatory ENA checklist field `isolate`, which is defined as the "individal isolate from which the sample was obtained". Such information can be generated in a number of formats, but here we will use a combination of [organism/host/location/isolate/date]. 

> ## Exercise 6.2
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
<BR>

### Checklist-based and user defined metadata
Now let's have a look at the data dictionary from the metadata lesson. Which variables did you identify an ENA variable name for based on the ENA checklist? Rename the columns where necessary.

> > ## Solution
> > #### Data dictionary:
> >
> > | Current variable name | ENA Variable name | Measurement unit | Allowed values | Definition | Description |
> > |-|-|-|-|-|-|
> > | sample_alias |  |  |  |  |  |
> > | date | collection date |  | format: YYYY-MM-DD, >=proj_start_date & <=today | Date of experiment ??? |  |
> > | tissue | isolation source host-associated |  |  |  |  |
> > | age | host age | years | | |  |
> > | health state | host health state |  | diseased, healthy |  |  |
> > | sex | host sex |  | male, female, unknown |  |  |
> > | symptoms | illness symptoms |  | fever, soar throat, fatigue, ageusia  |  |  |
> > | disease outcome | host disease outcome |  | dead, recovered |  |  |
> > | DESCRIPTION | sample description |  |  |  |  
> >
> >
> > Renaming columns:
> > 1. Click the down arrow next to a column titel to rename > `Edit column` > `Rename this column`. A pop-up window will appear on top.
> > 2. Type in the ENA variable name from the Data dictionary above and press return.  
> > 3. Repeat the steps to rename all columns mentioned in the list above.
> {: .solution}
{: .challenge}

With all columns renamed to comply with the ERC000033 checklist, what remains is to check if entered values for the field name also corresponds with correct field restrictions. 

First we notice the values for `host health state` is only semi-correct. In our column we have stated the values to `ill` and `healthy`. The correct values should be `diseased` and `healthy`.

Second, we can see some inconsistencies in the `illness symptoms` column. Make sure to correct any mis-spelling (e.g. sore throt), and replace `loss of taste` with the checklist term `ageusia`.
<BR>
<BR>
### Removing and reordering data
We have now identified and correctly named the columns we want to include for the ENA submission. The next step is to validate the dataset prior to submission, and that it conforms with a controlled vocabulary (ENA Checklist).

> ## Exercise
> 1. Using your knowledge from the previous exercises, make sure all required variables are in order and all eventual typos are corrected. Also make sure no cells are empty or with incorrect missing values.
> 2. Export the `NEBNext` subset of data in `csv` format.
>
> > ## Solution
> >To exclude all rows from other experiment types than `NEBNext`
1. Create a filter for the column `configuration` by clicking the down arrow in
the column header > `Text filter`
2. Type `NEBNext` in the text field and press return. 29 matching rows will be displayed.
3. In the same box, press `invert` in the top right.
4. Click the down arrow next to `All` in the left-most column header > `Edit rows` > `Remove matching rows`
5. Remove or reset the filter. Now, all remaining 6 rows should be of experiment type NEBNext.
>>
6. Remove all but the following columns:
- sample_alias  
- collection date
- tax_id
- scientific_name
- sample description 
- geographic location (country)
- geographic locatoin (region and locality)
- host disease ooutcome
- host common name
- host subject id
- host age
- host health state
- host sex
- collector name
- collecting institute
- isolate
> {: .solution}
{: .challenge}

<BR>
### Creating a tsv-file compatible with the ENA

1. Click `Export` in the top right and select the file type you want to export the data in. In this case we will choose `Tab-separated values` (`tsv`).
2. The file will be saved in your default downloads folder. Move the file to your course folder and save it as `ENA_samples_openrefine_lesson.tsv`
3. Open the file in a text editor such as NotePad or TextEdit.
4. Add the two following lines at the beginning of the file and `save`. Make sure that you have a tab between `#checklist_accession` and `ERC000033`

- #checklist_accession  ERC000033  
- #unique_name_prefix



{% include links.md %}
