# Introduction
Node.js has been sweeping the world of corporate development. Powering
names like Paypal, Netflix, Walmart, and IBM, it's clearly a technology
that allows for scalability, and offers the advantage of being able to
code in one language on the client and server. However, in it's current
state there is some question of how to best approach this new
technology. The aim of this book is to introduce this technology and
make it appraochable.

Sails.js is primarly designed for building real-time Application
Programming Interfaces (APIs), and in this book we will explore Sails
ability to make an API as well as views rendered on the server for the
sake of simplicity.

## Who is this book for?
This book was written to most approachable for those with some
experience in JavaScript or server side code in any languages. However
it's not meant to be for experts, or even those with some experience in
server side coding, unless the desire is specifically to gain experience
in the Sails framework. Despite all this, I'll make the best effort to
make this book approachable to those with no experience in writing code
of any kind.

## Prerequisities
As stated in the previous section, I'm working to make this book
approachable to any and all individuals, and as such no prerequsites are
strictly required. However, that said it's recommended that readers have
some experience in JavaScript, whether through
[Codecademy](http://www.codecademy.com/), or
[Eloquent JavaScript](http://eloquentjavascript.net/), however efforts
will be made to make this optional. As well, experience with the command
line and access to a Unix based development environment. Rather than
embark on the journey of showing Windows users how to setup such an
environment I recommend the use of a cloud based development
environement like [Nitrous.io](http://nitrous.io) or
[Cloud9](http://c9.io).

## Conventions in this book
Many examples in this book include use of the command line. Examples
will use a Unix-style command line prompt, with a dollar sign, as shown
below:

    $ echo "I'm learning Sails.js"

As discussed in the previous section I recommend that users in Windows
environments use a cloud based IDE such as 
[Nitrous.io](http://nitrous.io) or [Cloud9](http://c9.io).

This is useful because Sails.js comes with commands that must be run at
the command line.

We will use the the forward slash in file paths, the Unix convention for
directory separators.

    config/env/production.js

All file paths should be understood as relative to the application's
root.

This book will often include output from various programs. If what you
see doesn't match exactly don't worry. You may encounter errors not 
documented in this book. I encourage you to search for the error message
in various places such as [Google](http://google.com) or 
[Stack Overflow](http://stackoverflow.com) in order to help you solve 
the problem, which will lend itself greatly to your future development.

This tutorial will cover testing your application. Output from a failed
test will be indicated in RED, while output indicated a test passed will
be in GREEN.

Code will include syntax highlighting and previously written code will
be collapsed as indicated using the elipses below:

```node
#! Code with elipses
...
#! New code
```

## About the author
[Britton Broderick](www.linkedin.com/in/brittonbroderick/) is the author
of the [Sails.js
Tutorial](https://github.com/britton-jb/sailsjs-tutorial/),
and [Scaling Sails: MVP to
SOA](https://github.com/britton-jb/sails-tutorial-advanced.git)
His prior experience includes going to school for business at [Utah
Valley University](http://uvu.edu), realizing almost everything in
business could be automated and that we wanted to be the one to do it.
Adventures in learning to program followed.

## Acknowledgements

The inspiration for this book was [Michael
Hartl's](http://www.michaelhartl.com/) [Ruby on Rails
Tutorial](https://www.railstutorial.org/). I owe much to him for
allowing me to get into web development, and hope this tribute and
chance to pay it forward will do justice. Should you ever run into him
in your travels buy him a beer.

## License

    The MIT License

    Copyright (c) 2014 Britton Broderick 
 
    Permission is hereby granted, free of charge, to any person
    obtaining a copy of this software and associated documentation
    files (the "Software"), to deal in the Software without restriction,
    including without limitation the rights to use, copy, modify, merge,
    publish, distribute, sublicense, and/or sell copies of the Software,
    and to permit persons to whom the Software is furnished to do so,
    subject to the following conditions:
 
    The above copyright notice and this permission notice shall be
    included in all copies or substantial portions of the Software.
 
    THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND,
    EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
    MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
    NONINFRINGEMENT.  IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS
    BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN
    ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
    CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
    SOFTWARE.

    /*
     * -----------------------------------------------------------------
     * "THE BEERWARE LICENSE" (Revision 43):
     * Britton Broderick wrote this code. As long as you retain this
     * notice you can do whatever you want with this stuff. If we meet
     * some day, and you think this stuff is worth it, you can buy me a
     * beer in return.
     * -----------------------------------------------------------------
     */
