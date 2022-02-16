# nexus_deploy

                                                NEXUS Configuration
                                                 ---------------------------------
Step-1:  Create a t2.medium Instance 
----------------------------------------------------
Step-2:  Install JDK  
----------------------------
JAVA Download:
https://www.oracle.com/in/java/technologies/javase/javase8u211-later-

archive-downloads.html

 wget https://download.oracle.com/otn/java/jdk/8u311-

b11/4d5417147a92418ea8b615e228bb6935/jdk-8u311-linux-x64.tar.gz?

AuthParam=1644982266_3a48daddc2bd75f1a457f10477270f4c

 mv jdk-8u311-linux-x64.tar.gz\?AuthParam

\=1644982266_3a48daddc2bd75f1a457f10477270f4c jdk-8u311-linux-

x64.tar.gz

 tar -xzf jdk-8u311-linux-x64.tar.gz

  # cd  ~    <--- to move to home
  # ls -a
  # vi .profile
 [press 'i' for insert ]
   export JAVA_HOME="/opt/jdk1.8.0_311"
   export PATH=$JAVA_HOME/bin:$PATH
 [press :wq --> for write and quit ]
  
# source .profile

java version "1.8.0_311"
Java(TM) SE Runtime Environment (build 1.8.0_311-b11)
Java HotSpot(TM) 64-Bit Server VM (build 25.311-b11, mixed mode)

Step-3:  Download Nexus :
----------------------------------------
https://www.sonatype.com/products/repository-oss-download
https://help.sonatype.com/repomanager3/product-information/download

 wget https://sonatype-

download.global.ssl.fastly.net/repository/downloads-prod-group/3/nexus-

3.37.3-02-unix.tar.gz

tar -xzf nexus-3.37.3-02-unix.tar.gz

Step-4:  Launch or Run Nexus :
----------------------------------------------
  # cd /opt/nexus-3.37.3-02/bin
  # ./nexus run   
   
Started Sonatype Nexus OSS 3.37.3-02

  Open a Duplicate session --->   # netstat -lntp  --> can find a port : 8081
   Browser ---> http://18.116.59.148:8081
 
  Sign in 
      uname :  admin
        pwd    : /opt/sonatype-work/nexus3/admin.password

   # cat   /opt/sonatype-work/nexus3/admin.password
             reset admin password

             Settings  --> Users --> Create local user -->  create user




Step-5:  Update POM.xml file :
----------------------------------------------
              # cd mvnproj
              # vi pom.xml

        <repository>
            <id>nexus</id>
            <name>Internal Releases</name>
            <url>http://18.116.59.148:8081/repository/maven-releases/</url>
        </repository>

        <snapshotRepository>
            <id>nexus</id>
            <name>Internal Snapshot Releases</name>
            <url>http://18.116.59.148:8081/repository/maven-snapshots/</url>
        </snapshotRepository>

Step-6:  Update Settings.xml file :
--------------------------------------------------

              #cd /opt/apache-maven-3.8.4/conf
              # vi settings.xml

  <server>
      <id>nexus</id>
      <username>admin</username>
      <password>abcd1234</password>
    </server>


Step-7:  Compile , Package and Deploy the code :
------------------------------------------------------------------------

                #cd mvnproj
                #mvn clean compile test package  <--- to get package
                #mvn install    <----- to move file to local repo (.m2)
                #mvn deploy   <----- to move file to Global repo (Nexus)



