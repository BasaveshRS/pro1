pipeline {
    agent any
    stages{
        stage('build project'){
            steps{
                git url:'https://github.com/BasaveshRS/pro1.git', branch: "master"
                sh 'mvn clean package'
              
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t basaveshrs21/staragileprojectfinance:v1 .'
                    sh 'docker images'
                }
            }
        }
		 stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push basaveshrs21/staragileprojectfinance:v1'
                }
            }
        }
     stage('Deploy') {
            steps {
                sh 'sudo docker run -itd --name My-first-containe21211 -p 8083:8081 basaveshrs21/staragileprojectfinance:v1'
                  
                }
            }
        
    }
}
