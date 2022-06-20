## Infobaleen Documentation

The documentation uses [MkDocs](https://www.mkdocs.org/), which is a fast and simple static site generator geared towards building project documentation. Documentation source files are written in Markdown, and configured with a single YAML configuration file.

### Install MKDocs

To install MkDocs, run the following command from the command line (requires python):

```pip install mkdocs```


### Procudure for updating the online documentation 

1. Download the customer-succes repo:
    * First time its done: Run `git clone https://github.com/infobaleen/customer-success.git` 
    * Subsequently: Go to the local folder and run `git pull`

2. Check the generated version
    * Run `mkodcs serve`. This will serve the local version at `http://127.0.0.1:8000`
    * In the command window you might se `WARNING` messages. This is often for files that are not included in the documentation. Add these in the menu in `mkdocs.yml`

3. Push changes to Github
    * If you did any changes in step 2, push these to Github by:
        1. `git add -A`
        2. `git commit -m "Added latest changes"`
        3. `git push`


4. Push changes to the online Github page
     * `mkdocs gh-deploy` 