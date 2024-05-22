pipeline { 
  
   agent any

   // environment{
   //    DOCKERHUB_CREDENTIALS = credentials('ubuntu')
   // }

   stages {
   
     stage('Install Dependencies') { 
        steps { 
           sh 'npm install' 
        }
     }
     
     stage('Test') { 
        steps { 
           sh 'echo "testing application..."'
        }
      }

     // stage("Build"){
     //        steps{
     //            sh 'npm run build'
     //        }
     //    }

      stage("Build Image"){
            steps{
                sh 'docker build -t node:1.0 .'
            }
        }

     stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'docker_cred', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) {
                    sh 'docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD'
                    sh 'docker tag node:1.0 bhanu7/node:1.0'
                    sh 'docker push bhanu7/node:1.0'
                    sh 'docker logout'
                }
            }
        }

    stage('Deploy with Docker Compose') {
            steps {
                script {
                    // Ensure Docker Compose file is present
                    sh 'cat docker-compose.yml'

                    // Stop and remove any existing containers
                    sh 'docker-compose down'

                    // Start new containers
                    sh 'docker-compose up -d'
                }
            }
        }

         // stage("Deploy npm cloud application") { 
         // steps { 
         //   sh 'echo "deploying application..."'
         // }
         // }
  
   	}

   }
