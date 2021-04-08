---
layout: page
title: Setup
---

> ## Data
>
> The data for this lesson is part of the Introduction to Data Management
> practices workshop materials. It is a teaching dataset compiled for this workshop.
> It contains research data from the public domain as well as data created
> specifically for this workshop with inspiration from real data.
>
> The `samples_openrefine_lesson.csv` used in this lesson is mimicking a
> spreadsheet file used by a research
> lab working with genetically modified mice to study biomedical questions.
> Each researcher is responsible to record every animal used for an experiment in this
> spreadsheet. Little or no instructions on how to use it is provided and
> each researcher has their own way of working.
>
>
> **Download**  
> The folder containing the entire dataset for the Introduction to Data Management practices Workshop
>from [this page](https://doi.org/10.17044/scilifelab.14301317). Direct link : [https://doi.org/10.17044/scilifelab.14301317](https://doi.org/10.17044/scilifelab.14301317)  
>The three files needed for this lesson is found in dm-practices/6-openrefine  
**or**  
>The files for this lesson only
> - [samples_openrefine_lesson.csv](data/samples_openrefine_lesson.csv)
> - [data_cleaning_script_openrefine_lesson.txt](data/data_cleaning_script_openrefine_lesson.txt)
> - [ENA_sample_metadata_script.txt](data/ENA_sample_metadata_script.txt)
{: .prereq}


> ## Software
>
> For this lesson you will need **OpenRefine** and a web browser.  
> Note: this is a Java program that runs on your machine (not in the cloud). It runs inside your browser, but no web connection is needed.
>
> A text editor (like NotePad or TextEdit) is also needed.
{: .prereq}

> ## Presentation
>
> Slides for this module are available [here](data/module-openrefine-dm-practices.pdf)
{: .prereq}

#### Windows

- Check that you have Firefox or Chrome browsers installed and set as your
default browser. OpenRefine runs in your default browser. It will not run correctly in Internet Explorer.
- Download software from [http://openrefine.org](http://openrefine.org)
- Unzip the downloaded file into a directory by right-clicking and
selecting “Extract…”. Name that directory something like OpenRefine.
- Go to your newly created OpenRefine directory.
- Launch OpenRefine
- Click the openrefine.exe (this will launch a command prompt window, but you can ignore that and wait for the browser to launch)
- If you are using a different browser, or OpenRefine does not automatically open for you, point your browser at http://127.0.0.1:3333/ or http://localhost:3333 to launch the program.
- If you get a Java error when you try to open it you can try downloading [OpenRefine 3.4 beta 2 Windows kit with embedded Java](https://openrefine.org/download.html).


#### Mac

- Check that you have Firefox or Chrome browsers installed and set as your
default browser. OpenRefine runs in your default browser. It will not run correctly in Internet Explorer.
- Download software from [http://openrefine.org](http://openrefine.org)
- Unzip the downloaded file into a directory by double-clicking it. Name
that directory something like OpenRefine.
- Go to your newly created OpenRefine directory.
- Launch OpenRefine
- Drag icon into Applications folder, and Ctrl-click/Open… it.
- If you are using a different browser, or OpenRefine does not automatically open for you, point your browser at http://127.0.0.1:3333/ or http://localhost:3333 to launch the program.

#### Linux

- Check that you have Firefox or Chrome browsers installed and set as your
default browser. OpenRefine runs in your default browser. It will not run correctly in Internet Explorer.
- Download software from [http://openrefine.org](http://openrefine.org)
- Unzip the downloaded file into a directory. Name
that directory something like OpenRefine.
- Go to your newly created OpenRefine directory.
- Launch OpenRefine
- Type ./refine into the terminal within the OpenRefine directory
- If you are using a different browser, or OpenRefine does not automatically open for you, point your browser at http://127.0.0.1:3333/ or http://localhost:3333 to launch the program.
