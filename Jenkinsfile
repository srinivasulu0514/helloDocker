pipeline {
agent any
stages{
    stage ('Checkout GitHub repo') {
        steps {
            checkout scmGit(branches: [[name: '*/main']], extensions:[], userRemoteConfigs: [[url:"https://github.com/srinivasulu0514/dockerdemo"]])
        }
    }
    stage("Build and Tag Docker Image") {
        steps {
            script {
                sh 'docker build. -t hellodocker'
                sh 'docker tag hellodocker srinivasulu0514/dockervasu)'
                }
            }
    }
    stage ("Push the Docker Image to DockerHUb"){
        steps {
            script {
                withCredentials([string(credentialsId:'docker_hub',variable:'docker_hub')]){
                sh 'docker login -u vasyvasf@gmail.com -p ${docker_hub}'
                sh 'docker push srinivasulu0514/dockervasu'
                }
            }
        }
    }
    stage('Deploy deployment and service file'){
        steps{
            script{
                kubernetesDeploy configs: 'deploymentsvc.yaml',kubeconfigId:'k8_auth'
            }
        }
    }
}
}

