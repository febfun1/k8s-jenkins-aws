node {

    stage("Git Clone"){

        git branch: 'main', url: 'https://github.com/febfun1/k8s-jenkins-aws.git'
    }

     stage('Gradle Build') {

       sh './gradlew build'

    }

    stage("Docker build"){
        sh 'docker version'
        sh 'docker build -t febfun/docker-demo .'
        sh 'docker image list'
        sh 'docker tag docker-demo febfun/docker-demo:docker-demo'
    }

    withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'PASSWORD')]) {
        sh 'docker login -u febfun -p $PASSWORD'
    }

    stage("Push Image to Docker Hub"){
        sh 'docker push  febfun/docker-demo:docker-demo'
    }
    
    stage("kubernetes deployment"){
        sh 'kubectl apply -f k8s-spring-boot-deployment.yml'
    }
} 
