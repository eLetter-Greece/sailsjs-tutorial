# Chapter 1: Hit the ground running

## Setting up your environment
As I stated in the introduction setting up your development environment is something that makes even veteran developers squirm. Rather than explore how to setup a development environment, especially for those on Windows, I've opted to give you options that will work out of the box. However I recommend you at least attempt to setup your own environment in the future, upon completion of this tutorial. 

1. Register for [Cloud9](http://c9.io) or [Nitrous.io](http://nitrous.io). Both of these services offer free plans.
2. Setup a Node.js environment. This is the language Sails.js is written in. Either of these services will come stock with Node.js, NPM, and git. 
3. Install sails using the following command:

    $ npm install sails -g

## Crash course in the command line
Regardless of your background, the Unix command line is likely something you're not familiar with. If you're using one of the recommended services you'll have a Unix command line [shell](http://en.wikipedia.org/wiki/Shell_(computing)) setup with [Bash[(http://en.wikipedia.org/wiki/Bash_(Unix_shell)) and available in the bottom of the screen.

The command line is conceptually simple. By issuing short commands, users can perform a large number of action, such as creating directories (mkdir), moving and copying files (mv and cp), and navigating the filesystem by changing directories (cd). The command line may seem primitive to users mainly familiar with graphical user interfaces (GUIs), however, the command line is one of the most powerful tools in the developer’s toolbox.

The command line is a complex topic that deserves a tutorial of it's own, but for this book we will need only a few of the most common Unix commands, listed in Table 1.1. For a more information about the Unix command line, see [Conquering the Command Line](http://conqueringthecommandline.com/) by Mark Bates (available as a [free online version](http://conqueringthecommandline.com/book) and as [ebooks and screencasts](http://conqueringthecommandline.com/#pricing)).

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

    $ sails new helloWorld
    info: Created a new Sails app `example`!

#! do you need to npm install at this point to sails lift?

    $ cd helloWorld

You can now see the home page of the app you've created by entering

    $ sails lift

and going to `http://localhost:1337`.

## Sails file structure
Notice how many files and directories the `sails new` command creates. This standardized file structure is one of the many advantages of Sails. You immediately get a basic functional app, and because the file structure is the same between all Sails apps you can immediately understand where you are when dealing with someone else's code, and makes working with a team much easier, as you don't have to guess at where someone else would have put a particular file or function.

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

## NPM & Package.json
The [Node Package Manager](https://www.npmjs.org/) (NPM) is a package manager for Node.js. It runs through the `package.json` file and installs the necessary dependencies, while ensuring that all the needs of the dependencies are met.

Unless you specify a version number next to the package NPM will automatically install the latest version of the package published to the NPM registry.

There is also a way to specify versions of a package that include only minor or patching changes. `~1.0.0` for example will install any package up to, but not including `~1.1.0`.

## Model-View-Controller (MVC)
This early on it may be a bit difficult to understand, but it's good to get a high level view of the way Sails works. You may have noticed the standard Sails file structure includes an `api/` folder which contains a `models/` and `controllers/` as well as a separate folder for views. This should tip you off to the fact that Sails follows the [Model-View-Controller](http://en.wikipedia.org/wiki/Model-view-controller) pattern. This is used to separate "business logic" (the part of the program that determines how data is created, and used) from the input your application receives and what is shown to the user. In most web development "business logic" usually includes things like users or products. Sails has specifically designed to keep this separation high by being designed to build APIs for the consumption by other apps that serve as the view. For the sake of simplicity however, we will assume that our Sails app includes views within the app. 

When you interact with a Sails app your browser sends a request to a web server and passed to the Sails controller which dictates what happens next. Sometimes this will mean that a view is rendered immediately. This view is converted to HMTL and sent to the browser. Usually the controller interacts with a model which represents an object such as a user, as well as communicating with the database. At that point the data is sent back to the browser to be rendered in HTML.

## Hello world!
In this first example we'll make a very small change to the app, add a controller action to render the string "hello world!", rather than the default Sails.js homepage.

Controller actions are defined in controllers, as you can gather from their name. We'll call this action `hello` and place it in a brand new controller that we'll create, because as you'll notice, we don't currently have any controllers. You can verify that yourself by running this command:

    $ ls api/controllers/

which will allow you to see a list of the current controllers. This action uses the `res.render` function which we'll discuss more in a chapter 2.

###### Adding a HelloController and `hello` action.
`api/controllers/HelloController.js`
```node
module.exports = {
  hello: function(req, res) {
    res.send("Hello world!");
  }
};
```
You'll also need to modify the routes in order to set this new action to your home page.

#! add in the defaulted sails commentary?
`config/routes.js`
```node
module.exports.routes = {
 '/': 'HelloController.hello' 
};
```

You can now test your changes by running `$ sails lift` again, and going to `http://localhost:1337`

## Version control with Git


## Deploying to Heroku

## Conclusion

## Practice!
