pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                // sh 'npm test'
                /* sh 'npm run test:ci' */
                sh 'npm run build'
            }
        }
    }
}
