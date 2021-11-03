# How To Host a Resume on GitHub Pages Using Jekyll & Git Bash

Learn how to take your job search to the next level by hosting and formatting your resume for free using Markdown, Jekyll, and GitHub Pages. Check out the [example page](https://www.galbrame.github.io) to see what your resume could look like! This README will also endeavour to impart some general principles of technical writing (from the perspective of Andrew Etter in _[Modern Technical Writing](https://www.amazon.ca/Modern-Technical-Writing-Introduction-Documentation-ebook/dp/B01A2QL9SS)_) that you can employ in your own projects.

Hosting your own site won't just show off your resume to potential employers - it will show off your technical skills. As Etter extolls, writing webpages in html and xml is onerous at best, at best. Displaying your ability to create a webpage using modern tools like a static site generator and highly adaptable lightweight markup language will set you apart from other candidates. 


## PREREQUISITES
For this project, you will need:
* A resume that is already formatted in Markdown
  * Preferably GitHub Flavoured Markdown (GFM) to take advantage of the extended features
  * If you aren't familiar with Markdown, see [More Resources](#more-resources) for a good tutorial and GFM reference
* A Markdown editor (see [More Resources](#more-resources) for some suggestions)
* A GitHub account
* Jekyll<sup>[1](#notes)</sup> (or an alternative static site generator)
* Ruby<sup>[2](#notes)</sup> (version 2.5.0 or higher)
* Git Bash


## STEPS

### Step 1: Creating The GitHub Repository

1) We want our resume to be the landing page for our GitHub Pages account, so we'll need to make a new repository. After logging into GitHub, click on the "+" sign at the top right of the page. The "+" can be found on any GitHub page. Select "New repository" from the dropdown menu.

    ![new repository dropdown menu](/images/newRepo.png)

2) Select the account you would like your resume associated with under the **Owner** dropdown.

3) In the repository name, type ```<user>.github.io```, where ```<user>``` is your username.

4) Leave the description blank.

5) Leave the repository as Public so that anyone will be able to find your new digital resume.

6) Don't tick any of the initialize option checkboxes, since we will be adding all of the files later.

![create new repository menu](/images/newRepo2.png)


### Step 2: Creating the Local Repository

1) Create a folder on your computer where your site's source files will be stored.

2) Open Git Bash and navigate to the folder<sup>[3](#notes)</sup>. 

3) Initialize a local Git repository with the same name as the repository you made on GitHub, and change directory to the new repository.
   ```
   git init <username>.github.io
   cd <username>.github.io
   ```

5) We are going to use our gh-pages branch as our publishing source, so we will need to use checkout<sup>[4](#notes)</sup> to create and switch to that branch.
   ```git checkout --orphan gh-pages```

6) Create a new Jekyll site, using
   ```jekyll new --skip-bundle .```<sup>[5](#notes)</sup>.

7) Delete the ```_posts``` and ```about.markdown``` from your new repository folder. They will just add clutter to your final product. 

_NOTE_: Keep Git Bash open because you will use it again soon.


### Step 3: Prep Your Site for GitHub

1) Open the Gemfile. If you are comfortable with Vi or Emacs, you can do it right from Git Bash. Or you can open it with an editor, such as IntelliJ, Visual Studio, or Notepad++.

2) Find the line starting with ```gem "jekyll"``` and comment it out by adding "#" to the start of the line. 

3) Find the ```# gem "github-pages"``` line and uncomment it by deleting the "#".

4) Change the github-pages line to add the latest ```<version>``` of the github-pages gem ([listed here](https://pages.github.com/versions/)):
    ```
    gem "github-pages", "~> <version>", group : :jekyll_plugins
   ```

5) Save and close Gemfile.

6) Open ```index.markdown```.

7) Delete all of the content, then copy and paste your Markdown formatted resume into the file.

8) Save and close ```index.markdown```. This will be your site's homepage.

9) Return to Git Bash and run ```bundle install``` to create the proper Gem dependencies for your site.


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
![Megan's resume page](/images/resume.gif)

You should now have your resume hosted on its very own static website. Your url should be ```https://<username>.github.io```. Alternatively, you can find the url by going to your GitHub repository and going to Settings > Pages.


## OPTIONAL
### Customizing the Theme
GitHub offers 12 supported Jekyll themes, including the default "Minimal" that your site is already using. You can select a different theme through Settings > Pages > Change theme. Alternatively, many other unsupported themes can be found through search engines. These themes will have instructions on how to add them to your own site.

### Customizing _config.yml
There are several options for adding extra information to your site in this file, including site title, site description, and your GitHub username. If you would rather not have any of it, simply leave the tags empty. **Warning**: do not comment out any tags in the config file or your site will not render properly.


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

#### Why Markdown?
Markdown is a handy lightweight markup language with straightforward syntax. It is quickly and easily picked up and applied by nearly everyone and very human-readable. It is far easier and quicker to create a Markdown file and convert it to xml using Jekyll than it is to create something similar with html or xml. It's also one of the most popular lightweight markup languages, so choosing it over another lightweight markup language could be considered "future proofing" your material, as it is more likely to be supported for some time.
   

#### Why GitHub rather than Wordpress?
While both offer free versions of hosting, Wordpress is bloated with extraneous functionality that a lot of basic websites don't need. It is a large content management system (CMS), which requires varying degrees of maintenance and utilizes components that can crash. On the other hand, GitHub is a distributed version control system (DVCS). DVCSs, as Etter points out, are exemplary because they have better performance, can be used offline, and easily accommodate one file being worked on simultaneously by several people. Plus, developers prefer DVCSs, so you'll be showing off your knowledge of them. Besides being a better option to host your resume, you're also showing potential employers that you already understand the importance of DVCSs.


## NOTES
1) Windows is not officially supported by Jekyll, but it can be installed and run with careful "[tweaks](https://jekyllrb.com/docs/installation/windows/)."
2) Don't worry - you won't have to know or use any Ruby for this project. It is purely necessary to run Jekyll.
3) If any of the folders have a space in the name, you will need to put quotation marks around the folder name (double or single) or else Git Bash will perceive it as extra arguments. Alternatively, you can use a backslash before the space, such that ```New Folder``` would be ```New\ Folder```.
4) ```checkout``` is the git command for switching between branches in your repository.
5) The period at the end is important because it denotes the current directory. If you forget it, you will get "Error: You must specify a path."
