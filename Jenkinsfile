node 
{
    def mavenHome = tool name: "maven3.8.1"
    properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), pipelineTriggers([pollSCM('* * * * *')])])
    stage('CHECKOUT CODE')
    {
       git branch: 'development', credentialsId: '776fc8f5-65a6-40d9-8332-4ea5edf1fa2b', url: 'https://github.com/kiran-ec-firstproject/maven-web-application.git'
    }
    stage(' BUILD')
    {
       sh "${mavenHome}/bin/mvn clean package" 
    }
  /*
     stage(' SONARQUBE REPORT')
    {
       sh "${mavenHome}/bin/mvn sonar:sonar" 
    }
    stage(' nexus ARTIFACTS')
    {
       sh "${mavenHome}/bin/mvn deploy" 
    }
    stage ('deployapppto TOMAcat servers')
{
sshagent(['af933172-928b-48b0-9321-d098e89d8c09']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@13.232.71.8:/opt/apache-tomcat-9.0.46/webapps"

}
}
*/
stage ('sending email notification')
{
emailext body: '''buid over 
regards: kiran devops engineer
''', subject: 'BUILD DONE jaffa', to: 'dursetykiran2496@gmail.com'
}

}
