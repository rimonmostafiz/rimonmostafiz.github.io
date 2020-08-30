# Get Insulted by sudo

Do you know `sudo` can insult you? wait, what :question: :confused:

Take a look at what I'm talking about. `sudo` can insult you for typing incorrect password. :boom:

![sudo-insults](/images/sudo-insults.gif)

### Enable insults in `sudo`
Open a terminal and type:

    $ sudo visudo

This should open the configuration file in your default editor. In ubuntu like distros, it will be opened in `nano`.

Now you will have to find the section where the defaults are listed. <br>
Most probably you will find it at the top. Add following line to the section

    Defaults insults

Now save the file. If you are using `nano` then use `Ctrl+X` to leave the editor. At the time of quitting, it will ask you if you want to save the changes. To keep the changes, press `Y` and Then `Enter`.

![visudo](/images/visudo.gif)

Once you have saved the file you need to clear the old password from `sudo`’s memory by typing

    $ sudo -k


> NOTE: Always use `visudo` as it has a self-check system which will save you from messing up things.

To me, this little tweak is funny and is better than the plain old _**Sorry, incorrect password**_ error message. :smiley:

