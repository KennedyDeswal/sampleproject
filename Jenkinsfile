pipeline{
    agent any
    environment{
                 qg = waitForQualityGate()
                 jn = "${env.JOB_NAME}"
                 ws = "${env.WORKSPACE}"

                }

    stages{
       
        stage('dev-cleaning workinf dir'){
        
            steps{sh "sudo rm -rf /var/lib/jenkins/workspace/xyz/*"}
        }
        stage('dev-clone'){
          
            steps{git credentialsId: 'githubcred', url: 'https://github.com/KennedyDeswal/sampleproject.git' , branch: "master"}
        }

       stage("SonarQube analysis") {
                steps{
                  withSonarQubeEnv('sonar_scanner') {
                  sh 'cd /var/lib/jenkins/workspace/xyz && /opt/sonar_scanner/bin/sonar-scanner -Dsonar.sources=. -Dsonar.projectKey=project'
             }
         }
      }
      stage("Quality Gate"){
                steps{
                     timeout(time: 1, unit: 'HOURS') {
                     //if (qg.status != 'OK') {
                     error "Pipeline aborted due to quality gate failure: ${qg.status}"
              }
          }
      }
