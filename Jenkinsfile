pipeline { 
  
   agent any

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

     stage("Build"){
            steps{
                sh 'npm run build'
            }
        }

      stage("Build Image"){
            steps{
                sh 'docker build -t my-node-app:1.0 .'
            }
        }

         // stage("Deploy npm cloud application") { 
         // steps { 
         //   sh 'echo "deploying application..."'
         // }
         // }
  
   	}

   }
