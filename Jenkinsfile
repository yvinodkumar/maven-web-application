node{

echo "Job Name is:  ${env.JOB_NAME}"
echo "Node Name is:  ${env.NODE_NAME}"

 def mavenHome = tool name: "maven3.8.4"
 
//Get the code from the Github Repo
stage('CheckoutCode'){
git branch: 'development', credentialsId: '5787ed9e-0ff9-4c43-96f8-304c6cdfc0e2', url: 'https://github.com/srilatha777/maven-web-application.git'
}

//Do the build by using Maven Build tool
stage('Build'){
sh "${mavenHome}/bin/mvn clean package"
}

//Execute SonarQube Report
stage('ExecuteSonarQubeReport'){
sh "${mavenHome}/bin/mvn sonar:sonar"    
}   

//Upload Artifacts into Artifactory Repo
stage('UploadArtifactsIntoNexus'){
    sh "${mavenHome}/bin/mvn deploy"
}

//Deploy Application into Tomcat server
stage('DeployApplicationIntoTomcatServer'){
sshagent(['6f9f4626-e18c-49bd-af50-4672619503bf']) {
 sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.232.34.158:/opt/apache-tomcat-9.0.63/webapps/" 
}
}    
}







    
    
    
    
    
    
