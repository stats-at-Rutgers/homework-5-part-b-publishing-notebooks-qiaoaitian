# Homework-5b-publishing_notebooks

- My netid is ``yq102`` and my name is ``Yifeng Qiao`` (edit this with your name)


1. My notebook is published as a github gist at    
https://gist.github.com/8f91cf193e604ea4c7f6d2d1be69d759.git

2. My notebook is published on ``nbviewer`` at      
https://nbviewer.org/gist/someGithubUser/????????????????????????/

3. My GitHub Pages website is published at    
https://stats-at-rutgers.github.io/Homework-5b-publishing_notebooks-????????/

4. My notebook is published as HTML thanks to ``nbconvert`` hosted on Github Pages at     
https://stats-at-rutgers.github.io/Homework-5b-publishing_notebooks-??????/rates.html

# Homework 5: sharing, publishing notebook

In the Part A of Homework 5, you have performed an analysis with some visualizations on exchange rates data from the European Central Bank.
In this Part B, you will learn several ways to share your notebook as a link on the web, so that your collaborators can easily access it.
When you have done all the steps below, edit this file on your github assignment repository with the URL where your notebook can be accessed.


### 1. Gist

Go to <https://gist.github.com/> and login with your github account. Create a ``secret gist`` with filename ``rates.ipynb`` (you need to type the filename), and populate the content of the file by dragging the notebook ``rates.ipynb`` file from your computer to the large text area. A secret gist webpage will be created for you where GitHub renders the notebook. If you created a _secret_ gist (as opposed to a public gist), only visitors with the knowledge of the gist URL will be able to access it. An example of a gist as a webpage is <https://gist.github.com/bellecp/2606f67631064c7e6c472f7b3262fe16> from the previous lecture. When you are done, copy your gist URL, edit this ``README.md`` and add your URL in list item 1 above.        
_Github gist are actual git repositories that can be cloned, although this is a story for another day._

### 2. NBViewer

An alternative to share an already existing github gist on a webpage is nbviewer. Visit <https://nbviewer.org> and submit your gist URL there. You will be provided with a URL of the form <https://nbviewer.org/gist/someGithubUser/ew483101d9dw10d0w1n0nd1> that renders your notebook in a clean interface. Copy that nbviewer URL, edit the current file and put your nbviewer URL in list item 2 above.

### 3. Enable GitHub Pages

Webpages are HTML files that can be consumed by web browsers. You can also host a static website (made of HTML files, of or markdown files (ending in ``.md``)) using GitHub Pages. In the case of ``.md`` files, GitHub Pages will convert those to HTML pages automatically for you.
Go in the settings of this assignment repository and find ``Pages`` in the left menu. Select ``Deploy from a branch``, choose the ``main`` branch, and save.
Now go into the ``Actions`` tab of the repository and verify that a `` pages build and deployment`` workflow has been started. This means that GitHub is in the process
of publishing the content of this repository as a website. When the workflow is completed, to back to the `Settings->Pages`` menu to and see something resembling
```
Your site is live at https://stats-at-rutgers.github.io/Homework-5b-publishing_notebooks-??????/
```
By default, the homepage at this URL will be taken either from ``index.html``, or ``index.md``, or ``README.md``.
Copy this URL of your published Github Pages website, edit this README.me file and add this URL to list item 3 above.


### 4. nbconvert and converting notebooks to HTML

Install the ``nbconvert`` python package on your laptop and run
```
jupyter nbconvert rates.ipynb --to html
```
in order to convert your notebook file to a HTML file consumable by web browsers. Verify that this created a file ``rates.html`` next to your existing ``rates.ipynb`` file on your laptop.  Next, commit this ``rates.html`` file on this assignment repository, next to the present ``README.md`` file. Once this ``rates.html`` file is pushed on this repository on github, verify that a ``pages build and deployment`` workflow is starting, and when it is finished, that you can access the notebook as a webpage hosted on your GitHub pages website, by appending ``rates.html`` to the base URL of the previous question, to obtain something of the form
```
https://stats-at-rutgers.github.io/Homework-5b-publishing_notebooks-??????/rates.html
```
Verify that you can access this URL and view your notebook. Finally. Copy this URL ending in ``rates.html`` at the top of this README file in list item 4.

### 5. Converting publishing your notebooks automatically

Now, our goal will be to automate this using github actions. We will have the ``rates.ipynb`` actual notebook committed on the ``main`` branch,
while the Github Pages website will be published out of the ``gh-pages`` branch.

- Delete any ``rates.html`` from this repository using ``git rm rates.html`` or otherwise.
- Commit your ``rates.ipynb`` to the ``main`` branch.
- Create a file ``requirements.txt`` containing oneline with content ``nbconvert``. We will need the Github Action worker to perform ``nbconvert`` by theirself, this ``requirements.txt`` file will tell them which packages to install.
- Verify that you have a branch ``gh-pages`` already created. Go to ``Settings->Pages``, select ``Deploy from a branch``, but now select instead the ``gh-pages`` branch.
- Check out the file ``.github/workflows/publish_notebook_in_html.yml`` file and inspect each line carefully. 
- Go to the Github Actions tab, and trigger this workflow manually (main branch). When finished, verify that a ``rates.html`` file has been committed to the ``gh-pages`` branch, and that this triggered an extra ``pages build and deployment`` workflow (indeed, our ``publish_notebook_in_html.yml`` modified the ``gh-pages`` branch which is set to be published by Github pages, so any modification on ``gh-pages`` will trigger a new deployment of the Github Pages website).
- Currently, the ``publish_notebook_in_html.yml`` workflow needs to be manually triggered due to block
```
on:
  workflow_dispatch
```
which tells Github Actions that the workflow will only be triggered manually. Change the workflow to automatically every time a new commit is pushed on the ``main`` branch, by editing the ``.github/workflows/publish_notebook_in_html.yml`` file and replacing the above ``on: (...)`` block by
```
on:
  workflow_dispatch:
  push:
    branches:
      - main
```
so that the workflow will be either triggered manually or on every new commit pushed on the ``main`` branch.
Now, make a few minor changes to your ``rates.ipynb`` notebook on the ``main`` branch, push the changes, and observe the automatic trigger of the
``publish_notebook_in_html`` that will convert the new notebook to an ``html`` and commit this ``html`` file on the ``gh-pages`` branch, which will
trigger a ``pages build and deployment`` workflow to publish this new html on Github Pages.


### Grading

Your published notebooks (at the URLs shown at the top of this file) will be reviewed and graded manually to check the curves from Homework-5 part A.


### Student developer pack

Github Pages is available on homework assignments. For your own repositories, it is available for free for public repositories.
For your private repositories, as of 2024 Github Pages is available provided that you have a GitHub Pro account or that you have
applied for free for the Student Developer pack at <https://education.github.com/pack>. I recommend you apply, this will give
you several nice benefits for your project--in particular, access to host GitHub Pages websites for your private repositories.


