# Lightstreamer - Chat-Tile Demo - Java Adapter #

<!-- START DESCRIPTION lightstreamer-example-chattile-adapter-java -->

The *Chat-Tile Demo* implements a simple chat/collaborative application based on [Lightstreamer](http://www.lightstreamer.com) for its real-time communication needs.

This project shows the Data Adapter and Metadata Adapters for the *Chat-Tile Demo* and how they can be plugged into Lightstreamer Server.

As an example of a client using this adapter, you may refer to the [Chat-Tile Demo - HTML (JQuery, Masonry) Client](https://github.com/Lightstreamer/Lightstreamer-example-ChatTile-client-javascript) and view the corresponding [Live Demo](http://demos.lightstreamer.com/ChatTileDemo/).

## Details

This project includes the implementation of the [SmartDataProvider](https://lightstreamer.com/api/ls-adapter-inprocess/latest/com/lightstreamer/interfaces/data/SmartDataProvider.html) interface and the [MetadataProviderAdapter](https://lightstreamer.com/api/ls-adapter-inprocess/latest/com/lightstreamer/interfaces/metadata/MetadataProviderAdapter.html) interface for the *Lightstreamer Chat-Tile Demo*. Please refer to [General Concepts](http://www.lightstreamer.com/docs/base/General%20Concepts.pdf) for more details about Lightstreamer Adapters.

### Java Data Adapter and MetaData Adapter

The Data Adapter accepts message submission for the unique chat room. The sender is identified by an IP address and a nickname.

The Metadata Adapter inherits from the reusable [LiteralBasedProvider](https://github.com/Lightstreamer/Lightstreamer-example-ReusableMetadata-adapter-java) and just adds a simple support for message submission. It should not be used as a reference for a real case of client-originated message handling, as no guaranteed delivery and no clustering support is shown.
<!-- END DESCRIPTION lightstreamer-example-chattile-adapter-java -->


### The Adapter Set Configuration

This Adapter Set is configured and will be referenced by the clients as `CHATTILE`. 

The `adapters.xml` file for the *Chat-Tile Demo*, should look like:

```xml      
<?xml version="1.0"?>
<adapters_conf id="CHATTILE">

    <!--
      Not all configuration options of an Adapter Set are exposed by this file. 
      You can easily expand your configurations using the generic template, 
      `DOCS-SDKs/sdk_adapter_java_inprocess/doc/adapter_conf_template/adapters.xml`,
      as a reference.
    -->
    
    <metadata_adapter_initialised_first>Y</metadata_adapter_initialised_first>

    <metadata_provider>
        <adapter_class>com.lightstreamer.adapters.ChatTileDemo.ChatTileMetaAdapter</adapter_class>

        <!-- Optional configuration file for the Adapter's own logging.
             Logging is managed through log4j. -->
        <param name="log_config">adapters_log_conf.xml</param>
        <param name="log_config_refresh_seconds">10</param>
  
        <!--
          TCP port on which Sun/Oracle's JMXMP connector will be
          listening.
        -->
        <param name="jmxPort">9999</param>
        
        <messages_pool>
            <max_size>1000</max_size>
            <max_free>10</max_free>
        </messages_pool>
        
    </metadata_provider>
    
    <data_provider>
        <adapter_class>com.lightstreamer.adapters.ChatTileDemo.ChatTileAdapter</adapter_class>
          
    </data_provider>
</adapters_conf>
```

<i>NOTE: not all configuration options of an Adapter Set are exposed by the file suggested above. 
You can easily expand your configurations using the generic template, `DOCS-SDKs/sdk_adapter_java_inprocess/doc/adapter_conf_template/adapters.xml`, as a reference.</i><br>
<br>
Please refer [here](http://www.lightstreamer.com/docs/base/General%20Concepts.pdf) for more details about Lightstreamer Adapters.

## Install
If you want to install a version of this demo in your local Lightstreamer Server, follow these steps:
* Download *Lightstreamer Server* (Lightstreamer Server comes with a free non-expiring demo license for 20 connected users) from [Lightstreamer Download page](http://www.lightstreamer.com/download.htm), and install it, as explained in the `GETTING_STARTED.TXT` file in the installation home directory.
* Get the `deploy.zip` file of the [latest release](https://github.com/Lightstreamer/Lightstreamer-example-ChatTile-adapter-java/releases), unzip it, and copy the just unzipped `ChatTile` folder into the `adapters` folder of your Lightstreamer Server installation.
* Get the `ua-parser-1.2.2.jar` file from [ua_parser Java Library](https://github.com/tobie/ua-parser/tree/master/java) and copy it into the `adapters/ChatTile/lib` folder.
* Get the `snakeyaml-1.11.jar` files from [SnakeYAML](https://code.google.com/p/snakeyaml/) and copy it into the `adapters/ChatTile/lib` folder.
* [Optional] Customize the specific "LS_ChatTileDemo_Logger" and "LS_demos_Logger" categories in log4j configuration file `ChatTile/adapters_log_conf.xml`.
* Launch Lightstreamer Server.
* Test the Adapter, launching the client listed in [Clients Using This Adapter](https://github.com/Lightstreamer/Lightstreamer-example-ChatTile-adapter-java#clients-using-this-adapter).

## Build
To build your own version of `LS_ChatTile_Demo_Adapters.jar`, instead of using the one provided in the `deploy.zip` file from the [Install](https://github.com/Lightstreamer/Lightstreamer-example-ChatTile-adapter-java#install) section above, follow these steps:
* Download this project.
* Get the `ls-adapter-interface.jar` file from the [latest Lightstreamer distribution](http://www.lightstreamer.com/download), and copy it into the `lib` folder.
* Get the `log4j-1.2.17.jar` file from [Apache log4j](https://logging.apache.org/log4j/1.2/) and copy it into the `lib` folder.
* Get the `ua-parser-1.2.2.jar` file from [ua_parser Java Library](https://github.com/tobie/ua-parser/tree/master/java), and copy it into the `lib` folder.
* Get the `snakeyaml-1.11.jar` file from [SnakeYAML](https://code.google.com/p/snakeyaml/), and copy it into the `lib` folder.
* Build the jar `LS_ChatTile_Demo_Adapters.jar` with commands like these:
```sh
 > mkdir tmp_classes
 > javac -source 1.7 -target 1.7 -nowarn -g -classpath lib/log4j-1.2.17.jar;lib/ls-adapter-interface.jar;lib/jbox2d-library-2.2.1.1.jar;lib/ua-parser-1.2.2.jar;lib/snakeyaml-1.11.jar -sourcepath src/ -d tmp_classes src/com/lightstreamer/adapters/ChatTileDemo/ChatTileAdapter.java
 > jar cvf LS_ChatTile_Demo_Adapters.jar -C tmp_classes com
```
* Stop Lightstreamer Server; copy the just compiled LS_ChatTile_Demo_Adapters.jar in the adapters/ChatTile/lib folder of your Lightstreamer Server installation; restart Lightstreamer Server.

## See Also 

### Clients Using This Adapter
<!-- START RELATED_ENTRIES -->
<!-- END RELATED_ENTRIES -->

* [Lightstreamer - Chat-Tile Demo - JQuery Client](https://github.com/Lightstreamer/Lightstreamer-example-ChatTile-client-javascript)

<!-- END RELATED_ENTRIES -->

### Related Projects

* [Lightstreamer - Chat Demo - Java Adapter](https://github.com/Lightstreamer/Lightstreamer-example-Chat-adapter-java)
* [Lightstreamer - Reusable Metadata Adapters - Java Adapter](https://github.com/Lightstreamer/Lightstreamer-example-ReusableMetadata-adapter-java)
* [Lightstreamer - Basic Messenger Demo - Java Adapter](https://github.com/Lightstreamer/Lightstreamer-example-Messenger-adapter-java)
* [Lightstreamer - Basic Messenger Demo - HTML Client](https://github.com/Lightstreamer/Lightstreamer-example-Messenger-client-javascript)

## Lightstreamer Compatibility Notes

* Compatible with Lightstreamer SDK for Java In-Process Adapters since 6.0
- For a version of this example compatible with Lightstreamer SDK for Java Adapters version 5.1, please refer to [this tag](https://github.com/Lightstreamer/Lightstreamer-example-ChatTile-adapter-java/tree/for_Lightstreamer_5.1).
