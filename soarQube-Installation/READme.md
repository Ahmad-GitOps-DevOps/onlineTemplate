## SonarQube Installation And Setup In AWS EC2 Redhat Instnace.
##### Prerequisite
+ AWS Acccount.
+ Create Redhat EC2 T2.medium Instnace with 4GB RAM.
+ Create Security Group and open Required ports.
   + 9000 ..etc
+ Attach Security Group to EC2 Instance.
+ Install java openJDK 1.8+ for SonarQube version 7.8

## Create sonar user to manage the SonarQube server
```sh
#As a good security practice, SonarQuber Server is not advised to run sonar service as a root user, 
# create a new user called sonar and grant sudo access to manage sonar services as follows

sudo useradd sonar
# Grand sudo access to sonar user
sudo echo "sonar ALL=(ALL) NOPASSWD:ALL" | sudo tee /etc/sudoers.d/sonar
sudo su - sonar
```

### Install Java JDK 1.8+

``` sh
hostname sonar
cd /opt
sudo yum -y install unzip wget git
sudo wget -c --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/8u131-b11/d54c1d3a095b4ff2b6607d096fa80163/jdk-8u131-linux-x64.rpm
sudo yum install jdk-8u131-linux-x64.rpm -y
```
### Download and extract the SonarqQube Server software.
```sh
sudo wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-7.8.zip
sudo unzip sonarqube-7.8.zip
sudo rm -rf sonarqube-7.8.zip
sudo mv sonarqube-7.8 sonarqube
```

## Grant permissions for sonar user to start and manage sonarQube
```sh
sudo chown -R sonar:sonar /opt/sonarqube/
sudo chmod -R 775 /opt/sonarqube/
# start sonarQube server
sh /opt/sonarqube/bin/linux-x86-64/sonar.sh start 
sh /opt/sonarqube/bin/linux-x86-64/sonar.sh status
```

## Go to Maven folder or the folder where we want to perform SonarQube test
```sh


```

## SonarQube default login:
```sh
<<Comment  

SonarQube Configuratoin directory
/opt/sonarqube/conf/sonar.properties
login(username) = admin
     password  = admin 
To change it go to Administrator > Security > users > tokens > generate , and create new token
Go to pom.xml and past the token

        <properties>
                <jdk.version>1.8</jdk.version>
                <spring.version>5.1.2.RELEASE</spring.version>
                <junit.version>4.11</junit.version>
                <log4j.version>1.2.17</log4j.version>
                <sonar.host.url>http:172.31.87.34:9000/</sonar.host.url>
                <sonar.login>8584e56bfe7ef0b01c5c7fa8cb97c9b521b53fe6</sonar.login>
                <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
                <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
        </properties>
Comment

#If needed go to pom.xml > properties and edit/change password,IP, or Port number
<<Commnet

  <properties>
                <jdk.version>1.8</jdk.version>
                <spring.version>5.1.2.RELEASE</spring.version>
                <junit.version>4.11</junit.version>
                <log4j.version>1.2.17</log4j.version>
                <sonar.host.url>http:172.31.87.34:9000/</sonar.host.url>
                <sonar.login>admin</sonar.login>
                <sonar.password>admin</sonar.password>
                <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
                <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
        </properties>

Commnet
```


## Access SonarQube
```sh
#Run mvn package
#Run mvn sonar sonar
#Go to the browser type SonarQube IP:PortNumber

#To Setup roles go to Quality Gates
#To Setup Profiles to to Quality Profile

```


