This is the [nanoc](http://nanoc.ws/) tree used to generate the [UNC Computer Science Club Web site](http://csclub.cs.unc.edu/).
You can use [Bundler](http://gembundler.com/) to install the needed dependencies:

```sh
$ gem install bundler
$ bundle install
```

You can then build the site to the `output` directory by running:

```sh
$ bundle exec nanoc co
```

In order to view the site, run the following and point your browser at <http://127.0.0.1:3000/>:

```sh
$ bundle exec nanoc view
```

Note that pushes to the main GitHub repository trigger a server-side pull and rebuild of the site!
