node{

eco "Job Name is: ${env.JOB_NAME}"
eco "Node Name is:${env.NODE_NAME}"

def mavenHome = tool name: 'maven3.8.4'

//Get the code from Github Repo 
stage('CheckoutCode'){
git branch: 'development', credentialsId: 'e446d7ee-fb7b-47d6-ace7-966f174c819f', url: 'https://github.com/srilatha777/maven-web-application.git'
}

//Do the build by using maven build tool
stage('Build'){
sh "${mavenHome}/bin/mvn clean package"
}

//Execute the SonarQube report
stage('ExecuteSonarQubeReport'){
sh "${mavenHome}/bin/mvn sonar:sonar"

}

//Upload Artifacts into Artifactory Repo
stage('UploadArtifactsintoNexus'){
sh "${mavenHome}/bin/mvn deploy"
}

//Deploy Application into Tomcat Server
stage('DeployApplicationIntoTomcatServer'){
sshagent(['6f9f4626-e18c-49bd-af50-4672619503bf']) {
  sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.233.99.240:/opt/apache-tomcat-9.0.63/webapps/" 
}
}

}









