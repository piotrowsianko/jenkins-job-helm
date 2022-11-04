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

        stage('Input Helm version number'){
            when { changeset "testchart/*"} // Name of folder with Helm Charts to search for changes in
            steps{
                script {
                    env.CHART_VERSION = input message: 'Please enter valid HELM CHART version',
                                        parameters: [string(defaultValue: '',
                                                    description: '',
                                                    name: 'Version')]
                }
            }
        }
        stage('Helm'){
            when { changeset "testchart/*"} // Name of folder with Helm Charts to search for changes in
            steps{
                sh """sed -i 's/_CHART_VERSION_/"${CHART_VERSION}"/' testchart/Chart.yaml"""
                sh '''
                export GOOGLE_APPLICATION_CREDENTIALS=/mnt/c/Users/piotr.owsianko/Downloads/my-test-project-owspio-4d03fcfd448c.json
                helm package testchart 
                cat /mnt/c/Users/piotr.owsianko/Downloads/my-test-project-owspio-4d03fcfd448c.json | helm registry login -u _json_key --password-stdin https://europe-central2-docker.pkg.dev
                helm push testchart*.tgz oci://europe-central2-docker.pkg.dev/my-test-project-owspio/helm-chart-repo
                '''
            }
        }
        
        }
    }
 