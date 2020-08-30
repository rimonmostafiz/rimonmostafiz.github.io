# Install and Manage Node JS Using NVM

Node Version Manager (NVM) is a simple bash script to manage multiple active node.js versions.

## Install NVM
To install or update nvm, you can use the install script using cURL or Wget

    $ curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash
    $ wget -qO- https://raw.githubusercontent.com/creationix/nvm/v0.33.11/install.sh | bash

The script clones the nvm repository to `~/.nvm` and adds the source line to your profile (`~/.bash_profile`, `~/.zshrc`,`~/.profile`, or `~/.bashrc`).

    export NVM_DIR="$HOME/.nvm"
    [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm

### Verify installation
To verify that nvm has been installed, do:

    $ command -v nvm

which should output `nvm` if the installation was successful.

Please note that will`which nvm` not work, since `nvm` is a sourced shell function, not an executable binary.
After running the install script, if you get `nvm: command not found` or see no feedback from your terminal, simply close your current terminal, open a new terminal, and try verifying again.


## Usage
With `nvm` installed, you can install isolated Node.js versions. For information about the versions of Node.js that are available, type:

    $ nvm ls-remote

Which will give you something like

     ...
     v8.0.0
     v8.1.0
     v8.1.1
     v8.1.2
     v8.1.3
     v8.1.4
     v8.2.0
     v8.2.1
     v8.3.0
     v8.4.0
     v8.5.0
     v8.6.0
     v8.7.0
     v8.8.0
     v8.8.1
     v8.9.0   (LTS: Carbon)
     v8.9.1   (LTS: Carbon)
     v8.9.2   (LTS: Carbon)
     v8.9.3   (LTS: Carbon)
     v8.9.4   (LTS: Carbon)
    v8.10.0   (LTS: Carbon)
    v8.11.0   (LTS: Carbon)
    v8.11.1   (LTS: Carbon)
    v8.11.2   (LTS: Carbon)
    v8.11.3   (Latest LTS: Carbon)
     v9.0.0
     v9.1.0
     v9.2.0
     v9.2.1
     v9.3.0
     v9.4.0
     v9.5.0
     v9.6.0
     v9.6.1
     v9.7.0
     v9.7.1
     v9.8.0
     v9.9.0
    v9.10.0
    v9.10.1
    v9.11.0
    v9.11.1
    v9.11.2
    v10.0.0
    v10.1.0
    v10.2.0
    v10.2.1
    v10.3.0
    v10.4.0
    v10.4.1
    v10.5.0
    v10.6.0

As you can see, at the time of writing this article the current LTS version of `node` is `v8.11.3`. You can install that by typing:

    $ nvm install 8.11.3

Usually, `nvm` will switch to use the most recently installed version. You can tell `nvm` to use the version you just downloaded by typing:

    $ nvm use 8.11.3

To download, compile, and install the latest release of node, You can simply do this:

    $ nvm install node

And then in any new shell just use the installed version:

    $ nvm use node

Or you can just run it:

    $ nvm run node --version

Or, you can run any arbitrary command in a sub shell with the desired version of node:

    $ nvm 4.2 node --version

When you install Node.js using `nvm`, the executable is called `node`. You can see the version currently being used by the shell by typing:

    $ node -v

If you have multiple Node.js versions, you can see what is installed by typing:

    $ node ls

If you wish to default one of the versions, type:

    $ nvm alias default 8.11.3

This version will be automatically selected when a new session spawns. You can also reference it by the alias like this:

    $ nvm use default

Each version of Node.js will keep track of its own packages and has `npm` available to manage these.

You can have `npm` install packages to the Node.js project's `./node_modules` directory. Use the following syntax to install the `express` module:

    $ npm install express

If you'd like to install the module globally, making it available to other projects using the same version of Node.js, you can add the `-g` flag:

    $ npm install -g express

This will install the package in:

    ~/.nvm/versions/node/node_version/lib/node_modules/express

Installing the module globally will let you run the commands from the command line, but you'll have to link the package into your local sphere to require it from within a program:


    $ npm link express

You can learn more about the options available to you with nvm by typing:

    $ nvm help

## Removing Node.js
To uninstall a version of Node.js that you have enabled using `nvm`, first determine whether or not the version you would like to remove is the currently active version:

    $ nvm current

If the version you are targeting is **not** the currently active version, you can run:

    $ nvm uninstall node_version

This command will uninstall the selected version of Node.js.

If the version you would like to remove **is** the currently active version, you must first deactivate `nvm` to enable your changes:

    $ nvm deactivate

You can now uninstall the current version using the uninstall command above, which will remove all files associated with the targeted version of Node.js except the cached files that can be used for re-installment.

## Manual Uninstall
To remove nvm manually, execute the following:

    $ rm -rf "$NVM_DIR"

Edit `~/.bashrc` (or other shell resource configuration) and remove the lines below:

    export NVM_DIR="$HOME/.nvm"
    [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
    [[ -r $NVM_DIR/bash_completion ]] && \. $NVM_DIR/bash_completion

