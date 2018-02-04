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

> $HADOOP_HOME/sbin/mr-jobhistory-daemon.sh start historyserver

Finally, as a sanity check, we will make sure our java processes are running:

> jps 

You should see about 5 node processes running
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

We willn now copy 
