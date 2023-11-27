![sonar](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/6bc73c73-2d47-43ca-ab4f-6807167363e3)

<pre>
  TABLE OF CONTENTS
Launch Instances
Install Jenkins
Creating a Pipeline in Jenkins Server
Adding a Webhooks
Starting a SonarQube Server
Installing Docker
Password-based Server Connectivity
Building the Image and running the container
</pre>


<h1>Launch Instances</h1>
<p>
  I have created 3 t2.medium instances
  <li>Instance for Jenkins</li>
  <li>Instance for Sonarqube</li>
  <li>Instance for Docker</li>
</p>

![kl](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/c9e8adbe-d2b3-4b53-9753-cbecaa327c8d)

<h1>Install Jenkins</h1>
<p>Update the system</p>
<pre>
  sudo apt update
  clear
</pre>

Now we have to install java first before installing Jenkins
<pre>
  sudo apt install openjdk-11-jre -y
</pre>

Now we have to paste the Jenkins commands
<pre>
   curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee \
   /usr/share/keyrings/jenkins-keyring.asc > /dev/null
   echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
   https://pkg.jenkins.io/debian-stable binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null
  sudo apt-get update
  sudo apt-get install jenkins
</pre>

Now we have to allow port 8080 in the Jenkins server security group inbound settings

![dfa34375-6e63-4d8d-89cb-0f80ac0947b3](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/f2d57f02-4e9e-4a35-baf0-3eff0268e81b)

Now use the public api of instance with port 8080 to view the Jenkins server

![26f464b3-38c6-44a6-8c64-efe30006a062](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/1268d46a-289b-4fa4-8414-9b287b7ce8e3)

Copy the command which was highlighted in the above picture and use the command
<pre>
  sudo cat /var/lib/jenkins/secrets/initialAdminPassword
</pre>

It will show the output a password for the Jenkins server

![b5e9e13c-c112-4a7d-814b-c07d59cc7f54](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/8271624a-7025-4c15-b1cd-cad2b5cbae68)

Copy the password and paste it to the Jenkins server

![8a19b65f-eb48-4207-93e3-50beb321bde0](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/79701bae-1fd1-4c53-9e33-1f4c01eff9c1)

Click on -> Install suggested plugins
<br>
You can set admin credentials

![b3f4de45-9dd9-4bb9-b0c4-484d164cb15b](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/57a3607f-06da-4cd4-b839-c5f30cfd537f)


**Jenkins Installation done**

![041a6a53-4f76-430a-9319-73809d38c2bf](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/cafd5c48-69d0-447d-9914-3ebb24882190)

<h1>Creating a Pipeline in Jenkins Server</h1>
In this, I have selected the Freestyle project

![11c93238-30ac-4bc6-b012-d79f966ee0b4](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/060e8e19-93d7-4693-b47a-f0c1fb958cfd)

In the source code management, I have selected the Git option

![66935e93-ec40-4750-a131-e047a6d8518f](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/263cc9bf-acf7-4acc-9052-7793a71d52b5)

Also select branch of your git

![8775a904-c2b2-4e3f-968e-f417bd256bb9](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/83fdc997-92c0-4ddd-965f-204b6a3bcd8a)

<h1>Adding a Webhooks</h1>

Now open the settings of your Git Repository, select webhooks










