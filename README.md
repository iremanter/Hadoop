# Hadoop

Mac (Apple Chip M1, M2, M3) Users: Open a Terminal and pull the image:

docker pull bugbond/hadoop-spark-pig-hive-arm64
Run the services:

docker run -it --name bigtools -p 9000:9000 -p 2122:2122 -p 50070:50070 -p 50010:50010 -p 50075:50075 -p 50020:50020 -p 50090:50090 -p 8088:8088 -p 8030:8030 -p 8031:8031 -p 8032:8032 -p 8033:8033 -p 8040:8040 -p 8042:8042 -p 8080:8080 -p 8081:8081 -p 10000:10000 -p 9083:9083 bugbond/hadoop-spark-pig-hive-arm64:latest bash
Wait for few minutes until the prompt changes to something like this:

* Starting OpenBSD Secure Shell server sshd                                                                    
Waiting for hdfs to exit from safemode
Safe mode is OFF
Started
root@b5dc483f5c73:/# 
Port Number Explained

2122:2122 \ # SSH

50070:50070 \ # HDFS NameNode

50010:50010 \ # HDFS DataNode

50075:50075 \ # HDFS DataNode

50020:50020 \ # SecondaryNameNode

50090:50090 \ # HDFS DataNode Secure

8088:8088 \ # YARN ResourceManager

8030:8030 \ # YARN ResourceManager Scheduler

8031:8031 \ # YARN ResourceManager Scheduler

8032:8032 \ # YARN ResourceManager Scheduler

8033:8033 \ # YARN ResourceManager Scheduler

8040:8040 \ # YARN NodeManager

8042:8042 \ # YARN NodeManager Web UI

8080:8080 \ # Spark Master Web UI

8081:8081 \ # Spark Worker Web UI

10000:10000 \ # HiveServer2

Note: Use the below command if you exit Hadoop container and wanna re-run the created container and get access to your previous work:

docker exec -it myhadoop bash
To access Hadoop Web Interface, Open a browser window/tab and navigate to http://localhost:50070, and Spark at http://localhost:8080

Update Ubuntu: apt update

Install nano editor: apt install nano

Verify Hadoop Installation ls /usr/local/hadoop

Set Up Environment Variables:

nano ~/.bashrc
Add the following lines:

export HADOOP_HOME=/usr/local/hadoop
export HADOOP_CONF_DIR=$HADOOP_HOME/etc/hadoop
export PATH=$PATH:$HADOOP_HOME/bin:$HADOOP_HOME/sbin
Source the ~/.bashrc file:

source ~/.bashrc
Note: If, for any reason, Hadoop stops working, use the following commands to restart it:

stop-dfs.sh
stop-yarn.sh
start-dfs.sh
start-yarn.sh
. Navigate to the home directory: cd home and press Enter

Create a new directory: mkdir datasrc

Download this Amazon Books Reviews dataset to your computer.

Unzip the extracted folder

Open a new Command Prompot or Terminal window and copy the downloaded file to the container. The container ID looks like e.g. 3d6c17a05e33 extracted from root@3d6c17a05e33:~# prompt.

docker cp Books_rating.csv 3d6c17a05e33:/home/datasrc 
Create a directory in HDFS:

hadoop fs -mkdir -p /home/datasrc/bigDataTask
Upload the file to HDFS:

hadoop fs -put Books_rating.csv /home/datasrc/bigDataTask
Make sure the file is uploaded

hadoop fs -ls /home/datasrc/bigDataTask
Checking the Size of the File

hdfs dfs -du -h /home/datasrc/bigDataTask/Books_rating.csv
See the number of blocks

hadoop fsck /home/datasrc/bigDataTask
Note

Create a directory in HDFS: hdfs dfs -mkdir -p /user/root/test

Remove a directory in HDFS: hdfs dfs -rm -r /user/root/test

List files/folders in HDFS: hdfs dfs -ls /user/root
