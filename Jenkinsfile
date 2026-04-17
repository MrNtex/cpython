pipeline {
    agent any

    stages {
        stage('Build Builder Image') {
            steps {
                script {
                    sh 'docker build -f Dockerfile.build -t cpython-builder:${BUILD_NUMBER} -t cpython-builder:latest .'
                }
            }
        }

        stage('Build Deploy Image') {
            steps {
                sh "docker build -f Dockerfile.deploy -t cpython-deploy:3.13-build${env.BUILD_NUMBER} ."
            }
        }

        stage('Smoke Test') {
            steps {
                sh "docker run --rm cpython-deploy:3.13-build${env.BUILD_NUMBER} ./python -c \"print('Smoke test przeszedl pomyslnie!')\""
            }
        }
    }
}
