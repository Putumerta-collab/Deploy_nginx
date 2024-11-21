pipeline {
    agent any

    environment {
        KUBECONFIG = credentials('kubeconfig-credentials-id')  // Kredensial untuk kubeconfig
    }

    stages {

        stage('Checkout Source') {
            steps {
                // Mengambil kode dari repository dan memastikan branch 'main' digunakan
                git branch: 'main', url: 'https://github.com/Putumerta-collab/Deploy_nginx.git'
            }
        }

        stage('Deploy NGINX') {
            steps {
                script {
                    // Menerapkan file deployment dan service YAML ke Kubernetes
                    sh 'kubectl apply -f nginx-deployment.yaml'
                    sh 'kubectl apply -f nginx-service.yaml'
                }
            }
        }
    }

    post {
        always {
            // Menampilkan status semua pods di akhir build, baik berhasil maupun gagal
            script {
                sh 'kubectl get pods'
            }
        }
    }
}
