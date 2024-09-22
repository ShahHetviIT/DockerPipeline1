pipeline {
    agent any
    stages {
        stage("checkout") {
            steps {
                checkout scmGit(branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'github', url: 'https://github.com/ShahHetviIT/DockerPipeline1']])
            }
        }
        stage("Build Image") {
            steps {
                script {
                    if (isUnix()) {
                        sh 'docker build -t hetvi0406/dockerpipeline .'
                    } else {
                        bat 'docker build -t hetvi0406/dockerpipeline .'
                    }
                }
            }
        }
        stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'jenkins_id', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) {
                    script {
                        if (isUnix()) {
                            sh 'docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD'
                            sh 'docker push hetvi0406/dockerpipeline'
                            sh 'docker logout'
                        } else {
                            bat 'docker login -u %DOCKERHUB_USERNAME% -p %DOCKERHUB_PASSWORD%'
                            bat 'docker push hetvi0406/dockerpipeline'
                            bat 'docker logout'
                        }
                    }
                }
            }
        }
    }
}