pipeline {
    agent {
        docker { image 'cimg/android:2023.09.1' }
    }

    stages {
        stage('Setup') {
            steps {
                sh 'chmod +x ./gradlew'
            }
        }
        stage('Build') {
            steps {
                sh './gradlew build'
            }
        }
        stage('Run tests') {
            steps {
                sh './gradlew test'
            }
        }
    }
    post {
        success {
            // Archive the specific APK file after a successful build
            archiveArtifacts allowEmptyArchive: true, artifacts: '**/*.apk', followSymlinks: false
        }
        always {
            cleanWs()
        }
    }
}
