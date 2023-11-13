pipeline {
    agent {
        docker {
            image 'node:16-buster-slim' // menggunakan image docker
            args '-p 3000:3000'    // memakai port 3000 ke container
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'npm install' // intsall depedensi npm
            }
        }
        stage('Test') {
            steps {
                sh './jenkins/scripts/test.sh' // menjalankan pengujian 
            }
        }
        stage('Manual Approval') {
            steps {
                input message: 'Lanjutkan ke tahap Deploy?' // menunggu persetujuan untuk melanjutkan ke tahap selanjutnya
            }
        }
        stage('Deploy') {
            steps {
                sh './jenkins/scripts/deliver.sh' // menjalankan script pengiriman
                script {
                    // Tunggu selama 1 menit
                    sleep time: 60, unit: 'SECONDS'
                }
                sh './jenkins/scripts/kill.sh' // menjalankan script kill untuk memberhentikan
            }
        }
    }
}
