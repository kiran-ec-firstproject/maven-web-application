node 
{
def mavenID = toolname: "maven_3.8.1"

properties([buildDiscarder(logRotator(artifactDaysToKeepStr: '', artifactNumToKeepStr: '5', daysToKeepStr: '', numToKeepStr: '5')), pipelineTriggers([pollSCM('* * * * *')])])
stage ('checkoutcode')
{
git branch: 'development', credentialsId: '776fc8f5-65a6-40d9-8332-4ea5edf1fa2b', url: 'https://github.com/kiran-ec-firstproject/maven-web-application.git'
}

stage ('BUILD')
{
sh "${mavenID}/bin/mvn clean package"
}

stage ('sonarqubereport')
{
sh "${mavenID}/bin/mvn sonar:sonar"
}
stage ('upload artifacts')
{
sh "${mavenID}/bin/mvn deploy"

}

stage ('deployapppto TOMAcat servers')
{
sshagent(['af933172-928b-48b0-9321-d098e89d8c09']) {
    sh "scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@52.66.237.38:/opt/apache-tomcat-9.0.46/webapps"

}
}

stage ('sending email notification')
{
emailext body: '''buid over 
regards: kiran devops engineer
''', subject: 'BUILD DONE jaffa', to: 'dursetykiran2496@gmail.com'
}


}
