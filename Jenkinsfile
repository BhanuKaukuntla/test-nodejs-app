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
                sh 'docker build -t my-node-app:1.0 .'
            }
        }

     stage('Docker Push') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'ubuntu', passwordVariable: 'DOCKERHUB_PASSWORD', usernameVariable: 'DOCKERHUB_USERNAME')]) {
                    sh 'docker login -u $DOCKERHUB_USERNAME -p $DOCKERHUB_PASSWORD'
                    sh 'docker tag node:1.0 bhanu7/node:1.0'
                    sh 'docker push bhanu7/node:1.0'
                    sh 'docker logout'
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
