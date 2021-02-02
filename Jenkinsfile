pipeline{
  agent any
  stages {
    stage('WORKSPACE CleanUP') {
      steps {
        sh "whoami && rm -rf /var/lib/jenkins/workspace/xyz/*"
      }
    }
    stage('SCM CheckOut') {
      steps {
        git credentialsId: 'githubcred', url: 'https://github.com/KennedyDeswal/sampleproject.git' , branch: "master"
      }
    }
    stage("SonarQube Analysis") {
      environment {
        scannerHome = tool 'SonarQubeScanner'
      }
      steps {
        withSonarQubeEnv('sonarqube') {
          sh "${scannerHome}/bin/sonar-scanner"
        }
        timeout(time: 10, unit: 'MINUTES') {
          waitForQualityGate abortPipeline: true
        }
      }
    }
  }
}


