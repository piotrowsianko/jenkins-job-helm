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
        stage('Helm'){
            when { changeset "testchart/*"} // Name of folder with Helm Charts to search for changes in
            steps{
                sh '''
                export GOOGLE_APPLICATION_CREDENTIALS=/mnt/c/Users/piotr.owsianko/Downloads/my-test-project-owspio-4d03fcfd448c.json
                helm package testchart 
                gcloud auth application-default print-access-token | helm registry login -u oauth2accesstoken --password-stdin https://europe-central2-docker.pkg.dev/my-test-project-owspio/helm-chart-repo
                helm push testchart*.tgz oci://europe-central2-docker.pkg.dev/my-test-project-owspio/helm-chart-repo
                '''
            }
        }
        
        }
    }
