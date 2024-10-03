pipeline {
    agent any

    environment {
        KUBECONFIG = credentials('kubeconfig-credentials-id')
    }

    stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Putumerta-collab/Deploy_nginx.git'
            }
        }

        stage('Deploy NGINX') {
            steps {
                script {
                    // Terapkan file deployment dan service ke Kubernetes
                    sh 'kubectl apply -f nginx-deployment.yaml'
                    sh 'kubectl apply -f nginx-service.yaml'
                }
            }
        }

        stage('Verify Deployment') {
            steps {
                script {
                    // Mengecek status deployment
                    sh 'kubectl rollout status deployment/nginx-deployment'
                    // Mendapatkan informasi service
                    sh 'kubectl get svc nginx-service'
                }
            }
        }
    }
}
