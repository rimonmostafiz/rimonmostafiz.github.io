# Oracle SQL Developer in Ubuntu


You will need a free Oracle account to log in and download SQL Developer from [Oracle Technology Network](http://www.oracle.com/technetwork/developer-tools/sql-developer/downloads/index.html) site. For ubuntu download the _Other Platforms_ version.<br>
At the time of writing this post, I download version is **sqldeveloper-17.2.0.188.1159-no-jre.zip.**
You will also need Java to run Oracle SQL developer. <br>

After download, I moved the download file to `/home/rimonmostafiz/Applications` (you can choose any other location you prefer).

Move the download file to `/home/rimonmostafiz/Applications`. you can choose any other location you prefer.

    $ sudo mv sqldeveloper-17.2.0.188.1159-no-jre.zip /home/rimonmostafiz/Applications
    $ cd /home/rimonmostafiz/Applications
    $ sudo unzip sqldeveloper-17.2.0.188.1159-no-jre.zip

Next link over an in-path launcher for Oracle SQL Developer

    $ sudo ln -s /home/rimonmostafiz/Applications/sqldeveloper/sqldeveloper.sh /bin/sqldeveloper
    $ sudo rm /usr/local/bin/sqldeveloper*.zip

Edit `/home/rimonmostafiz/Applications/sqldeveloper/sqldeveloper.sh` and replace it's content to:

    #!/bin/bash
    unset -v GNOME_DESKTOP_SESSION_ID
    cd /home/rimonmostafiz/Applications/sqldeveloper/sqldeveloper/bin
    ./sqldeveloper "$@"

If `./sqldeveloper` permission denied error occurs
Try this

    #!/bin/bash
    unset -v GNOME_DESKTOP_SESSION_ID
    cd /home/rimonmostafiz/Applications/sqldeveloper/sqldeveloper/bin && bash sqldeveloper $*

Now run sql developer by typing command

    $ sqldeveloper

> Note: When you run Sql Developer at the first time, you need to specify the path of JDK's folder.
In my computer, JDK stored at `/home/rimonmostafiz/.sdkman/candidates/java/8u152`<br>
I prefer use SDKMAN to manage my different versions of java. You can read details about SDKMAN from My [Manage JDK using SDKMAN](http://rimonmostafiz.com/post/manage-jdk-using-sdkman/) post.**

Now we can create a desktop application for easy to use:


    $ cd /usr/share/applications/
    $ sudo vim sqldeveloper.desktop

then add the following lines to the file

    [Desktop Entry]
    Exec=sqldeveloper
    Terminal=false
    StartupNotify=true
    Categories=GNOME;Oracle;
    Type=Application
    Icon=/home/rimonmostafiz/Applications/sqldeveloper/icon.png
    Name=Oracle SQL Developer

Finally run

    $ sudo update-desktop-database

Now you will find Oracle SQL Developer in your app launcher.

  * Ubuntu Verson: `16.04 LTS`
  * JDK Verison: `1.8`
  * SQL Developer Version:  `sqldeveloper-17.2.0.188.1159-no-jre.zip`

