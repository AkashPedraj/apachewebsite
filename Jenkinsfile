pipeline {
    agent any
    environment {
        DOCKER_IMAGE = 'akashdeveloper001/apachewebsite:latest'
        KUBECONFIG = credentials('kubeconfig')
    }
    stages {
        stage('Clone Git repository') {
            steps {
                git 'https://github.com/AkashPedraj/apachewebsite.git'
            }
        }
        stage('run ansibleplaybook'){
            steps{
                ansiblePlaybook credentialsId: 'ansible-ssh', installation: 'ansible2', inventory: 'inventory.ini', playbook: 'installapche.yml', vaultTmpPath: ''
            }
        }
        stage('Docker Build & Push') {
            steps {
                script {
                    withDockerRegistry([credentialsId: 'docker', url: 'https://index.docker.io/v1/']) {
                        sh '''
                        docker build --no-cache -t $DOCKER_IMAGE -f Dockerfile .
                        docker push $DOCKER_IMAGE
                        '''
                    }
                }
            }
        }
        stage('Deploy to Kubernetes') {
            steps {
                script {
                    withCredentials([file(credentialsId: 'kubeconfig', variable: 'KUBECONFIG_FILE')]) {
                        sh '''
                        export KUBECONFIG=$KUBECONFIG_FILE
                        kubectl apply -f deployment.yml
                        kubectl apply -f service.yml
                        '''
                    }
                }
            }
        }
    }
}
