node {

    stage("Git Clone"){

        git branch: 'main', url: 'https://github.com/febfun1/k8s-jenkins-aws.git'
    }

     stage('Gradle Build') {

       sh './gradlew build'

    }

    stage("Docker build"){
        sh 'docker build -t olu-docker-demo:${BUILD_NUMBER} .'
    }
    
    stage("Push"){
       
    withCredentials([credentialsId: 'dockerhub', passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {
        sh 'docker login -u $DOCKER_USERNAME -p $DOCKER_PASSWORD'
        
        sh 'docker push olu-docker-demo:$BUILD_NUMBER'
    }
    
    stage("kubernetes deployment"){
        sh 'kubectl apply -f k8s-spring-boot-deployment.yml'
    }
} 
