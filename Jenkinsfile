pipeline
{
    agent any
    stages{
        stage('Clone'){
            steps {
               sh '''
               cd /root
               rm -rf front-end-demo
               git clone https://github.com/nagarajui7/front-end-demo.git
               '''
            }
        }
        stage('docker login'){
            steps{
                sh 'docker login --username nagarajubatchu1 --password b@TChU!779263'
            }
        }
        stage('docker image creation'){
            steps{
                sh '''
                cd /root/front-end-demo
                docker build -t nagarajubatchu1/front-end-1-${BUILD_NUMBER} .
                '''
            }
        }
        stage('docker image push'){
            steps{
                sh 'docker push nagarajubatchu1/front-end-1-${BUILD_NUMBER}'
            }
        }
        stage('kubernetes'){
            steps{
                sh '''
                cd /root/
                sed -i "s/front-end-1-.*/front-end-1-${BUILD_NUMBER}/g" complete-demo.yaml
                kubectl create -f complete-demo.yaml
                '''
            }
        }
    }
    
}
