# Google Drive in Ubuntu


At the time of writing, there is no official Google Drive client for Ubuntu or Linux Mint but if you need to use it then there is an unofficial client called **_Grive2_**. <br>
Grive is a Google Drive client for GNU/Linux systems. It allows the synchronization of all your files on the cloud with a directory of your choice and the upload of new files to Google Drive.

Those of you used Google Drive client on Windows or Mac, Grive2 will do the same for you in Ubuntu or Linux Mint.

To install Grive2 in Ubuntu, Linux Mint and derivatives by using the main _WebUpd8 PPA_, use the following commands:


    $ sudo add-apt-repository ppa:nilarimogard/webupd8
    $ sudo apt-get update
    $ sudo apt-get install grive

**Step 1:** <br>
Grive2 will download/upload new or changed files from the directory you run it. You can name it anything you want to. Let’s create a new folder – I'll create it on my `/home/rimonmostafiz` folder and going to name it **_GoogleDrive_**

    $ mkdir -p ~/GoogleDrive

**Step 2:** <br>
Next, navigate using the terminal into the newly created “GoogleDrive” folder:

    $ cd ~/GoogleDrive

**Step 3:** <br>
The first time you run Grive2, you must use the `-a` argument to grant it permission to access your Google Drive:

    grive -a

After running the command above, an URL should be displayed in the terminal.
Copy that URL and paste it in a web browser. In the newly loaded page, you’ll be asked to give Grive permission to access your Google Drive and after clicking **Allow access**, an authentication code will be displayed. Copy that code and paste it in the terminal where you ran Grive2.

That’s it. Grive 2 Will start syncing your files and folder from Google Drive, wait for sync to complete for the first time. Don't close the terminal.

Now each time you want to sync Google Drive with your local `GoogleDrive` folder, navigate to the `GoogleDrive` folder and run grive (this time without `-a` since you’ve already authenticated Grive with Google Drive).

If you want to sync only one sub-folder (a folder from your `~/GoogleDrive` directory) with Google Drive, use:

    $ grive -s folder
    # replace folder with the name of the sub-folder you want to sync

To see all the available options, type:

    grive --help

**_Courtesy:_** [_askubuntu.com_](http://askubuntu.com/)

