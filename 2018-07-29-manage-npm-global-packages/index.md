# Manage npm Global Packages

This post is about how can we install, update, uninstall and list out installed global packages of NPM.

The commands that start with `$` are meant to be run in the terminal or command line.<br>
The output of the command will follow immediately. <br>
Comments will begin with `#`.

### Install Global Packages

    $ npm install -g <package>

For example, to install express globally, type

    $ npm install -g express
    + express@4.16.3
    added 50 packages from 47 contributors in 10.433s

### Update Global Packages

    $ npm update -g <package>

For example, to update `express` globally type

    $ npm update -g express

To find out which packages need to be updated, type

    $ npm outdated -g --depth=0
    Package  Current  Wanted  Latest  Location
    nodemon   1.18.2  1.18.3  1.18.3
    npm        6.1.0   6.2.0   6.2.0

To update all global packages, type

    $ npm update -g

### List All Installed Global Packages

    $ npm list -g --depth 0
    /home/rimonmostafiz/.nvm/versions/node/v10.6.0/lib
    ├── express@4.16.3
    ├── nodemon@1.18.2
    └── npm@6.1.0

* `list -g`: display a tree of every package found in the user's folder(without the `-g` option it only shows the cureent directory's packages)
* `--depth 0 OR --depth=0`: to avoid including every package's dependencies in the tree view

### Uninstall Global Packages

    $ npm uninstall -g <package>

For example, uninstall `express` globally

    $ npm uninstall -g express
    removed 50 packages in 0.289s

