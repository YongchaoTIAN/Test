# DiNoDB

DiNoDB is an interactive-speed query engine for ad-hoc queries on data stored in HDFS. DiNoDB has three components: DiNoDB node, DiNoDB client and MetaConnector. Here we omit the instruction about how to set up a Hadoop cluster.

## Install and Configuration

### DiNoDB node

DiNoDB node is a variant of PostgresSQL. To install and start DiNoDB node, simply execute command below on each machine: 

```bash installdinodbnode.sh```

If user is starting from DiNoDB image where DiNoDB node is already installed, user can just start DiNoDB node by command:

```bash startdinodbnode.sh```

By default, three instances of DiNoDB node on each machine is started.

### DiNoDB client

DiNoDB client is based on Stado, which is an open source shared-nothing database system. To install DiNoDB client on master machine:

```bash installconfigstado.sh```

You need to configurate DiNoDB client by editing ```stado/config/stado.config```. Each DiNoDB node instance is a xdb.node. 

If user is using DiNoDB image, only configuration is needed.

### MetaConnector

MetaConnector is the bridge between DiNoDB and HDFS. It's written in Python script and needs to install on each machine. You need to configurate it in ```metastore/metastore.conf``` where information of HDFS and DiNoDB node is provided. Remember to propagate configuration modification for each time.

## How to use

After each component of DiNoDB is installed and configured, DiNoDB system is initialized by:

```cd stado/bin;./createmddb.sh -u admin -p secret```

New database in DiNoDB can be created by:

```./gs-createdb.sh -u admin -p secret -d dbname -n <nodelist>```

DiNoDB SQL interface is started by:

```./gs-cmdline.sh -u admin -p secret -d dbname```

Table schema in DiNoDB can be defined here. But to link tables in DiNoDB to data files stored in HDFS, user needs to use MetaConnector. First, daemon process of MetaConnector in each DiNoDB node machine should be started by command:

```cd metastore; python dinodbnode.py &```

To link data in HDFS to table in DiNoDB:

```python dinodbconf.py -r <tablename> -f <hdfsdirectory> -d <dbname>```

Pay attention that after using MetaConnector linking data and table schema, DiNoDB database needs to be restarted by commands:

```./gs-dbstop.sh -u admin -p secret -d dbname; ./gs-dbstart.sh -u admin -p secret -d dbname```
