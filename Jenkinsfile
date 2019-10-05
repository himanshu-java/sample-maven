pipeline {
agent any
 
tools{
maven 'maven 3'
jdk 'java 8'
}
 
stages {
stage ("initialize") {
steps {
sh '''
echo "PATH = ${PATH}"
echo "M2_HOME = ${M2_HOME}"
'''
}
}
 stage ('Build project') {
steps {
dir("project_templates/java_project_template"){
sh 'mvn clean verify'
 
}
}
}
 stage ('SonarQube Analysis'){
steps{
dir("project_templates/java_project_template"){
withSonarQubeEnv('SonarQube5.3') {
sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar'
}
}
}
}
}
}
