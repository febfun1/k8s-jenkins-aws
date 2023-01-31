node {

    stage("Git Clone"){

        git branch: 'main', url: 'https://github.com/febfun1/k8s-jenkins-aws.git'
    }

     stage('Gradle Build') {

       sh './gradlew build'

    }

    stage("Docker build"){
        sh 'docker version'
        sh 'docker build -t olu-docker-demo .'
        sh 'docker image list'
        sh 'docker tag olu-docker-demo ajileye/olu-docker-demo:olu-docker-demo'
    }

    withCredentials([credentialsId: 'dockerhub', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
        sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
    }

    stage("Push Image to Docker Hub"){
        sh 'docker push  ajileye/olu-docker-demo:jhooq-docker-demo'
    }
    
    stage("kubernetes deployment"){
        sh 'kubectl apply -f k8s-spring-boot-deployment.yml'
    }
} 
