# class_aug28

## Class Example

To push documents to GitHub, following the following steps

`git init`

This command initializes/reinitializes a repository for the project
youre working on.

`git add notes_examples/class_aug28.qmd`

This command stages the doc you want to push to GitHub. We aren’t
actually pushing the document out yet. Be sure that the file path and
file name are correct. Otherwise, you will get an error saying the file
is not found/

`git commit -m "initial commit`

This command actually commits the document to GitHub. In quotation
marks, add a note about what you are committing. Here, I am making the
initial commit.

From this point, there is some code on GitHub we need to copy and paste
over to get our document sent to the right repository.

`git remote add origin https://github.com/cassidycatrett/micr_575.git`

This command denotes the remote repository location we want to use. This
path will be different for each project you’re working on.

`git branch -M main`

This command denotes that we are adding this directory to the main
branch of our repository.

`git push -u origin main`

This is the actual command that pushes our document from our desktop to
our remote repository. Here, we have to log in with our GitHub username
and personal access token or access token. I used an access token for
this but plan to swap to ssh authentication. Once the username and
access token was authorized, my document was successfully pushed to my
GitHub repository.
