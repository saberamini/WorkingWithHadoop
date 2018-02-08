# Working with Hadoop

Before you start, take a <b>snapshot</b> of your virtual machine after you have setup Hadoop.  
This way, you can "go back" to a fresh install in case something "messes up" in the process.


Startup your DFS - distributed file system. (takes a bit of time).
Remember we only have a single node (your virtual machine) so there is not a lot of parallel processing but the elements are there even in a single node and this allows us to see if everything in our setup is working.

> $HADOOP_HOME/sbin/start-dfs.sh

Pay attention to the log outputs. You need to get into the habit of always checking logs for any commands but especially when working with a complex software setup such as Hadoop.

Type "Yes" and press enter when asked "Are you sure you want to continue connecting"

Once it is done, you can look at the information on your file system in the browswer.  Open up firefox in your virtual machine (not your native operating system) and go to the address:

> http://localhost:50070

Take a look around the site.  It gives you a lot of information and you will use this as an administrator to troubleshoot issues with your Hadoop setup.

Now we want to start YARN.  Remember YARN stands for "Yet Another Resource Locater".  It is an improved version of MapReduce and it is sometimes called MapReduce 2.0

> $HADOOP_HOME/sbin/start-yarn.sh

Start the History Server

> $HADOOP_HOME/sbin/mr-jobhistory-daemon.sh start historyserver

Finally, as a sanity check, we will make sure our java processes are running:

> jps 

You should see about 5 node processes running, soimething like:
```
8065 SecondaryNameNode
8243 ResourceManager
8676 JobHistoryServer
7877 DataNode
7765 NameNode
8717 Jps
```

# Test the HDFS 

Create a txt file in your local home folder.

> echo "Hello this will be my first distributed and fault-tolerant data set\!" cat >> my_file.txt

Next we will list the files that are in our HDFS.

> hdfs dfs -ls /

This should not return anything because we have just formatted the file system.

We now will create a directory called user using in our HDFS

> hdfs dfs -mkdir /user

Go to the webbrowser, click on the "Utilities" menu and click on "Browse the file system".  You will see the user folder and the statistics.

We will list the files again.

> hdfs dfs -ls /

You should see the folder user listed.

We willn now copy the created file a few times:

> hdfs dfs -copyFromLocal ~/my_file.txt /user

> hdfs dfs -copyFromLocal ~/my_file.txt /user/my_file2.txt

> hdfs dfs -copyFromLocal ~/my_file.txt /user/my_file3.txt

You can now list the files in the new folder

> hdfs dfs -ls /user

You can also use your browser and see the files list under "user" in the under "Utilities" --> "Browse the file system"

Remove the files with a name starting with my_file

> hdfs dfs -rm /user/my_file*

YOu should see the files removed.

Finally you can delete the file "user"

> hdfs dfs -rmdir /user

And you should see it removed (either on the webbrowser or on the command line using the command shown above)


