pipeline{
    agent{
        docker{
            image "grafana/k6"
            args "--entrypoint=''"
        }
    }
    stages{
        stage('version de k6'){
            steps{
                sh 'k6 -v'
            }
            
        }
        stage('run test'){
            steps{
                sh 'k6 run script.js'
            }
        }
    }
}