---
layout: post
title: "Setup Hadoop HDFS Locally"
date: 2020-02-19 11:00:00 +0800
tags: [data-engineering]
description: local setup
---

# Brief notes

## namenode

Namenode store meta data of all files of the all the datanodes in its cluster. The information is usually loaded into memory so thus the machine is memory intensive. Thus creating small files is not good practice as it would quickly eat up the memory in the Namenode. Even though datanodes are far from their storing capacity, no more files can be saved due to the lack of memory in namenode.

## datanode

Datanode is IO intensive. It writes file partion to disk and then copies to another datanode as replica.

## secondaryNameNode

Though the name suggests that secondaryNameNode is shadowing the primary namenode, its real job is **housekeeping**. It works with FsImage file and edits logs to make sure namenode can recover the information if it fails.

## standbyNamenode

A real-time standby Namenode that is in-sync with the primay namenode. Usually standbyNamenode and primaryNamenode will both subscribe from a journal manager (JM). Multiple JMs needs to be setup to establish quoram. This ensures the JM does not become the single point of failure.

# HDFS well explained

[Cartoon version](https://wiki.scc.kit.edu/gridkaschool/upload/1/18/Hdfs-cartoon.pdf)

## Text version

### Write operation

- client initiate a request to namenode, stating the block size, file fize
- namenode reply with list of datanodes for each partition
- client starts transfer to 1st datanode for each partition
- datanode writes into disk and copy to other datanodes
- all datanodes inform namenode that they have completed the write operation
- namenode writes metadata of and close file
- namenode inform client write is completed and successful

# local setup

```shell
# gen key
ssh-keygen -t rsa -P ''
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
chmod 0600 ~/.ssh/authorized_keys
# setup
tar -xzf hadoop-3.2.1.tar.gz
rm hadoop-3.2.1.tar.gz
mv hadoop-3.2.1 hadoop
chmod -R 755 hadoop
# .zshrc
export HADOOP_HOME=~/hadoop
export JAVA_HOME=`/usr/libexec/java_home -v 1.8`
export PATH=$PATH:$HADOOP_HOME/bin:$JAVA_HOME/bin
# working dir
mkdir -p $HADOOP_HOME/hadoop_store/tmp
chmod -R 755 $HADOOP_HOME/hadoop_store/tmp
mkdir -p $HADOOP_HOME/hadoop_store/namenode
mkdir -p $HADOOP_HOME/hadoop_store/datanode
chmod -R 755 $HADOOP_HOME/hadoop_store/namenode
chmod -R 755 $HADOOP_HOME/hadoop_store/datanode
cp ~/hadoopconfig/* $HADOOP_HOME/etc/hadoop
# start hdfs
ssh localhost
hdfs namenode -format
hdfs dfs -mkdir /user
sbin/start-all.sh
```

### Reference

[hadoop single cluster setup](https://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-common/SingleCluster.html)

[single node setup by @thedsa.in](https://medium.com/@thedsa.in/install-hadoop-3-2-setting-up-a-single-node-hadoop-cluster-22a5754bd9fc)
