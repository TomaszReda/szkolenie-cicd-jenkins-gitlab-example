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
                    withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'github-id', usernameVariable: 'GITHUB_USER', passwordVariable: 'GITHUB_TOKEN']]) {
                        sh "mvn -B -Dusername=${GITHUB_USER} -Dpassword=${GITHUB_TOKEN} release:prepare"
                    }
                }
            }
        }

        stage('Finish release') {
            steps {
                script {
                    withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: '69cf887a-1206-4c7d-98c1-cfb1a41b7d72', usernameVariable: 'GITHUB_USER', passwordVariable: 'GITHUB_TOKEN']]) {
                        sh "mvn -B -Dusername=${GITHUB_USER} -Dpassword=${GITHUB_TOKEN} release:perform"
                    }
                }
            }
        }

   stage('Clean repository') {
                    steps {
                        cleanWs()
                    }
                }

    }
}