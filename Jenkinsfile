pipeline {
    agent any

    stages {
        stage('checkout'){
            when { changeset "testchart/*" }
            steps{
                checkout scm
                cleanWs()
                sh 'git clone git@github.com:piotrowsianko/jenkins-job-helm.git .'}
            }
        
        }
    }
