pipeline {
    agent any
    tools {
        gradle "Gradle-8"
    }
    stages {
        stage('clone repository') {
            steps {
                git 'https://github.com/AlbertineN/java-todo'
            }
        }
        stage('Build project') {
            steps {
                sh 'gradle build'
            }
        }
        stage('Test'){
            steps {
                sh 'gradle test'
            }
        }
        stage('Email notification on build and test'){
            steps{
               mail bcc: '', body: 'Successful build and test complete. Systems go for deployment. ', cc: '', from: '', replyTo: '', subject: 'Build and test sucess', to: 'albertinengingan@gmail.com,albertinenginga@gmail.com'
            }
        }
        stage('Deploy to Heroku') {
            steps {
                withCredentials([usernameColonPassword(credentialsId: 'javatodo', variable: 'HEROKU_CREDENTIALS')]){
                sh 'git push https://${HEROKU_CREDENTIALS}@git.heroku.com/polar-bayou-12504.git master'
                }
            }
        }
        stage('slack notification'){
            steps{
                slackSend channel: ' #slack-intergration ', color: '#008000', message: 'sucessfully deployed to heroku. link:https://polar-bayou-12504.herokuapp.com/', teamDomain: 'projectsdevop-ddy1039', tokenCredentialId: 'slack-jenkins'
            }
        }

    }
}}
