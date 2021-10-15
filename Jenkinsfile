pipeline{
  agent{
    label 'worker1'
  }
  tools{
    nodejs "nodejs16"
  }
  stages{
    stage('Checksum'){
      steps{
        checkout scm
      }
    }
    stage('Build'){
      parallel{
        stage('compressed JS'){
          steps{
            sh 'cat www/js/* | uglifyjs -o www/min/compress.min.js --compress'
          }
        }
        stage('compressed CSS'){
          steps{
            sh 'cat www/css/* | cleancss -o www/min/compress.min.css'
          }
        }
      }
    }
    stage('Archived'){
       steps{
         sh 'tar -czf --exclude=.git --exclude=www/js --exclude=www/css /tmp/result.tar.gz .'
       }
    } 
  }
}
