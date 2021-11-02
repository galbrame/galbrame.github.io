# How To Host a Resume on GitHub Pages

Learn how to take your job search to the next level by hosting and formating your resume for free using Markdown, Jekyll, and GitHub Pages. This README will also endevour to impart some general principles of technical writing (from the perspective of Adrew Etter in _Modern Technical Writing_) that you can employ in your own projects.

Hosting your site won't just show off your resume to potential employers - it will show off your technical skills. It will be different than applying for a specific job, since you'll need to make a more general resume, but keep your overall audience in mind: prospective companies in your chosen field. One of Etter's key points in his book is knowing your audience before writing anything. Think about who could be reading your resume, what they will be looking to get out of reading your work.


## PREREQUISITES
For this project, you will need:
* A resume that is already formatted in Markdown
  * Preferably GitHub Flavoured Markdown (GFM) to take advantage of the extended features
  * If you aren't familiar with Markdown, see [More Resources](#more-resources) for a good tutorial and GFM reference
* A Markdown editor (see [More Resources](#more-resources) for some suggestions)
* A GitHub account
* Jekyll (or an alternative static site generator)
* Ruby<sup>[1](#notes)</sup> (version 2.5.0 or higher)
* Git Bash

A little bit about my personal setup:
* Operating System: Windows 10<sup>[2](#notes)</sup>
* Mardown editor: IntelliJ IDEA Community
* Ruby version: 2.7.4p191 (x64-mingw32)
* Jekyll version: 4.2.1
* Git Bash: [Git for Windows](https://gitforwindows.org/)


## STEPS

### Step 1: Creating The Repository

1) We want our resume to be the landing page for our GitHub Pages account, so we'll need to make a new repository. After logging into GitHub, click on the "+" sign at the top right of the page. The "+" can be found on any GitHub page. Select "New repository" from the dropdown menu.

2) If you have more than one option in the **Owner** dropdown, select the account you would like your resume associated with.

3) In the repository name, type ```<user>.github.io```, where ```<user>``` is your username.

4) Leave the description blank, unless you want the text to show up on your resume as well. Alternatively, you could just add the text to your resume.md file.

5) Leave the repository as Public so that anyone will be able to find your new digital resume.

6) Don't tick any of the initialize option checkboxes, since we will be adding all of the files we need ourselves.


### Step 2: Creating Your Site Locally

1) Create a local folder on your computer where your site's source files will be stored.

2) Open Git Bash and navigate to the folder you made for your site's source files. _Note_: if any of the folders have a space in the name, you will need to put quotation marks around the folder name (double or single) or else Git Bash will think you are trying to give it extra arguments. Alternatively, you can use a backslash before the space, such that ```New Folder``` would be ```New\ Folder```.

3) Initialize a local Git repository with the same name as the repository you made on GitHub, and change directory to the new repository.
   ```
   git init <username>.github.io
   cd <username>.github.io
   ```

5) We are going to use our gh-pages branch as our publishing source, so we will need to use checkout<sup>[3](#notes)</sup> to create and switch to that branch.
   ```git checkout --orphan gh-pages```

6) Create a new Jekyll site, using
   ```jekyll new --skip-bundle .```
   * _NOTE_: the period is important because it denotes the current directory. If you forget it, yu will get "Error: You must specify a path."

7) Copy or move your resume markdown file into the _posts folder and delete the auto-generated example post.

_NOTE_: Keep Git Bash open because you will use it again at the end of the next step.


### Step 3: Prep Your Site for GitHub

1) Open the Gemfile that Jekyll just made. If you are comfortable with Vi or Emacs, you can do it right from Git Bash. Or you can open it with an editor, such as IntelliJ, Visual Studio, Notepad++, or even just Notepad.

2) Find the line starting with ```gem "jekyll"```. Comment it out by adding "#" to the start of the line. 

3) Find the ```# gem "github-pages"``` line, just a few lines below that. Uncomment it by deleting the "#".

4) Change the github-pages line to match:
    ```
    gem "github-pages", "~> <version>", group : :jekyll_plugins
   ```
   ```<version>``` is the latest version of the github-pages gem. You find the versio number in this [list](https://pages.github.com/versions/).

6) Save and close Gemfile.

7) Open the _config.yml file in a text editor of your choosing.

8) Find the "baseurl" line. Add the name of your repository between the quotation marks so that the line reads 
   ```
    baseurl: "<username>.github.io"
   ```
   
9) Save and close _config.yml.

10) Return to the Git Bash command line and run ```bundle install``` to create the proper Gem dependencies for your site.


### Step 4: Pushing Your Site to GitHub

1) Add and commit your site source by running:
   ```
   git add .
   git commit -m 'Initial GitHub pages site with Jekyll'
   ```

2) Add your repository to GitHub.com:
   ```
   git remote add origin https://github.com/<username>/<username>.github.io
   ```

3) Push the local repository to GitHub:
   ```
   git push -u origin gh-pages
   ```


You should now have your resume hosted on its very own static website. Your url should be ```https://<username>.github.io```. Alternatively, you can find the url by going to your GitHub respository and going to Settings > Pages.


## OPTIONAL
### Customizing the Theme
GitHub offers 12 supported Jekyll themes, including the default "Minimal" that your site is already using. You can select a different theme through Settings > Pages > Change theme. Alternatively, many other unsupported themes can be found through search engines. These themes will have instructions on how to add them to your own site.


## MORE RESOURCES
* A very basic but quick [Markdown tutorial](https://www.markdowntutorial.com/)
* A handy reference guide for [GitHub Flavoured Markdown](https://docs.github.com/en/github/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)
* University of Manitoba Career Services offers a free [resume writing workbook (pdf)](https://www.google.ca/url?sa=t&rct=j&q=&esrc=s&source=web&cd=&ved=2ahUKEwj5zL3tyffzAhUCl2oFHdtrBW0QFnoECAMQAQ&url=https%3A%2F%2Fumanitoba.ca%2Fstudent%2Fcareerservices%2Fmedia%2FResume.pdf&usg=AOvVaw1-mk1zbwOpgkFdHZBIfrlh)
* A short list of potential Markdown editors:
  * Atom
  * Notepad++
  * Visual Studio
  * Vim (not user friendly if you are not already familiar with it)


## AUTHORS & ACKNOWLEDGMENTS
Author: Megan Galbraith

A big thank you to all of Group 1 for helpful edits and constructive criticism:
* Andrea Abellera
* Matthew Kwiatkowski
* Andrii Provozin
* Ian Tobinpe


## FAQ

1) Why Markdown?


   * Markdown is a handy lightweight markup language with straightforward syntax. It is quickly and easily picked up and applied by nearly everyone and very human-readable. It is far easier and quicker to create a Markdown file and convert it to xml using Jekyll than it is to create something similar with html or xml. It's also one of the most popular lightweight markup languages, so choosing it over anohter lightweight markup language could be considered "future proofing" your material, as it is more likely to be supported for some time.
   

2) Why GitHub rather than Wordpress?


  * While both offer free versions of hosting, Wordpress is bloated with extraneous functionality that a lot of basic websites don't need. It relies on PHP and backened databases, which require varying degrees of maintenance and can crash. We are just hosting a simple resume. As Etter points out, static sites are perfect because of their speed, simplicity, portability, and security. And with a distributed version control system (DVCS) like GitHub, managing your site is quick, easy, and portable. Plus, developers prefer DVCSs, so you'll be showing off your knowledge of them.


## NOTES
1) Don't worry - you won't have to know or use any Ruby for this project. It is purely necessary to run Jekyll.
2) Windows is not officially supported by Jekyll, but it can be installed and run with careful "[tweaks](https://jekyllrb.com/docs/installation/windows/)."
3) '''checkout''' is the git command for switching between branches in your repository.