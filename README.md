running-janusgraph-locally
==========================

Provides the docker-compose scripts and configuration files along with
instructions on how to install and run Janusgraph on a local machine

 

Requirements
------------

Docker-Compose must be installed on your machine. See [Install
Compose](https://docs.docker.com/v17.09/compose/install/)

After installation, it is recommended that you assign 4 cores and at least 6GB
of memory to Docker using the Docker application settings.

 

 

![](https://github.com/sadams-rti-org/running-janusgraph-locally/blob/master/details/janusgraph-logo-small.png)

Instructions for installing and using JanusGraph
------------------------------------------------

1.  Open a Terminal or Powershell window, depending on your platform

2.  Navigate to where you want to install JanusGraph

3.  Clone this repository, renaming it as desired

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
git clone https://github.com/sadams-rti-org/running-janusgraph-locally
mv running-janusgraph-locally my-janusgraph
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

4.  Use one the following commands as desired to run/stop JanusGraph:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
./janus-up
./janus-down
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

5.  Once you have run JanusGraph, all your data is stored in the ./details/data
    folder. The next time you start JanusGaph, it will attach to this data
    automatically. If you desire to erase this data and start over, use the
    following command:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
./janus-erase
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

 

 

![](https://github.com/sadams-rti-org/running-janusgraph-locally/blob/master/details/tinkertools-logo-small.png)

Instructions for using Tinkertools
----------------------------------

Optionally, use one of the following commands as desired to run/stop
Tinkertools, the interactive scripting, editing and visualization tool for
janusgraph databases:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
./tinkertools-up
./tinkertools-down
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Once you have run Tinkertools, your script database will be stored in
./details/data/mongodb. The next time you start Tinkertools, it will attach to
this data automatically. If you desire to erase this data and start over, use
the following command:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
./tinkertools-erase
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

 


Reading and writing graph data to and from files
------------------------------------------------

The folder at ./details/graph-io in your installation is bound to
/opt/janusgraph/graph-io inside the container hosting Janusgraph.  This means
any file in the ./details/graph-io folder is visible to your Gremlin/Groovy
scripts at /opt/janusgraph/graph-io.  You can use FTP to move files to and from
the server hosting Janusgraph.

 

In this distribution there are two graph files provided as examples:

-   air-routes-latest.graphml

-   ohio-counties-with-adjoins-edges.graphson

 

To load these into your database, use gremlin scripts like the following:

For GraphML format:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
graph.io(IoCore.graphml()).readGraph("/opt/janusgraph/graph-io/air-routes-latest.graphml")
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

or for GraphSON3 format:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
graph.io(IoCore.graphson()).readGraph("/opt/janusgraph/graph-io/ohio-counties-with-adjoins-edges.graphson")
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

 

To save your graph to a file, use one of these scripts depending on the output
format desired:

For GraphML format:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
graph.io(IoCore.graphml()).writeGraph("/opt/janusgraph/graph-io/my-graph.xml")
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For GraphSON3 format:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
graph.io(graphson()).writeGraph("/opt/janusgraph/graph-io/my-graph.graphson")
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For Gryo(Kryo) format:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
graph.io(gryo()).writeGraph("/opt/janusgraph/graph-io/my-graph.kryo")
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Which can then be read using:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
graph.io(gryo()).readGraph("/opt/janusgraph/graph-io/my-graph.kryo")
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
