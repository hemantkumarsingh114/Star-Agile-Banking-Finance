pipeline{
    agent any
    stages{
        stage('1. Checkout the Code from GITHUB'){
            steps{
                 git url: 'https://github.com/hemantkumarsingh114/Star-Agile-Banking-Finance/'
                 echo 'github url checkout'
            }
        }
        stage('2. Code Compile with Hemant'){
            steps{
                echo 'starting compiling'
                sh 'mvn compile'
            }
        }
        stage('3. Code Testing with Hemant'){
            steps{
                sh 'mvn test'
            }
        }
        stage('4. QA with Hemant'){
            steps{
                sh 'mvn checkstyle:checkstyle'
            }
        }
        stage('5. Package with Hemant'){
            steps{
                sh 'mvn package'
            }
        }
        stage('6. Run Dockerfile'){
          steps{
               sh 'docker build -t myimg .'
           }
         }
        stage('7. Port Expose'){
            steps{
                sh 'docker run -dt -p 8081:8081 --name C01 myimg'
            }
        }   
    }
}
