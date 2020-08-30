# Installing and Running Elasticsearch


The easiest way to understand what Elasticsearch is to play with it, so let’s get started. Elastic search is easy to install. In this tutorial, I will walk you through the elasticsearch installation process in Ubuntu 16.04. Elasticsearch requires a recent version of java. Oracle JDK version 1.8 is recommended. <br>
I am using **JDK 1.8.0_131**.

Before you install Elasticsearch, please check your Java version first by running:


    java -version
    echo $JAVA_HOME


We can download Elasticsearch from [`www.elastic.co/downloads`](http://www.elastic.co/downloads) along with all the release that has been made in the past. For each release `zip` `tar` archive, or `DEB` and `RPM` package is available.


At the time of writing post the latest version of Elasticsearch is 5.6.0.
Let's download `tar.gz`from `[www.elastic.co/downloads/elasticsearch](http://www.elastic.co/downloads/elasticsearch)`
Then extract it as follows:

    tar -xvf elasticsearch-5.6.0.tar.gz

Now go to the bin directory:

    cd elasticsearch-5.6.0/bin

And now we are ready to start our node and single cluster:

    ./elasticsearch


<blockquote>Add -d if you want to run it in the background as a daemon.

If you’re running Elasticsearch on Windows, simply run `bin\elasticsearch.bat` instead.</blockquote>


If everything goes well, you should see a bunch of messages that look like:


    [2017-09-15T23:49:35,321][INFO ][o.e.n.Node ] [] initializing ...
    [2017-09-15T23:49:35,729][INFO ][o.e.e.NodeEnvironment ] [AxGDTVX] using [1] data paths, mounts [[/ (/dev/sda2)]], net usable_space [19.1gb], net total_space [96.5gb], spins? [possibly], types [ext4]
    [2017-09-15T23:49:35,730][INFO ][o.e.e.NodeEnvironment ] [AxGDTVX] heap size [1.9gb], compressed ordinary object pointers [true]
    [2017-09-15T23:49:35,734][INFO ][o.e.n.Node ] node name [AxGDTVX] derived from node ID [AxGDTVX3RrmSo1oI4sAtFQ]; set [node.name] to override
    [2017-09-15T23:49:35,734][INFO ][o.e.n.Node ] version[5.6.0], pid[18814], build[781a835/2017-09-07T03:09:58.087Z], OS[Linux/4.4.0-93-generic/amd64], JVM[Oracle Corporation/Java HotSpot(TM) 64-Bit Server VM/1.8.0_131/25.131-b11]
    [2017-09-15T23:49:35,735][INFO ][o.e.n.Node ] JVM arguments [-Xms2g, -Xmx2g, -XX:+UseConcMarkSweepGC, -XX:CMSInitiatingOccupancyFraction=75, -XX:+UseCMSInitiatingOccupancyOnly, -XX:+AlwaysPreTouch, -Xss1m, -Djava.awt.headless=true, -Dfile.encoding=UTF-8, -Djna.nosys=true, -Djdk.io.permissionsUseCanonicalPath=true, -Dio.netty.noUnsafe=true, -Dio.netty.noKeySetOptimization=true, -Dio.netty.recycler.maxCapacityPerThread=0, -Dlog4j.shutdownHookEnabled=false, -Dlog4j2.disable.jmx=true, -Dlog4j.skipJansi=true, -XX:+HeapDumpOnOutOfMemoryError, -Des.path.home=/home/rimonmostafiz/Applications/elasticsearch-5.6.0]
    [2017-09-15T23:49:37,418][INFO ][o.e.p.PluginsService ] [AxGDTVX] loaded module [aggs-matrix-stats]
    [2017-09-15T23:49:37,418][INFO ][o.e.p.PluginsService ] [AxGDTVX] loaded module [ingest-common]
    [2017-09-15T23:49:37,418][INFO ][o.e.p.PluginsService ] [AxGDTVX] loaded module [lang-expression]
    [2017-09-15T23:49:37,418][INFO ][o.e.p.PluginsService ] [AxGDTVX] loaded module [lang-groovy]
    [2017-09-15T23:49:37,419][INFO ][o.e.p.PluginsService ] [AxGDTVX] loaded module [lang-mustache]
    [2017-09-15T23:49:37,419][INFO ][o.e.p.PluginsService ] [AxGDTVX] loaded module [lang-painless]
    [2017-09-15T23:49:37,419][INFO ][o.e.p.PluginsService ] [AxGDTVX] loaded module [parent-join]
    [2017-09-15T23:49:37,419][INFO ][o.e.p.PluginsService ] [AxGDTVX] loaded module [percolator]
    [2017-09-15T23:49:37,419][INFO ][o.e.p.PluginsService ] [AxGDTVX] loaded module [reindex]
    [2017-09-15T23:49:37,420][INFO ][o.e.p.PluginsService ] [AxGDTVX] loaded module [transport-netty3]
    [2017-09-15T23:49:37,420][INFO ][o.e.p.PluginsService ] [AxGDTVX] loaded module [transport-netty4]
    [2017-09-15T23:49:37,421][INFO ][o.e.p.PluginsService ] [AxGDTVX] no plugins loaded
    [2017-09-15T23:49:40,745][INFO ][o.e.d.DiscoveryModule ] [AxGDTVX] using discovery type [zen]
    [2017-09-15T23:49:41,885][INFO ][o.e.n.Node ] initialized
    [2017-09-15T23:49:41,885][INFO ][o.e.n.Node ] [AxGDTVX] starting ...
    [2017-09-15T23:49:42,159][INFO ][o.e.t.TransportService ] [AxGDTVX] publish_address {127.0.0.1:9300}, bound_addresses {[::1]:9300}, {127.0.0.1:9300}
    [2017-09-15T23:49:42,183][WARN ][o.e.b.BootstrapChecks ] [AxGDTVX] max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]
    [2017-09-15T23:49:45,275][INFO ][o.e.c.s.ClusterService ] [AxGDTVX] new_master {AxGDTVX}{AxGDTVX3RrmSo1oI4sAtFQ}{W15blCZPT8m4q1zaExLQnA}{127.0.0.1}{127.0.0.1:9300}, reason: zen-disco-elected-as-master ([0] nodes joined)
    [2017-09-15T23:49:45,364][INFO ][o.e.h.n.Netty4HttpServerTransport] [AxGDTVX] publish_address {127.0.0.1:9200}, bound_addresses {[::1]:9200}, {127.0.0.1:9200}
    [2017-09-15T23:49:45,364][INFO ][o.e.n.Node ] [AxGDTVX] started
    [2017-09-15T23:49:45,410][INFO ][o.e.g.GatewayService ] [AxGDTVX] recovered [0] indices into cluster_state


Here we can see our node name is `AxGDTVX`(which will be a different set of characters in your case) has started and elected itself as a master in a single cluster.
We can override either the cluster or node name. This can be done from the command line when starting Elasticsearch as follows:


    ./elasticsearch -Ecluster.name=my_cluster_name -Enode.name=my_node_name


Elasticsearch is running on HTTP address (127.0.0.1) which is localhost and port (9200) that our node is reachable from.
By default, Elasticsearch uses port 9200 to provide access to its REST API. This port is configurable if necessary.

So if now we fire up a browser and hit `http://localhost:9200,` Its gives something like:


    {
      "name" : "AxGDTVX",
      "cluster_name" : "elasticsearch",
      "cluster_uuid" : "KzVOPWDoROWQwQuxHqz1yg",
      "version" : {
        "number" : "5.6.0",
        "build_hash" : "781a835",
        "build_date" : "2017-09-07T03:09:58.087Z",
        "build_snapshot" : false,
        "lucene_version" : "6.6.0"
      },
      "tagline" : "You Know, for Search"
    }


So we can see that Elasticsearch is up and running.
If you use windows then you can find the installation guide from [here](https://www.elastic.co/guide/en/elasticsearch/reference/5.6/_installation.html).

