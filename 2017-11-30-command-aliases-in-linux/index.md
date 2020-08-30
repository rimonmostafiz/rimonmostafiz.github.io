# Command Aliases in Ubuntu Linux

## How to set up alias in Linux

Every time I need to see different projects logs from _application servers_ logs folder from different terminal window,  I have to go to Weblogic's logs folder and then open the log file using `less or tail -f project-name.log `

    cd /home/rimonmostafiz/Applications/Oracle/Middleware/Oracle_Home/user_projects/domains/base_domain/logs/
    less project-name.log or tail -f project-name.log

I don't want to write this long string Everytime, Wouldn’t it be easier to just type something like the following?

    logs
    less project-name.log


### Open your .bashrc file

Your _.bashrc_ file is located in your user directory. Open it in your favorite text editor. I like vim

    vim ~/.bashrc

Then go to the end of the file In vim you can

    Press        Shift + G (Will go to the last line of your file)
    Then Press   Shift + A (Will start appending after the last line)
    Then Press   Enter

### Add alias

Basic format of the alias is<br>
`alias aliasname='mycommand'`<br>
Note that there is no space between alias name and the EQUAL(=) and command

So my alias should be

    alias logs='cd /home/rimonmostafiz/Applications/Oracle/Middleware/Oracle_Home/user_projects/domains/base_domain/logs/'

### Chain Multiple Commands In alias

    alias logs='cd /home/rimonmostafiz/Applications/Oracle/Middleware/Oracle_Home/ && cd user_projects/domains/base_domain/logs/'

This && operator will run a set of commands and only continue to the next command if the previous one was successful.


### Write and Close .bashrc File

In vim, Press ESCAPE to get to normal mode and run the following command and press ENTER to write and quit:

    :wq

If you use any other editor, just save and close the file.

### Source .bashrc

    $source ~/.bashrc

Done, Now your alias should work.

### Another Cool Approach

So Isn't it be cooler If you could do something like this?

    less_logs project-name.log
    tail-f_logs project-name.log

Guess what, Yes you can do that :)
`alias` does not accept parameters but a function can be called just like an alias. For example:

### Function call like alias
I have added following functions in my .bashrc

    less_logs() {
        cd /home/rimonmostafiz/Applications/Oracle/Middleware/Oracle_Home/user_projects/domains/base_domain/logs/;
        less "$1";
    }

    tail_f_logs() {
        cd /home/rimonmostafiz/Applications/Oracle/Middleware/Oracle_Home/user_projects/domains/base_domain/logs/;
        tail -f "$1";
    }


That's it, It can save your time and increase your efficiency :)

