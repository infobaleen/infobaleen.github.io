# Table of Contents
1. [Format of files](#format-of-files)
1. [Running scripts](#running-scripts)
    1. [Generate README Table of Contents](#generate-readme-table-of-contents)
        1. [Using the script](#using-the-script)
        1. [How the script works](#how-the-script-works)
    1. [Generate Table of Contents in files](#generate-table-of-contents-in-files)
[](#table-of-contents)

[*Back to top*](#table-of-contents)

# Format of files

All files consist of a top row with a header starting with `#`. Running the Table of Contents generator will add a table of content above this title row. Running it again will update the existing table of contents.

[*Back to top*](#table-of-contents)

# Running scripts

[*Back to top*](#table-of-contents)

## Generate README Table of Contents

[*Back to top*](#table-of-contents)

### Using the script

When new edits are made to the file tree, whether it be renaming, removing or creating files or directories, run the `readme_generator.py` to generate a new README.md with updated table of contents and hyperlinks. Note that you must have the repo as your working directory for the script to work, such as:

`C:\Users\MyUser\Infobaleen\customer-success> python3 readme_generator.py`

[*Back to top*](#table-of-contents)

### How the script works
The script opens the folder `Documentation` from the current working directory, which is why it has to be run from the repo folder. It then walks the file tree and writes a line to the readme file for each directory it encounters, and then for all files in that directory.

The markdown formatting for each **directory** is done in three parts:
1. Create an indent (4 spaces) for the current depth from the `Documentation` folder minus 1.
2. Create a header with a `1.` followed by one `#` for each level below the `Documenatation` folder.
3. Create a link by texting the title of the directory and linking to the github repo based on the directory name

The markdown formatting for each **file** is done in three parts:
1. Create an indent (4 spaces) for the current depth from the `Documentation` folder.
2. Create a bullet list by adding a `- ` to the line.
3. Create a link like with the directories, but replace any `-` with spaces and remove `.md` suffix.

[*Back to top*](#table-of-contents)

## Generate Table of Contents in files

In development in `table_of_contents_generator.py`

[*Back to top*](#table-of-contents)
