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

sh 'mvn clean verify'
 

}
}
 stage('Dependency Check') {
      steps {
          sh 'mvn org.owasp:dependency-check-maven:check -Dformat=XML -DdataDirectory=/usr/share/nvd -DautoUpdate=false'
          step([$class: 'DependencyCheckPublisher', unstableTotalAll: '0'])
        }
      }
 stage ('SonarQube Analysis'){
steps{

withSonarQubeEnv('SonarQube5.3') {
sh 'mvn org.sonarsource.scanner.maven:sonar-maven-plugin:3.2:sonar'

}
}
}
 
}
}
