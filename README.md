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

![scre1](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/b1f31e4b-6b68-41eb-b925-7e7cf1cbde7f)

Click to Add Webhook, that time it will ask you to enter your password, <br>
once you enter your password, you're able to add Webhooks.

<br>
<li>Enter the Jenkins URL such as http://35.175.189.203:8080/</li>
<li>and extension github-webhook after the URL</li>



![screen1](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/fbcf9826-3798-4e95-9a07-663da68a10ed)

Click to Add Webhook

![screen2](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/121b110b-c838-47b4-a2db-51126596b1e0)


Now in Build Triggers, select the GitHub hook trigger for GITScm polling <br>
(because this function can trigger the pipeline automatically whenever we make changes to the repository.


<br>

![171388f4-083d-44d5-b14d-ce5fb0a97a2f](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/10261270-bb91-4223-ac7a-bf4db9d445df)

<br>
Click to save.
<br>
Without Webhook I have clicked to Build now and it is working perfectly fine

![404296de-eab1-4716-b32d-dca80826936b](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/536338e6-d101-41d0-906a-1dd72452191a)



Now time to verify Webhooks, I have clicked on the workspace in Jenkins, <br>
and here text.txt file is not present which I am going to create to test the Webhook

![1574a688-abf8-4d83-865f-3ff2f1a44ac7](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/8a751d93-e230-4ac9-af80-298bd3a9b061)


I have visited the Git Repository and created a new file by the name of test.txt


![Capture](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/21b8d1d0-ef66-45ac-bf1b-05073802e276)


I committed the file
<br>
Now I am back to the Jenkins server to check #2 build auto trigger and it is working fine.

![4ae8d251-1475-4e18-ae55-f56265f7a56c](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/871a81cf-706a-4d70-aef8-bbdd98add519)

![26f8a021-1f65-48fb-bca9-143934b82fa9](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/8546315e-ad9f-4c9c-9e6c-f859cca42540)

Now test.txt file is showing in the workspace

![48cb2544-1d36-43e4-a784-c07125771cf7](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/d1502abb-2664-4f20-9fb4-dc734c3f0681)


<h1>Starting a SonarQube Server</h1>
Start the Sonarqube Instance

<pre>
  sudo apt update
  clear
</pre>

We need to install Java on the server but 17 version earlier we were using 11 version

<pre>
  sudo apt install openjdk-17-jre -y
</pre>

Search for the SonarQube website and download the community for the free version<br>

SonarQube Download Copy the link and paste it to the terminal of the SonarQube Instance

<br>

![a097c83d-a980-4906-9279-763b2e385ea7](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/88c535bf-007b-4631-9753-1c30feead73d)

<pre>sudo adduser sonarqube
</pre>

![4a6cc6dc-fb48-4645-9548-bced7f50ccec](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/049ca112-76fc-4a3e-bdb3-24d789e6cbe8)

Use the command below with wget

<pre>
  wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-9.4.0.54424.zip
</pre>


![17688fc3-752f-4eb5-8afb-e59d487c385c](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/34a0faf3-461e-4c94-bde2-6a6f114297ca)


<pre>
  sudo apt install unzip
  unzip *
  ls
</pre>

Now the unzipped file is showing

![9d2ee9e6-e2d5-4dde-8f2c-7c98ff07db5b](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/878f451f-58ad-48e0-a673-60be2213296b)

<pre>
  cd sonarqube-9.4.0.54424 
ls
</pre>

![7652b9ab-5f85-47dc-a623-74beec0c2a52](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/f84ac169-c437-4530-813c-55e02c6f738f)


Go to the bin folder
<pre>
  cd bin
  cd linux-x86-64
  ls
</pre>
![c611fd78-564a-4f99-b1a5-3022d670b404](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/1724531e-3afa-4a83-8852-b5e6c08f64fe)


Now start the sonar server by using the command

<pre>./sonar.sh start</pre>

And also we need to port 9000 in the inbound setting of the security group

![f71b771d-2e6b-4222-9fba-16257693f97c](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/569052ab-1e16-4654-8e43-f77c09045cf8)


Now it's time to check the URL http://54.88.67.190:9000/

![aebca526-2027-4d5e-9db1-6669e38a6e0f](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/bcfe9563-63d1-4ee2-bc59-df1a75cd6617)

Update the password

![eb284491-e258-4175-b1fa-426dc7d1ecf7](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/d0b60e2e-7deb-4765-b9a3-05c633e4324f)

After updating the password we can access the Sonarqube

<h1>Follow Me on GitHub for more Projects</h1>

![c357ffa8-b7b4-456a-b0e8-38b0d8e5c32e](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/72c25d73-dc11-4063-8995-206b27115e52)

Now I have selected the project type Manually

![3e18d31f-db24-42e8-9acc-ead266df5dac](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/a2dda2b2-2a10-4086-baac-afe3617c8741)

After this, I have selected the CI platform, Jenkins

![437ac7bb-2cc7-45d2-8bcd-e5c174a7b181](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/3f1ad367-d055-435b-91d3-a638b494866c)

Selected the DevOps platform GitHub

![e77a9a76-7892-499e-b0ec-6ce9361916ed](https://github.com/samsorrahman/Jenkins-SonarQube-Docker/assets/112087807/9c21c00c-c355-48fa-99f3-210e329cd12b)









