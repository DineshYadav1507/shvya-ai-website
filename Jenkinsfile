pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Checking out source code...'
                checkout scm
            }
        }

        stage('List Files') {
            steps {
                sh 'ls -R'
            }
        }

        stage('Validate index.html') {
            steps {
                script {
                    if (!fileExists('index.html')) {
                        error "index.html not found! ❌"
                    } else {
                        echo "index.html found. ✅"
                    }
                }
            }
        }

        stage('Archive Full Site (Deploy Package)') {
            steps {
                echo 'Archiving full static site (HTML, CSS, JS)...'
                archiveArtifacts artifacts: '**/*', fingerprint: true, onlyIfSuccessful: true
            }
        }
    }

    post {
        success {
            echo 'Build Succeeded ✅'
        }
        failure {
            echo 'Build Failed ❌'
        }
    }
}

