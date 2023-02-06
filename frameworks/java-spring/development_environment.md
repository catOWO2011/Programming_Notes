# Development Environment

# Table of Contents
1. [What do you need for spring ?](#what-do-you-need-for-spring)
2. [Setup Maven for intellij](#setup-maven-for-intellij)
3. [How to open a project created with spring initializr using intellij](#how-to-open-a-project-created-with-spring-initializr-using-intellij)

## What do you need for spring ?
You need the following tools
### Java JDK
Check if you have installed with:
```bash
java --version && java --version
openjdk 11.0.14.1 2022-02-08 LTS
OpenJDK Runtime Environment Corretto-11.0.14.10.1 (build 11.0.14.1+10-LTS)
OpenJDK 64-Bit Server VM Corretto-11.0.14.10.1 (build 11.0.14.1+10-LTS, mixed mode)
openjdk 11.0.14.1 2022-02-08 LTS
OpenJDK Runtime Environment Corretto-11.0.14.10.1 (build 11.0.14.1+10-LTS)
OpenJDK 64-Bit Server VM Corretto-11.0.14.10.1 (build 11.0.14.1+10-LTS, mixed mode)
```
### Maven

#### Installing Maven

Download Maven Binaries:
```bash
$ wget https://dlcdn.apache.org/maven/maven-3/3.8.6/binaries/apache-maven-3.8.6-bin.tar.gz
$ tar -xvf apache-maven-3.8.6-bin.tar.gz
$ mv apache-maven-3.8.6 /opt/
```
Set the following configuration on the ``.profile`` file
```bash
# maven java configuration
JAVA_HOME='/usr/lib/jvm/java-17-amazon-corretto'
PATH="$JAVA_HOME/bin:$PATH"
export PATH
M2_HOME='/opt/apache-maven-3.8.6'
PATH="$M2_HOME/bin:$PATH"
export PATH
```
Excute the following command
```bash
source .profile
```

```bash
mvn --version
Apache Maven 3.6.3
Maven home: /usr/share/maven
Java version: 11.0.14.1, vendor: Amazon.com Inc., runtime: /usr/lib/jvm/java-11-amazon-corretto
Default locale: en_US, platform encoding: UTF-8
OS name: "linux", version: "5.4.0-113-generic", arch: "amd64", family: "unix"
```
#### Gradle
```bash
gradle --version

------------------------------------------------------------
Gradle 7.4.2
------------------------------------------------------------

Build time:   2022-03-31 15:25:29 UTC
Revision:     540473b8118064efcc264694cbcaa4b677f61041

Kotlin:       1.5.31
Groovy:       3.0.9
Ant:          Apache Ant(TM) version 1.10.11 compiled on July 10 2021
JVM:          11.0.14.1 (Amazon.com Inc. 11.0.14.1+10-LTS)
OS:           Linux 5.4.0-113-generic amd64
```

## Setup Maven for intellij
To avoid this problem
![Example screenshot](./setup-environment-assets/is-not-correct-mave-home.png)
Setup the following config:
![Setup maven](./setup-environment-assets/setup-maven-intellij.png)

Setup java version
![Setup java](./setup-environment-assets/setup-sdk-java-version-jdk.png)
## How to open a project created with spring initializr using intellij

We need to take the files from the zip and open a project from intellij selection the **pom.xml** file