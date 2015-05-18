# DiNoDB

DiNoDB has three parts: DiNoDB node, DiNoDB client and MetaConnector.

## DiNoDB node

DiNoDB node is a variant of PostgresSQL. To install DiNoDB node, simply execute command below on each machine: 

```bash installdinodb.sh```

By default, three instances of DiNoDB node on each machine is started.

## DiNoDB client

DiNoDB client is based on Stado, which is an open source shared-nothing database system. To install DiNoDB client on master machine:

```bash installconfigstado.sh```

You need to config DiNoDB client.

## MetaConnector

MetaConnector is the bridge between DiNoDB and HDFS. It's written in Python script.


