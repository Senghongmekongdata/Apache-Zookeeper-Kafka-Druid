# Apache-Zookeeper-Kafka-Druid

![apache](https://user-images.githubusercontent.com/58208161/177106579-de43c730-998e-486a-8f09-2a5e47d28245.jpg)

[![APACHE-ZOOKEEPER](https://img.shields.io/badge/APACHE-ZOOKEEPER-%23FFac45.svg?&style=for-the-badge&logo=apache&logoColor=white&color=blue)](https://github.com/)
[![APACHE-KAFKA](https://img.shields.io/badge/APACHE-KAFKA-%23FFac45.svg?&style=for-the-badge&logo=apache&logoColor=white&color=yellow)](https://github.com/)
[![APACHE-DRUID](https://img.shields.io/badge/APACHE-DRUID-%230077B5.svg?&style=for-the-badge&logo=apache&logoColor=white)](https://www.linkedin.com/)
[![APACHE-SUPPERSET](http://img.shields.io/badge/APACHE-SUPPERSET-%231877F2.svg?&style=for-the-badge&logo=apache&logoColor=white&color=black)](https://github.com/)

## Pre-requirement

### Hardware 
```




```

### Software
To follow along, you will need:
```
- One Ubuntu 20.04 server and a non-root user with sudo privileges. Follow the steps specified in this guide if you do not have a non-root user set up.
- At least 4GB of RAM on your server. Installations without this amount of RAM may cause the Kafka service to fail.
- OpenJDK 11 installed on your server. To install this version, follow our tutorial How To Install Java with APT on Ubuntu 20.04. Kafka is written in Java, so it requires a JVM.

```

#### 1. Install Ubuntu 22.04 or highest one
You can install one from your microsoft store

![download](https://user-images.githubusercontent.com/58208161/177113568-2e4bfdc8-4c95-428e-93ff-16b1a80f29af.png)


#### 2. Install JAVA (Installing the Default JRE/JDK)
##### To install this version, first update the package index:
```
sudo apt update
```
##### Next, check if Java is already installed:
```
java -version


Output
Command 'java' not found, but can be installed with:

sudo apt install default-jre              # version 2:1.11-72build1, or
sudo apt install openjdk-11-jre-headless  # version 11.0.14+9-0ubuntu2
sudo apt install openjdk-17-jre-headless  # version 17.0.2+8-1
sudo apt install openjdk-18-jre-headless  # version 18~36ea-1
sudo apt install openjdk-8-jre-headless   # version 8u312-b07-0ubuntu1
```
##### Execute the following command to install the default Java Runtime Environment (JRE), which will install the JRE from OpenJDK 11 (latest version):
```
sudo apt install default-jre
```
-The JRE will allow you to run almost all Java software.
##### Verify the installation with:
```
java -version
```
##### You’ll see output similar to the following:
```
Output
openjdk version "11.0.14" 2022-01-18
OpenJDK Runtime Environment (build 11.0.14+9-Ubuntu-0ubuntu2)
OpenJDK 64-Bit Server VM (build 11.0.14+9-Ubuntu-0ubuntu2, mixed mode, sharing)
```
##### You may need the Java Development Kit (JDK) in addition to the JRE in order to compile and run some specific Java-based software. To install the JDK, execute the following command, which will also install the JRE:
```
sudo apt install default-jdk
```
##### Verify that the JDK is installed by checking the version of javac, the Java compiler:
```
javac -version

Output
javac 11.0.14
```

#### 3. SET JAVA_HOME path on your ubuntu machine
All you have to do now is to set the “JAVA_HOME” and “PATH” environment variables and then you are done. Enter the following commands to set your environment variables. Make sure that your environment variables point to a valid installation of JDK on your machine. For Ubuntu 18.04, the path is /usr/lib/jvm/java-8-openjdk-amd64/
```
export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
```
##### To check whether your JAVA_HOME path has been successfully saved, enter the following command to check.
```
echo $JAVA_HOME
```


#### 4 Add JAVA bin directory to the PATH variable

Like we have added JAVA_HOME path, we will now update the PATH variable as well. To do that, enter the following command on the terminal.
```
export PATH=$PATH:$JAVA_HOME/bin
```
##### You can also check the PATH variable by entering the following command
```
echo $PATH
```
##### Test JAVA setup
```
java -version
```

## Install Kafka

[Download](https://www.apache.org/dyn/closer.cgi?path=/kafka/3.2.0/kafka_2.13-3.2.0.tgz) the latest Kafka release and extract it:

### STEP 1: GET KAFKA
#### You can download using bash script:
```
$ wget https://dlcdn.apache.org/kafka/3.2.0/kafka_2.13-3.2.0.tgz
```
#### Extract this file:
```
$ tar -xzf kafka_2.13-3.2.0.tgz
$ cd kafka_2.13-3.2.0
```
### STEP 2: START THE KAFKA ENVIRONMENT
#### Run the following commands in order to start all services in the correct order:
```
# Start the ZooKeeper service
# Note: Soon, ZooKeeper will no longer be required by Apache Kafka.
$ bin/zookeeper-server-start.sh config/zookeeper.properties
```
#### Open another terminal session and run:
```
# Start the Kafka broker service
$ bin/kafka-server-start.sh config/server.properties
```
### STEP 3: CREATE A TOPIC TO STORE YOUR EVENTS
Kafka is a distributed event streaming platform that lets you read, write, store, and process events (also called records or messages in the documentation) across many machines.

Example events are payment transactions, geolocation updates from mobile phones, shipping orders, sensor measurements from IoT devices or medical equipment, and much more. These events are organized and stored in topics. Very simplified, a topic is similar to a folder in a filesystem, and the events are the files in that folder.

#### So before you can write your first events, you must create a topic. Open another terminal session and run:
```
$ bin/kafka-topics.sh --create --topic quickstart-events --bootstrap-server localhost:9092
```

All of Kafka's command line tools have additional options: run the kafka-topics.sh command without any arguments to display usage information. For example, it can also show you details such as the partition count of the new topic:
```
$ bin/kafka-topics.sh --describe --topic quickstart-events --bootstrap-server localhost:9092

Output
Topic:quickstart-events  PartitionCount:1    ReplicationFactor:1 Configs:
    Topic: quickstart-events Partition: 0    Leader: 0   Replicas: 0 Isr: 0
```




