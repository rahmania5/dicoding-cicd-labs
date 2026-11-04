node {
    // fetch source from the repo this job is configured with
    checkout scm
    // run all stages inside node container
    docker.image('node:26-trixie-slim').inside('-p 3000:3000') {
        // install dependencies
        stage('Build') {
            sh 'npm clean-install'
        }
        // run test script
        stage('Test') {
            sh './jenkins/scripts/test.sh'
        }
        stage('Deploy') {
            steps {
                sh './jenkins/scripts/deliver.sh'
                input message: 'Sudah selesai menggunakan React App? (Klik "Proceed" untuk mengakhiri)'
                sh './jenkins/scripts/kill.sh'
            }
        }
    }
}
