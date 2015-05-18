# DiNoDB

DiNoDB has three components: DiNoDB node, DiNoDB client and MetaConnector.

## Install and Configuration

### DiNoDB node

DiNoDB node is a variant of PostgresSQL. To install DiNoDB node, simply execute command below on each machine: 

```bash installdinodb.sh```

By default, three instances of DiNoDB node on each machine is started.

### DiNoDB client

DiNoDB client is based on Stado, which is an open source shared-nothing database system. To install DiNoDB client on master machine:

```bash installconfigstado.sh```

You need to configurate DiNoDB client by editing stado/config/stado.config. Each DiNoDB node instance is a xdb.node.

### MetaConnector

MetaConnector is the bridge between DiNoDB and HDFS. It's written in Python script and needs to install on each machine. You need to configurate it in metastore.conf where information of HDFS and DiNoDB node is provided. Remember to propagate configuration modification for each time.

## How to use

After each component of DiNoDB is installed and configured, DiNoDB system is initialized by:

```cd stado/bin;./createmddb.sh -u admin -p secret```

New database in DiNoDB can be created by:

```./gs-createdb.sh -u admin -p secret -d dbname -n <nodelist>```


