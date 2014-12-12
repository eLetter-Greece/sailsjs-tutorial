# Chapter 1: Hit the ground running

## Setting up your environment
As I stated in the introduction setting up your development environment
is something that makes even veteran developers squirm. Rather than
explore how to setup a development environment, especially for those on
Windows, I've opted to give you options that will work out of the box.
However I recommend you at least attempt to setup your own environment
in the future, upon completion of this tutorial. 

1. Register for [Cloud9](http://c9.io) or 
[Nitrous.io](http://nitrous.io). Both of these services offer free 
plans.
2. Setup a Node.js environment. This is the language Sails.js is written
in. Either of these services will come stock with Node.js, NPM, and git. 
3. Install sails using the following command:

    $ npm install sails -g

## Crash course in the command line
Regardless of your background, the Unix command line is likely something
you're not familiar with. If you're using one of the recommended
services you'll have a Unix command line
[shell](http://en.wikipedia.org/wiki/Shell_(computing)) setup with
[Bash[(http://en.wikipedia.org/wiki/Bash_(Unix_shell)) and available in
the bottom of the screen.

The command line is conceptually simple. By issuing short commands,
users can perform a large number of action, such as creating directories
(mkdir), moving and copying files (mv and cp), and navigating the
filesystem by changing directories (cd). The command line may seem
primitive to users mainly familiar with graphical user interfaces (GUIs)
however, the command line is one of the most powerful tools in the
developer’s toolbox.

The command line is a complex topic that deserves a tutorial of it's
own, but for this book we will need only a few of the most common Unix
commands, listed in Table 1.1. For a more information about the Unix
command line, see [Conquering the Command
Line](http://conqueringthecommandline.com/) by Mark Bates (available as
a [free online version](http://conqueringthecommandline.com/book) and as
[ebooks and screencasts](http://conqueringthecommandline.com/#pricing)).

###### Table 1.1
Description | Command | Example
----------- | ------- | -------
list contents | ls | # ls -l
make directory | mkdir <dirname> | mkdir myStuff
change directory | cd <dirname> | cd myStuff
cd up one | | cd ..
cd home | | cd ~
cd path to incl. home dir | | cd ~/mystuff/
move file (rename) | mv <source> <target> | mv README.txt README.md
copy file | cp <source> <target> | cp README.txt README.md
remove file | rm <file> | rm README.txt
remove empty directory | rmdir <directory> | rmdir myStuff
remove non-empty directory | rm -rf <directory> | rm -rf ./myStuff
concatenate & display file contents | cat <file> | cat README.md

## Your first app
Now we create your first Sails.js app using the command line. 

```
$ sails new helloWorld
info: Created a new Sails app `example`!
```

#! do you need to npm install at this point to sails lift?

```
$ cd helloWorld
```

You can now see the home page of the app you've created by entering

```
$ sails lift
```

and going to `http://localhost:1337`.

## Sails file structure
Notice how many files and directories the `sails new` command creates.
This standardized file structure is one of the many advantages of Sails.
You immediately get a basic functional app, and because the file
structure is the same between all Sails apps you can immediately
understand where you are when dealing with someone else's code, and
makes working with a team much easier, as you don't have to guess at
where someone else would have put a particular file or function.

```
helloWorld/
  -- config/
  -- views/
  -- api/
    -- models/
    -- controllers/
    -- policies/
    -- responses/
    -- services/
  -- tasks/
  -- assets/
    -- images/
    -- js/
    -- styles/
  README.md
  .gitignore
  package.json
  .sailsrc
  app.js
  Gruntfile.js
```

## NPM & Package.json
The [Node Package Manager](https://www.npmjs.org/) (NPM) is a package
manager for Node.js. It runs through the `package.json` file and
installs the necessary dependencies, while ensuring that all the needs
of the dependencies are met.

Unless you specify a version number next to the package NPM will
automatically install the latest version of the package published to the
NPM registry.

There is also a way to specify versions of a package that include only
minor or patching changes. `~1.0.0` for example will install any package
up to, but not including `~1.1.0`.

## Model-View-Controller (MVC)
This early on it may be a bit difficult to understand, but it's good to
get a high level view of the way Sails works. You may have noticed the
standard Sails file structure includes an `api/` folder which contains a
`models/` and `controllers/` as well as a separate folder for views.
This should tip you off to the fact that Sails follows the
[Model-View-Controller](http://en.wikipedia.org/wiki/Model-view-controller)
pattern. This is used to separate "business logic" (the part of the
program that determines how data is created, and used) from the input
your application receives and what is shown to the user. In most web
development "business logic" usually includes things like users or
products. Sails has specifically designed to keep this separation high
by being designed to build APIs for the consumption by other apps that
serve as the view. For the sake of simplicity however, we will assume
that our Sails app includes views within the app. 

When you interact with a Sails app your browser sends a request to a web
server and passed to the Sails controller which dictates what happens
next. Sometimes this will mean that a view is rendered immediately. This
view is converted to HMTL and sent to the browser. Usually the
controller interacts with a model which represents an object such as a
user, as well as communicating with the database. At that point the data
is sent back to the browser to be rendered in HTML.

## Hello world!
In this first example we'll make a very small change to the app, add a
controller action to render the string "hello world!", rather than the
default Sails.js homepage.

Controller actions are defined in controllers, as you can gather from
their name. We'll call this action `hello` and place it in a brand new
controller that we'll create, because as you'll notice, we don't
currently have any controllers. You can verify that yourself by running
this command:

```
$ ls api/controllers/
```

which will allow you to see a list of the current controllers. This
action uses the `res.render` function which we'll discuss more in a
chapter 2.

###### Adding a HelloController and `hello` action.
`api/controllers/HelloController.js`
```node
module.exports = {
  hello: function(req, res) {
    res.send("Hello world!");
  }
};
```

In order to you'll also need to modify the routes in order to set this
new action to your home page. To do this we'll need to edit Sails'
router. The router sits in front of the controllers, and determines
which controllers to send requests to. We want to change the root route,
which determines what is displayed at the root URL. (It's called the
root URL because it's the URL for a website which contains nothing after
the first forward slash. For example http://example.com/ would be a root
URL.)

`config/routes.js`
```node
.
.
.
module.exports.routes = {
.
.
.
 '/': 'HelloController.hello' 
.
.
.
};
```

You can now test your changes by running `$ sails lift` again, and going
to `http://localhost:1337`.

## Version control with Git
Now that we have the a working Sails app we're going to put our code
under version control. For this particular app it may be overkill, but
when you're dealing with an app of any complexity or importance you'll
want to put your code under version control. Version control is used to
track changes in the code, collaborate, and roll back to reverse any
unintentional errors created as you are creating new features, or
deleting old files. Version control is an essential skill for every
developer.

The most commonly used version control system is
[Git](http://git-scm.com/). Git is another large, complex topic. If
you'd like to dive deeper into Git check out the free book [Pro 
Git](http://git-scm.com/book/en/v2).

Git comes installed on either of the cloud services, and most Unix
operating systems, but if you need to install Git [go
here](http://git-scm.com/book/en/v2/Getting-Started-Installing-Git).

### Setting up Git
Before we get going with Git it's important to set it up. Because these
are system setups you only need to do them once per computer.

```
$ git config --global user.name "Your Name"
$ git config --global user.email yourEmail@example.com
$ git config --global push.default matching
$ git config --global alias.co checkout
$ git config --global alias.ci commit
$ git config --global alias.br branch
$ git config --global alias.st status
```

The name and email address you specify in your global Git config will be
included in any repositories you make public. The first two are the only
ones required for this tutorial. The third line ensures
forward-compatibility, and the fourth line is simply for convenience,
allowing you to use the command `git checkout` with `git co`. 

### New repos
When starting a new project you'll need to create a new repository (repo
for short). Navigate to the root of the new project and intialize the
new repo using the following commands:

```
$ git init
Initialized empty Git repository in /home/helloWorld/.git/
```

Next we're going to add all of the files to the repo using:

```
$ git add -A
```

This adds all files in the current directory, barring those that match
patterns included in the `.gitignore` file, which specifies files you
don't want to be included in teh repo. The `sails new` command
automatically generates a `.gitignore` file with sane defaults for a
Sails project, but you can add new ones if you'd like.

When you add files they're first placed in a staging area, that has all
of your pending code changes. You can check which files are in the
staging area using the `git status` command.

```
$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

  new file:   .editorconfig
  new file:   .gitignore
  new file:   .sailsrc
  new file:   Gruntfile.js
  new file:   README.md
  .
  .
  .
```

In order to keep the changes that you just made you can use the `commit`
command, as shown below:

```
git commit -m 'Initial commit'
[master (root-commit) 7a21161] Initial commit
.
.
.
```

The `-m` flag allows you to add a message to your commit on the command
line with your commit, otherwise your system's default editor will be
opened up and you will be prompted to enter your commit message there.
Note that commit messages are used to tell your future self and others
what exactly you did. As such more descriptive commit messages are
always preferable to generic ones like "fixed bug". For commit's other
than your intial commit I recommend that you use your system's editor,
and follow the guidelines outlined below, borrowed and slightly modified
from [Tim
Pope](http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)
and Torvald's [Linux commit
guides](https://www.kernel.org/doc/Documentation/SubmittingPatches). 
My chief omission here is not limiting each line to 72 characters or
less, however because you'll be using Github or Bitbucket's web
interface this particular piece of advice is less necessary, though
still valuable to follow.

```
Capitalized, short (~50 chars or less) summary

A more detailed explanatory text, if necessary. The blank line
separating the the summary from the body is critical if you have the
body. Tools like rebase can get confused if you run the two lines
together. 

Write your commit message in the imperative: "Fix bug" and not "Fixed
bug" or "Fixes bug."  This convention matches up with commit messages
generated by commands like git merge and git revert.

Further paragraphs come after blank lines.

- Bullet points are okay, too

- Typically a hyphen or asterisk is used for the bullet, followed by a
  single space, with blank lines in between, but conventions vary here

- Use a hanging indent
```

Note that when you make a commit it is only recorded on your computer
until you utilize the push command. This is called storing the commits
(changes) locally. We'll go over using a remote reposistory (one not on
your local machine) later.

You can see a list of all previous commit messages using the Git `log`
command.

```
$ git log
commit 7a21161777161e42ad5e255e2e72c8f9217330ed
Author: Britton Broderick <britton.jb@gmail.com>
Date:   Mon Nov 17 08:59:32 2014 -0700

    Initial commit
```

If your repo's log is long enough to require scrolling to see all of it
you have to type `q` to exit the log.

### So... why Git?
Right now it's probably still not exactly clear why you should use Git
if you haven't used it before. To illustrate exactly why let's go
through two different scenarios, one a bit of an extreme example.
Suppose you're building your app and accidentally delete the controllers
directory.

```
$ rm -rf api/controllers/
```

Using the `rm -rf` command tells the system that you would like to
remove the following files and directories and the `-rf` flag tells you
to remove each file and directory under the targeted folder without
asking for confirmation.

We're able to see the the damage done using the `git status` command:

```
$ git status
On branch master
Changes not staged for commit:
  (use "git add/rm <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

  deleted:    api/controllers/.gitkeep
  deleted:    api/controllers/HelloController.js

no changes added to commit (use "git add" and/or "git commit -a")
```

We can now see that these flies have been deleted, but currently they
are on the "working tree" because the changes haven't been commited yet.

Without Git you would be panicking at this point, and crying distraught
tears because you just wiped out all of the work you (and your team)
have been doing. This is where Git saves the day. You can now undo these
changes using the `checkout` command with the force flag `-f`.

```
$ git checkout -f
$ git status
On branch master
nothing to commit (working directory clean)
```

You can verify this undid the damage by running the command:

    $ ls api/

And seeing the files and directories are back where they belong.

### Github & Bitbucket
Now that we're using Git, we need to push our code to remote repo. To do
this wee need to setup a remote Git repo. To do this we recommend using
either Github or Bitbucket, which are the two most popular services for
remote Git repos.

The differences between these two services are small, but significant.
Github allows for unlimited free public repos, but Bitbucket allows for
unlimited private repos, with a limited number of contributors. As well
as both having differences in the UI.

In practice if you're building an app for commercial purposes I'd
recommend using Bitbucket, but if you're building an open source
project, or attempting to build a portfolio of apps I would recommend
using Github.

The reason for using one of these services is two-fold. First it allows
you to have a backup of your code, so if you lose all the data on your
hard drive you won't lose your whole project. Also, it makes it much
easier to work with a team.

Getting started with either of these services is easy.

1. Sign up for an account.
2. Copy your [public 
key](https://en.wikipedia.org/wiki/Public-key_cryptography), as show
below.

```
$ cat ~/.ssh/id_rsa.pub
```

3. Add your public key to your account by going into your account
settings and then the **SSH KEY** section.
4. Create a new repo called helloApp.
5. Add the remote repo, and push to the remote repo.

```
$ git remote add origin git@<service domain>:<username>/helloApp.git
$ git push -u origin --all
```

The command `push -u origin -all` tells Git to send all of the changes
you've commited to your local repo to the remote repo called `origin`
which in this case represents Github or Bitbucket. The `--all` option
tells Git to send all of the *branches* that you've commited. We'll go
over branches later in the book.

Of course, you shoudl have replaced <username> and <service domain> with
your username and the domain of the service you're using. For example I
could run either of the following:

```
$ git remote add origin git@github.com:britton-jb/helloApp.git
$ git remote add origin git@bitbucket.org:brittonjb/helloApp.git
```

### Git workflow
In this section we'll make some changes to the README to showcase the
preferred Git workflow style.

Branching is a key part of the Git workflow. It allows us to make a copy
of the repo we're working on where we can make the changes we need
without changing the primary code base. Most of the time the *master*
branch is the primary branch, from which we can create a new topic
specific branch to deal with a new bug, feature, or simple experiment
using the checkout command and the `-b` flag.

```
$ git checkout -b update-README
Switched to a new branch 'update-README'
$ git branch
  master
* update-README
```

In the above example the `branch` command lists all of the local
branches and the asterisk lets you know which branch you're on at the
moment. The `git checkout -b update-README` command creates a new branch
and switches to it.

After creating your new topic branch we'll edit the README.md to include
a better description of your project, as show below:

```
# Sails.js Tutorial: "Hello world"

I've completed the first exercise of the [*Sails.js
Tutorial*](https://github.com/britton-jb/sailsjs-tutorial) by Britton
Broderick.
```

Now we're going to commit the changes that we've made to our branch. We can do that using a shortcut on the git commit command as shown.

```
$ git commit -a -m "Update the README"
[master 7f23826] Update the README
 1 file changed, 2 insertions(+), 2 deletions(-)
```

In case you missed it the `-a` flag adds all files you'ved modified
since the last commit and adds them to that commit. It's worth noting
that this only adds existing files that have been modified, not newly
added files to your commit.

As an aside, when you're writing commit messages you should ensure that
you always use the present tense. Because each git commit is a patch, it
makes more sense to tell readers what each patch does, rather than what
it did. For reference [here's an article on writing great commit
messages](https://github.com/blog/926-shiny-new-commit-styles).

Now that we've made the changes we wanted to make, we can merge this
topic branch back into the master branch.

```
$ git checkout master
Switched to branch 'master'
$ git merge update-README
Updating 7f23826..d679903
Fast-forward
 README.md | 4 ++--
 1 file changed, 2 insertion(+), 2 deletion(-)
```

You may have noticed that Git output usually includes random strings
like `7f23826`. These are related to how Git represents repos. Your
results will be different, but should be essentially the same despite
that.

As a matter of good house keeping once you've merged in changes from a
branch you should delete the the branch.

``` 
$ git branch -d update-README
Deleted branch update-README (was 7f23826).
```

Now that you've updated the `README` it's time to push the changes to
see the result. Now that you've done an intial commit you can omit
`origin master`, and simply `git push`.

## Deploying to Heroku
We're now going to take an action that at this stage would realistically
be pointless, but is good exercise to learn how to deploy, and get your
app into a *production* environment. The other thing to note here is
that it prevents issues with differences between development and
production to deploy early and often.

Deploying a Sails app is easy. There are a number of different options
available, but my favorite at this point is
[Heroku](http://heroku.com/). Heroku is a platform built to make
deploying web apps easy, as long as you're using Git.

If you're using one of the cloud based development environments it's
likely that Heroku's Toolbelt is already installed. If not you can find
instructions to set it up [here](https://toolbelt.heroku.com/).

To test if Heroku is installed run the command

```
$ heroku version
```

Next sign up for an account at Heroku. Once that is taken care of you'll
need to use the Heroku command line tools to login and use your SSH key.

```
$ heroku login
$ heroku keys:add
```

Now that you're logged in you'll need to create a place in the Heroku
servers for your app to live.

```
$ heroku create
Creating rocky-oasis-2464... done, stack is cedar-14
https://rocky-oasis-2464.herokuapp.com/ | git@heroku.com:rocky-oasis-2464.git
Git remote heroku added
```

Now that you've added the place for your app to live you can push your app.

```
$ git push heroku master
```

At this point you may see the different logging messages, and warnings.
You can likely safely ignore these. Once you see that the app has been
launched and deployed you can see your creation by going to the URL
output when you ran `heroku create`.

It will look exactly like it did running locally, but it's now in a live
production environment.

If you'd like to dive deeper into Heroku there are a number of other
[commands avaiable](http://devcenter.heroku.com/heroku-command) via the
Toolbelt.

## Conclusion
At this point you have done a lot. It's my hope that I've explained
things so far in such a way that you're not overwhemled. You should have
learned the following, how to setup your development environment,
version control with Git, and how to deploy an app to Heroku. In this
next chapter we'll make a toy app that interacts with a database, which
will give you a better feel of what's possible using Sails.

If you'd like to share how far you've come, send a tweet or Facebook
post with something like: 

I'm learning Sails.js with the 

#! I need a domain, and twitter stuff

I also recommend signing up for our email list.

### What you learned
* Sails.js is a web development framwork written in JavaScript.
* Installing Sails, generating an app, and editing the files is easy
  using your cloud development environment.
* Sails comes with a command-line command called `sails` that can
  generate new applications and run your server locally.
* We added a controller, controller action, and changed the root route
  to "hello world".
* We have taken steps to prevent loss of our code and laid the
  foundation for others to be able to work with us on projects using Git
  and Github.
* We've deployed our app to a production environment using Heroku.

## Practice!
1. Change the content of the `hello` action to "hola, mundo!" instead of
  "hello world".
2. Using the `hello` action add another action called `goodbye` that
  sends the text "goodbye, world!". Then edit the routes file to change
  the root route to the `goodbye` action, rather than the `hello`.
