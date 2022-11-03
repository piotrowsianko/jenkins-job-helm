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
                helm package testchart
                gcloud auth application-default print-access-token | helm registry login -u oauth2accesstoken --password-stdin https://europe-central2-docker.pkg.dev/my-test-project-owspio/helm-chart-repo
                helm push testchart-0.1.0.tgz oci://europe-central2-docker.pkg.dev/my-test-project-owspio/helm-chart-repo
                
                '''

            }
        }
        
        }
    }
