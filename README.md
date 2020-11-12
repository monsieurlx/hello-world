pipeline{
  agent any
  stages{
    stage('Build'){
      echo 'Building the docker images'
      echo 'docker build -t myflaskapp .'
    }
    stages('Run'){
      parallel{
        stage{'run redis'){
        steps{
          echo 'docker run -d -p 6379:6379 --name myredis redis sh au lieu de echo'
              }
             }
      stage ('run flask'){
          steps{
            echo 'docker run -d -p 5000:5000 --name
            myflaskapp_c myflaskapp'
          }
        }
      }
    }
    stage ('Testing'){
    steps{
      echo 'python test_app.py'
    }
    stage ('stop containers') {
    stages {
      steps{
        echo 'docker rm -f myflaskapp_c'
        echo 'docker rm -f redis'
        
      }
    }
    }
  }
}
