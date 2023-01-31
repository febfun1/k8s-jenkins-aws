node {

    stage("Git Clone"){

        git credentialsId: 'GIT_HUB_CREDENTIALS', url: 'https://github.com/rahulwagh/k8s-jenkins-aws'
    }

     stage('Gradle Build') {

       sh './gradlew build'

    }

    stage("Docker build"){
        sh 'docker version'
        sh 'docker build -t olu-docker-demo .'
        sh 'docker image list'
        sh 'docker tag ajileye-docker-demo ajileye/olu-docker-demo:olu-docker-demo'
    }

    withCredentials([string(credentialsId: 'dockerhub', variable: 'PASSWORD')]) {
        sh 'docker login -u febfun1 -p $PASSWORD'
    }

    stage("Push Image to Docker Hub"){
        sh 'docker push  ajileye/olu-docker-demo:jhooq-docker-demo'
    }
    
    stage("kubernetes deployment"){
        sh 'kubectl apply -f k8s-spring-boot-deployment.yml'
    }
} 
