# Installing and Running Kibana


### Installing Kibana and Console

[_**Kibana**_](https://www.elastic.co/guide/en/kibana/current/index.html) is an open source analytics and visualization platform designed to work with Elasticsearch and Console (Previously its name was Sence, Sence was renamed to Console and it is available on Kibana 5)
Kibana provides an interactive console for submitting requests to Elasticsearch directly from your browser.

The Console plugin provides a UI to interact with the REST API of Elasticsearch. The console has two main areas: the **editor**, where you compose requests to Elasticsearch, and the **response** pane, which displays the responses to the request.

We need to install Kibana. Kibana is available in tar, zip, deb, rpm and docker package formats. For Linux and Darwin, we can download tar.gz package.
[Download Latest Kibana](https://www.elastic.co/downloads/kibana) version. Other versions can be found on the [Past Releases page](https://www.elastic.co/downloads/past-releases).

The 64-bit Linux archive for Kibana v5.6.0 can be downloaded and installed as follows:


    wget https://artifacts.elastic.co/downloads/kibana/kibana-5.6.0-linux-x86_64.tar.gz
    sha1sum kibana-5.6.0-linux-x86_64.tar.gz

Then extract it as follows:

    tar -xzf kibana-5.6.0-linux-x86_64.tar.gz

Now go to the directory:

    cd kibana-5.6.0-linux-x86_64

Now you can run kibana using the following command:

    ./bin/kibana


By default, Kibana runs in the foreground, prints its logs to the standard output `stdout`, You can stop kibana by pressing.`Ctrl-C`

    log [13:56:16.449] [info][status][plugin:kibana@5.6.0] Status changed from uninitialized to green - Ready
    log [13:56:16.553] [info][status][plugin:elasticsearch@5.6.0] Status changed from uninitialized to yellow - Waiting for Elasticsearch
    log [13:56:16.590] [info][status][plugin:console@5.6.0] Status changed from uninitialized to green - Ready
    log [13:56:16.617] [info][status][plugin:metrics@5.6.0] Status changed from uninitialized to green - Ready
    log [13:56:16.882] [info][status][plugin:timelion@5.6.0] Status changed from uninitialized to green - Ready
    log [13:56:16.888] [info][listening] Server running at http://localhost:5601
    log [13:56:16.890] [info][status][ui settings] Status changed from uninitialized to yellow - Elasticsearch plugin is yellow
    log [13:56:24.579] [info][status][plugin:elasticsearch@5.6.0] Status changed from yellow to yellow - No existing Kibana index found
    log [13:56:35.752] [info][status][plugin:elasticsearch@5.6.0] Status changed from yellow to green - Kibana index ready
    log [13:56:35.759] [info][status][ui settings] Status changed from yellow to green - Ready<code class="literal">


You can see from the log that Server running at http://localhost:5601, Kibana is a web application that you access through port 5601. All you need to do is point your web browser at the machine where Kibana is running and specify the port number. For example, `localhost:5601`

In Kibana, just click on _Dev Tools_:

![](http://www.rimonmostafiz.com/wp-content/uploads/2017/09/kibana-console-300x168.png)

Now you can communicate with Elasticsearch through this Console. Now click on the green play icon to run the command.

