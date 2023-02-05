node {

    stage("Git Clone"){

        git branch: 'main', url: 'https://github.com/febfun1/k8s-jenkins-aws.git'
    }

     stage('Gradle Build') {

       sh './gradlew build'

    }

    stage("Docker build"){
        sh 'docker version'
        sh 'docker build -t febfun/app-deploy1 .'
        sh 'docker image list'
        sh 'docker tag febfun/app-deploy1 febfun/app-deploy1:app-deploy'
    }

    withCredentials([string(credentialsId: 'DOCKER_HUB_PASSWORD', variable: 'PASSWORD')]) {
        sh 'docker login -u febfun -p $PASSWORD'
    }

    stage("Push Image to Docker Hub"){
        sh 'docker push  febfun/app-deploy1:app-deploy'
    }
    
    stage("kubernetes deployment"){
        sh 'kubectl apply -f k8s-spring-boot-deployment.yml'
    }
} 
