pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'mvn clean package'
            }
        }
    }
    post { 
        always { 
            echo 'I will always say Hello again!'
        }
    }
}
