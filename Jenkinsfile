pipeline{
    agent any
    stages{
        stage("Build Docker image"){
            steps{
                echo "Build Docker image"
                bat "docker build -t kubdemoapp:v1 ."
            }
        }
        stage("Docker Login"){
            steps{
                bat "docker login -u shivanibonagiri -p E25cbi3u@"
            }
        }
        stage("push Docker image to docker hub"){
            steps{
                echo "push Docker image to docker hub"
                bat "docker tag kubdemoapp:v1 shivanibonagiri/kubernetes:t1"
                bat "docker push shivanibonagiri/kubernetes"
            }
        }
        stage("Deploy to kubernetes"){
            steps{
                echo "Deploy to kubernetes"
                bat "kubectl apply -f deployment.yaml --validate=false"
                bat "kubectl apply -f service.yaml"
            }
        }
    }
    post{
        success{
            echo "Pipeline executed successfully"
        }
        failure{
            echo "pipeline failed.Please check the logs"
        }
    }
}