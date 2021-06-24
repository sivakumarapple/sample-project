# maven-project

Simple Maven Project

This is a simple CICD Pileline project by using Jenkins, Maven, Docker, Nexus and Sonarqube.

Launch 2 EC2 Instances (t2.micro and t3a.medium)

On t2.micro:-
Install GIT:- yum install git -y
	git clone https://github.com/Debasish960/my-project.git

Install JAVA:- yum install java-1.8.0-openjdk-devel -y
---------------------------------------------------


Install Maven:-
	mkdir /opt/maven && cd /opt/maven
	wget https://downloads.apache.org/maven/maven-3/3.8.1/binaries/apache-maven-3.8.1-bin.tar.gz
	tar -xvf apache-maven-3.8.1-bin.tar.gz
	vi /etc/profile.d/maven.sh

	export M2_HOME=/opt/maven/apache-maven-3.8.1
	export PATH=${M2_HOME}/bin:${PATH}
	mvn -version
  
  
  
  Install JENKINS:-
	yum -y install wget
	wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
	rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
	yum -y install jenkins

	Start Jenkins
	# Start jenkins service
	systemctl start jenkins

	# Setup Jenkins to start at boot,
	systemctl enable jenkins

	Accessing Jenkins
	By default jenkins runs at port 8080, You can access jenkins at

	http://YOUR-SERVER-PUBLIC-IP:8080
  
  
  
  Install DOCKER:-
	yum install docker -y
	usermod -aG docker jenkins
	usermod -aG docker ec2-user
	service jenkins restart
  
  
  accessing nexus
  
  Configuring Nexus as a Maven repo
What we will do:
– create a private (hosted) repository for our snapshots
– create a private (hosted) repository for our releases
– create a proxy repository pointing to Maven Central
– create a group repository to provide all of these repos under a single UR

https://blog.sonatype.com/using-nexus-3-as-your-repository-part-1-maven-artifacts

Add in project's pom.xml

  <distributionManagement>
    <repository>
      <id>my-project</id>
      <url>http://65.2.116.192:8081/nexus/content/repositories/maven-host-release</url>
    </repository>
    <snapshotRepository>
      <id>my-project</id>
      <url>http://65.2.116.192:8081/nexus/content/repositories/maven-host-snapshot</url>
    </snapshotRepository>
  </distributionManagement>

vi /opt/maven/apache-maven-3.6.3/conf

<server>
  <id>my-project</id>
  <username>admin</username>
  <password>admin123</password>
</server>

mvn deploy
 
  
  Accessing SonarQube
Nexus runs at port 9000, You can access Nexus at 
Configuring SonarQube project
What we will do:
 create a project
 Generate Token
 Select Maven 
 
 mvn sonar:sonar 

