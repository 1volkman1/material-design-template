pipeline{
  agent{
    label 'worker1'
  }
  tools{
    nodejs "nodejs16"
  }
  stages{
    stage('Checksum'){
      step{
        checkout scm
      }
    }
    stage('Build'){
      parallel{
        stage('compressed JS'){
          step{
            sh 'cat www/js/* | uglifyjs -o www/min/merged-and-compressed.js --compress'
          }
        }
        stage('compressed CSS'){
          step{
            sh 'cat www/css/* | cleancss -o www/min/merged-and-minified.css'
          }
        }
      }
     stage('Archived'){
       step{
         sh 'tar -czf --exclude=.git --exclude=www/js --exclude=www/css /tmp/result.tar.gz .'
       }
      } 
    }
  }
}
