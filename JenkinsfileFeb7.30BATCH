node{
    
    echo "The job name is: ${env.JOB_NAME}"
    echo "The build number is: ${env.BUILD_NUMBER}"
    echo "The node name is: ${env.NODE_NAME}"
    
    properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])
    
def mavenHome = tool name: 'maven3.8.8'
    
stage('CheckoutCode'){
    git branch: 'development', credentialsId: '69301e7e-b78a-4791-ae68-0078dad4f847', url: 'https://github.com/raghuDevopstej/maven-web-application.git'
}

stage('Build'){
    sh "${mavenHome}/bin/mvn clean package"
}

/*
stage('ExecuteSonarQubeReport'){
    sh "${mavenHome}/bin/mvn clean sonar:sonar"
}

stage('UploadArtifactsInNexus'){
    sh "${mavenHome}/bin/mvn clean deploy"
}

stage('DeployAppintoTomcat'){
sshagent(['c1d498af-528c-4384-9213-4a7aa9e7cc68']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@172.31.12.180:/opt/apache-tomcat-9.0.73/webapps"
}
}
*/
}
