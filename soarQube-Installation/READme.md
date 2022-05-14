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
sudo yum install wget git nano unzip -y
sudo yum install java-11-openjdk-devel java-1.8.0-openjdk-devel -y
```
### Download and extract the SonarqQube Server software.
```sh
sudo wget http://download.sonatype.com/nexus/3/nexus-3.15.2-01-unix.tar.gz 
sudo tar -zxvf nexus-3.15.2-01-unix.tar.gz
sudo mv /opt/nexus-3.15.2-01 /opt/nexus
sudo rm -rf nexus-3.15.2-01-unix.tar.gz
```

## Grant permissions for sonar user to start and manage sonarQube
```sh

# Change the owner and group permissions to /opt/nexus and /opt/sonatype-work directories.
sudo chown -R nexus:nexus /opt/nexus
sudo chown -R nexus:nexus /opt/sonatype-work
sudo chmod -R 775 /opt/nexus
sudo chmod -R 775 /opt/sonatype-work

```
## change from #run_as_user="" to [ run_as_user="nexus" ]
```sh
nano /opt/nexus/bin/nexus.rc
sudo echo run_as_user="nexus" > nexus.rc

```
## CONFIGURE NEXUS TO RUN AS A SERVICE
```sh
sudo ln -s /opt/nexus/bin/nexus /etc/init.d/nexus

#9 Enable and start the nexus services
sudo systemctl enable nexus
sudo systemctl start nexus
sudo systemctl status nexus
echo "end of nexus installation"

```

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


