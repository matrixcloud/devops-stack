pipeline {
    agent any
    stages {
        stage('Print Env') {
            steps {
                sh 'printenv'
            }
        }
    }
    post {
        success {
            gerritReview labels: ['Code-Style': 1]
            gerritReview labels: [Verified: 1]
        }
        unstable { 
            gerritReview labels: ['Code-Style': 0], message: 'Check Style is unstable'
            gerritReview labels: [Verified: 0], message: 'Build is unstable' 
        }
        failure {
            gerritReview labels: [Verified: -1]
            gerritReview labels: ['Code-Style': -1]
        }
    }
}