This is the [nanoc](http://nanoc.stoneship.org/) tree used to generate the [UNC
Computer Science Club Web site](http://csclub.cs.unc.edu/).  In order to build
successfully, the following additional Ruby packages are required:

* [Haml](http://haml-lang.com/) and [Sass](http://sass-lang.com/) 3.1 or later
* [kramdown](http://kramdown.rubyforge.org/)

To build, use `rake`; the generated output will be placed in a new directory
named `output`.  Note that pushes to the main GitHub repository will trigger a
server-side pull and rebuild of the site!
