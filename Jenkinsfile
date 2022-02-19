node
{
   properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), [$class: 'JobLocalConfiguration', changeReasonComment: ''], pipelineTriggers([pollSCM('* * * * *')])])
    
    def mavenHome = tool name:"maven3.8.4"
    
stage('CheckoutCode')
   {
   git branch: 'development', credentialsId: 'be511f15-4cc8-4dfc-b11c-0322b410022d', url: 'https://github.com/akhilsivakotiorg/maven-web-application.git'
   }
stage('Build')
   {
   sh "${mavenHome}/bin/mvn clean package"
   } 
   /*
 stage ('Executesonarqubereport')
 {
     sh "${mavenHome}/bin/mvn sonar:sonar"
 }
 
 */
 stage ('uploadartifactintoNexusRepository')
 {
     sh "${mavenHome}/bin/mvn deploy "
 }
 stage('upload into tomccat server')
 {
     sshagent(['80ff57a2-6586-4a60-8de4-f52d67eb661a']) 
     {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.234.136.139:8080:/opt/apache-tomcat-9.0.58/webapps/"


      }
     
 }
}
