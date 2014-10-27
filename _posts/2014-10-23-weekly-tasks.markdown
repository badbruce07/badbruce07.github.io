---
layout: post
baseurl: /badbruce07.github.io/
title:  "Harvest - Learning to Make a Pull request on Github"
date:   2014-10-23 12:27:54
categories: jekyll update
---

On Thursday October 23, 2014, I worked on using github to learn how to remove files from another repository. In other words HarvestAPI.
Since I have made many changes in creating an improved HarvestAPI, the owner of the original version was Varun Baker aka varunity on 
GitHub. In order to make a pull request, I had to first `fork` and then `pull`.

<b> About Pull Requests </b>

Pull requests let you tell others about changes you've pushed to a GitHub repository. 
Once a pull request is sent, interested parties can review the set of changes, discuss potential modifications, 
and even push follow-up commits if necessary.
This guide walks through the process of sending a hypothetical pull request and using the various code review 
and management tools to take the change to completion.

So at first I had to clone the HarvestAPI repository and then in the terminal, I typed the command:
{% highlight ruby %}
git clone https://github.com/badbruce07/HarvestAPI.git
{% endhighlight%}

This would therefore download all of HarvestAPI content to any directory you wish to work from. Then you open the directory of HarvestAPI 
simply by typing `cd <Directory>` in the terminal.
<br>
After I've entered the directory path, I type in the terminal:

{% highlight ruby %}
git checkout gh-pages
{% endhighlight%}
This would allow me to navigate through the gh-pages branch. 

<b> About git checkout </b>

The git checkout command lets you navigate between the branches created by git branch. 
Checking out a branch updates the files in the working directory to match the version stored in that branch, 
and it tells Git to record all new commits on that branch. Think of it as a way to select which line of development 
you’re working on.

In the previous module, we saw how git checkout can be used to view old commits. 
Checking out branches is similar in that the working directory is updated to match the selected branch/revision; 
however, new changes are saved in the project history—that is, it’s not a read-only operation.

<b> Removing Content From the gh-pages Branch </b>

In order to remove content from the gh-pages branch, I had to use the command:
{% highlight ruby %}
git rm -r *
{% endhighlight%}
This is due to the fact that the existing content need to be replaced before adding the new information to the gh-pages branch
in the HarvestAPI repository. Then you can apply the command to make the changes:
{% highlight ruby %}
git commit -m "Changes"
{% endhighlight%}

<b> Adding the new content to the repository </b> <br/>
You can copy your new files from the directory you were working on into the HarvestAPI folder. In adding all of the content to 
git you use the command:
{% highlight ruby %}
git add .
{% endhighlight%}
Then you will have to type the following command in making the changes:
{% highlight ruby %}
git commit -m "Adding Files"
{% endhighlight%}

Then you will have to apply a push to gh-pages. This therefore shows all the new content that will be pushed to github:
{% highlight ruby %}
git push origin gh-pages
{% endhighlight%}

The terminal will then ask for your github username and password to let the push proceed.

N.B. <br/>
Even tho the content is pushed to github, it will <b>NOT</b> be shown to the wider public since the original creator
hasn't accepted the pull request. Varunity would have to accept it for the changes to be made.