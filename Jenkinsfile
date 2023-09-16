pipeline {
    agent any

  tools {
        maven 'maven-3'
        jdk "jdk-17"
    }

    stages {
        stage('Start release') {
            steps {
                script {
                    withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'gitlab-tmaszreda', usernameVariable: 'GITHUB_USER', passwordVariable: 'GITHUB_TOKEN']]) {
                        sh "mvn -B -Dusername=${GITHUB_USER} -Dpassword=${GITHUB_TOKEN} release:prepare"
                    }
                }
            }
        }

        stage('Finish release') {
            steps {
                script {
                    withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'gitlab-tmaszreda', usernameVariable: 'GITHUB_USER', passwordVariable: 'GITHUB_TOKEN']]) {
                        sh "mvn -B -Dusername=${GITHUB_USER} -Dpassword=${GITHUB_TOKEN} release:perform"
                    }
                }
            }
        }
    }
}