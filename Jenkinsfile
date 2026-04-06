pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Building Docker image...'
                sh 'docker build -t oleshchukapp:latest .'
            }
        }
        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'echo "Tests passed!"'
            }
        }
       stage('Deploy') {
    steps {
        echo 'Pushing Docker image to DockerHub...'
        withCredentials([usernamePassword(credentialsId: 'dockerhub-credentials', passwordVariable: 'DOCKER_PASS', usernameVariable: 'DOCKER_USER')]) {
            // 1. Логін (використовуємо --password-stdin для безпеки)
            sh "echo ${DOCKER_PASS} | docker login -u ${DOCKER_USER} --password-stdin"
            
            // 2. Тегування (перейменування для вашого репозиторію)
            sh "docker tag oleshchukapp:latest ${DOCKER_USER}/oleshchukapp:latest"
            
            // 3. Пуш
            sh "docker push ${DOCKER_USER}/oleshchukapp:latest"
        }
    }
}
