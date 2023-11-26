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



