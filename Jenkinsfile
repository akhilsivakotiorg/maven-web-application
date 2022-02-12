node
{
    
    def mavenHome = tool name:"maven3.8.4"
    
stage('CheckoutCode')
   {
   git branch: 'development', credentialsId: 'be511f15-4cc8-4dfc-b11c-0322b410022d', url: 'https://github.com/akhilsivakotiorg/maven-web-application.git'
   }
stage('Build')
   {
   sh "${mavenHome}/bin/mvn clean package"
   } 
 stage ('Executesonarqubereport')
 {
     sh "${mavenHome}/bin/mvn sonar:sonar"
 }
 stage ('uploadartifactintoNexusRepository')
 {
     sh "${mavenHome}/bin/mvn deploy "
 }
 stage('upload into tomccat server')
 {
     
 }
}
