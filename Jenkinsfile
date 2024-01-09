node {
def mavenHome = tool name: "maven3.9.6"
properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])

stage('checkout')
{
git branch: 'development', credentialsId: '08363382-88b7-459f-bb31-4be930642404', url: 'https://github.com/Mavenlearning/maven-web-application.git'	
}
 
 stage('build')
 {
 sh "${mavenHome}/bin/mvn clean package"
 }
 
 stage('executesonarsonarqubereport')
 {
 sh "${mavenHome}/bin/mvn sonar:sonar"
 }
 
 stage('uploadartiintonexus')
 {
 sh "${mavenHome}/bin/mvn deploy"
 }
 
 stage('deploy')
 {
 sshagent(['22196197-cfc1-4764-9dfd-3d9663168082']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@172.31.47.67:/opt/apache-tomcat-9.0.84/webapps"

}
}
 
 }
 
