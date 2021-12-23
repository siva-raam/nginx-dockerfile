
pipeline {
    agent any
    stages {
        stage('Git Checkout.....................') {
            steps {
                sh 'rm -rf nginx-dockerfile'
                sh 'git clone https://github.com/siva-raam/nginx-dockerfile.git'
            }
        }
        stage('Building Nginx docker image-----------------') {
            steps {
                sh 'cd /var/lib/jenkins/workspace/first-pipeline/nginx-dockerfile/'
                sh 'cp -rvfp /var/lib/jenkins/workspace/first-pipeline/nginx-dockerfile/* /var/lib/jenkins/workspace/first-pipeline/'
                sh 'docker build -t shivaraam/nginx:${BUILD_NUMBER} .'
            }
        }
        stage('Pushing the docker image to docker hub----------------') {
            steps {
                sh 'docker push shivaraam/nginx:${BUILD_NUMBER}'
            }
            
        }
        stage('Deploy the docker container----------------') {
            steps{
                sh 'docker rm -f nginx-web'
                sh 'docker run -dit --name nginx-web -p 8081:80 shivaraam/nginx:${BUILD_NUMBER}'
            }
        }
        stage('Check webapp availability------------------') {
            steps{
                sh 'sleep 10s'
                sh 'curl http://13.232.243.128:8081/'
            }
        }
    }
}
