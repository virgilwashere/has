# has

`has` checks presence of various command line tools on the path and also reports their installed version

[![Build Status](https://travis-ci.org/kdabir/has.svg?branch=master)](https://travis-ci.org/kdabir/has)
[![Open Source Helpers](https://www.codetriage.com/kdabir/has/badges/users.svg)](https://www.codetriage.com/kdabir/has)


[![demo](demo.svg)](demo.svg)


## How ?

Download the `has` file. There is no dependency apart from `bash` itself 

    $ has node npm java git gradle 
    ✔ node 8.2.1
    ✔ npm 5.3.0
    ✔ java 1.8.0
    ✔ git 2.14.1
    ✔ gradle 4.0.1

If everything is good `has` exits with status code `0`. The status code 
reflects number of commands **not found** on your path.  

    $ has node go javac
    ✔ node 8.2.1
    ✔ go 1.8.3
    ✘ javac

And echo the status:

    $ echo $?
    1


## Installing

Just download the `has` script in your path. 

    git clone https://github.com/kdabir/has.git && cd has && make install


If you are lazy, you can run `has` directly off the internet as well:

    curl -sL https://git.io/_has | bash -s git node npm
    ✔ git 2.14.1
    ✔ node 8.2.1
    ✔ npm 5.3.0


And if that's too much of typing every time, setup an alias
    
    alias has="curl -sL https://git.io/_has | bash -s"

And use it

    $ has git
    ✔ git 2.14.1

## command not understood by has?

Let's say `$ has foobar` returns `foobar not understood`, because `has` may not have whitelisted `foobar`.

In such cases, pass `HAS_ALLOW_UNSAFE=y has foobar`. This is should still check for existance of `foobar` and tries to detect version as well.


## the `.hasrc` file

`has` looks for `.hasrc` file in the directory from where `has` command is issued. This file can contain commands that `has` 
will check for. List one command per line. Lines starting with `#` are treated as comments.


Following is example of `.hasrc` file:

```
# tools
git
curl

# interpreters
ruby
node
``` 

When `has` is run in dir containing this file, it produces:

```
$ has
✔ git 2.19.1
✔ curl 7.54.0
✔ ruby 2.3.1
✔ node 10.7.0
``` 

Also, CLI arguments passed to `has` are additive to `.hasrc` file. For example, in the same dir, if the following command is fired,
`has` checks for both commands passed from cli args and provided in `.hasrc` file.  

```
$ has java
✔ java 11.0.1
✔ git 2.19.1
✔ curl 7.54.0
✔ ruby 2.3.1
✔ node 10.7.0
```


*Pro Tip*: commit `.hasrc` file in root of your project. This can work as a quick check for confirming presence all command
line tools required to build and run your project.

on machines that don't even have `has` installed, your project's `.hasrc` is honored by this command: 

`curl -sL https://git.io/_has | bash -s` 

> take a look at .hasrc file of this repo

## Demo 

[![asciicast](https://asciinema.org/a/135790.png)](https://asciinema.org/a/135790)

## Contributing

[![Build Status](https://travis-ci.org/kdabir/has.svg?branch=has)](https://travis-ci.org/kdabir/has)


1. Star the repo, tweet about it, spread the word 
2. Update the documentation (i.e. the README file)
3. Adding support for more commands
4. Adding more features to `has`


## Adding Features

If you are contributing a feature, please ensure to check current tests. Add test cases for your feature. Tests are
executed using excellent [bats](https://github.com/bats-core/bats-core) testing framework. Add tests and run `make test`
   

## ♥
