pipeline{
  agent any
  environment {
    qg = waitForQualityGate()
    jn = "${env.JOB_NAME}"
    ws = "${env.WORKSPACE}"
  }
  stages {
    stage('WORKSPACE CleanUP') {
      steps {
        sh "sudo rm -rf /var/lib/jenkins/workspace/xyz/*"
      }
    }
    stage('SCM CheckOut') {
      steps {
        git credentialsId: 'githubcred', url: 'https://github.com/KennedyDeswal/sampleproject.git' , branch: "master"
      }
    }
    stage("test") {
      steps {
        sh 'echo "Test"'
      }
    }
  }
}


