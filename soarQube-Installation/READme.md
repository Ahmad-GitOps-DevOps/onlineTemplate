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
sudo hostname sonar

```

### Install Java JDK 1.8+

``` sh
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


## Integrate SonarQube to Manven
```sh
<<Comment to integrate SonarQube to Manven we need to be authticate by going MavenServer > project folder > pom.xml > properties > change the app address/portNumber and add login details for sonarQube server
Comment
```

## SonarQube default login:
```sh
<<Comment  
login(username) = admin
      password  = admin

To change the password to token go to Administrator > Security > users > tokens > generate , and create new token
Go to pom.xml and past the token
Comment

```
## SonarQube Configuratoin directory > /opt/sonarqube/conf/sonar.properties

## Access SonarQube
```sh
#Run mvn package
#Run mvn sonar sonar
#Go to the browser type SonarQube IP:PortNumber

#To Setup roles go to Quality Gates
#To Setup Profiles to to Quality Profile

```


