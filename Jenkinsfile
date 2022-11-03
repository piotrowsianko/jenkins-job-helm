pipeline {
    agent any

    stages {
        when { changeset "testchart/*" }
        stage('checkout'){
            steps{
                checkout scm
                cleanWs()
                sh 'git clone git@github.com:piotrowsianko/jenkins-job-helm.git .'}
            }
        
        }
    }
}