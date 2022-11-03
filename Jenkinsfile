pipeline {
    agent any
    triggers{
        pollSCM('H/2 * * * *')
    }
    stages {
        stage('checkout'){
            when { changeset "testchart/*" } // Name of folder with Helm Charts to search for changes in
            steps{
                checkout scm
                cleanWs()
                sh 'git clone git@github.com:piotrowsianko/jenkins-job-helm.git .'} //test step
            }

        
        }
    }
