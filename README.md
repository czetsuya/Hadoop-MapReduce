# Hadoop MapReduce Demo

Versions:
 - Hadoop 3.1.1
 - Java10

Set the following environment variables:
 - JAVA_HOME
 - Hadoop_HOME

## For Windows:
Download Hadoop 3.1.1 binaries for windows at https://github.com/s911415/apache-Hadoop-3.1.0-winutils. Extract in Hadoop_HOME\bin and make sure to override the existing files.

## For Ubuntu:
```sh
$ ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
$ cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
$ chmod 0600 ~/.ssh/authorized_keys
```

1.) Create the following folders:
 * Hadoop_HOME/tmp
 * Hadoop_HOME/tmp/dfs/data
 * Hadoop_HOME/tmp/dfs/name

2.) Set the following properties:
core-site.xml and hdfs-site.xml
```sh
<property>
  <name>fs.defaultFS</name>
  <value>hdfs://localhost:9001</value>
</property>
```
core-site.xml
```sh
<property>
	<name>Hadoop.tmp.dir</name>
	<value>Hadoop_HOME/tmp</value>
</property>
```
hdfs-site.xml
```sh
<property>
	<name>dfs.namenode.name.dir</name>
	<value>file:///Hadoop_HOME/tmp/dfs/name</value>
</property>
<property>
	<name>dfs.datanode.data.dir</name>
	<value>file:///Hadoop_HOME/tmp/dfs/data</value>
</property>
<!-- Will allow us to upload or create file later in hdfs -->
<property>
	<name>dfs.permissions</name>
	<value>false</value>
</property>
```

3.) Run Hadoop namenode -format
Don't forget the file:/// prefix in hdfs-site.xml for windows. Otherwise, the format will fail.

4.) Run Hadoop_HOME/sbin/start-dfs.xml.

5.) If all goes well, you can check the log for the web port in the console. In my case it's http://localhost:9870.

6.) You can now upload any file in the #4 URL.

Now let's try to create a project that will test our Hadoop setup. Or download an already existing one. For example this project: https://www.guru99.com/create-your-first-Hadoop-program.html. It has a nice explanation with it, so let's try. I've repackaged it into a pom project and uploaded at Github at https://github.com/czetsuya/Hadoop-MapReduce.

1.) Clone the repository.

2.) Open the hdfs url from the #5 above, and create an input and output folder.

3.) In input folder, upload the file SalesJan2009 from the project's root folder.

4.) Run Hadoop jar Hadoop-mapreduce-0.0.1-SNAPSHOT.jar /input /output.

5.) Check the output from the URL and download the resulting file.

Here's a more complicated example https://github.com/rathboma/Hadoop-framework-examples/tree/master/java-mapreduce.

### Common cause of problems:
 * Un-properly configured core-site or hdfs-site related to data and name node?
 * File / folder permission