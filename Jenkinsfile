node {
    docker.image('node:lts-buster-slim').inside('-p 3000:3000'){
        withEnv(['CI=true']){
            stage('Install'){
                git branch: "react-app", url: 'https://github.com/Arrizki16/a428-cicd-labs.git'
            }
            stage('Build') { 
                sh 'npm install' 
            }
            stage('Test') {
                sh './jenkins/scripts/test.sh'
            }
            stage('Manual Approval') {
                input message: 'Lanjutkan ke tahap Deploy? (Klik "Proceed" untuk mengakhiri)'
            }
            stage('Deploy') {
                sh './jenkins/scripts/deliver.sh'
                sleep(60)
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}