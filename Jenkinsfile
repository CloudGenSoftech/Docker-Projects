node{
    stage('git checkout'){
        git 'https://github.com/CloudGenSoftech/Docker-Projects.git'
    }
    stage('Docker Build Image'){
        sh 'docker image build -t $JOB_NAME:v1.$BUILD_ID .'
        sh 'docker image tag $JOB_NAME:v1.$BUILD_ID thanish/$JOB_NAME:v1.$BUILD_ID'
        sh 'docker image tag $JOB_NAME:v1.$BUILD_ID thanish/$JOB_NAME:latest'
    }
    stage('Pushing the Docker image to Docker HUB')
    {
        withCredentials([string(credentialsId: 'DockerPasswd', variable: 'DockerPasswd')]) {
           sh "docker login -u thanish -p ${DockerPasswd}"
           sh 'docker image push thanish/$JOB_NAME:v1.$BUILD_ID'
           sh 'docker image push thanish/$JOB_NAME:latest'
           sh 'docker image rm $JOB_NAME:v1.$BUILD_ID thanish/$JOB_NAME:v1.$BUILD_ID  thanish/$JOB_NAME:latest'
            
        }

    }
}
