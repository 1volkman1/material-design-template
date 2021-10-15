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
            sh 'ls www/js/ | xargs -I{file} uglifyjs -o www/min/{file} --compress'
          }
        }
        stage('compressed CSS'){
          steps{
            sh 'ls www/css/ | xargs -I{file} cleancss -o www/min/{file}'
          }
        }
      }
    }
    stage('Archived'){
       steps{
         sh "tar --exclude='.git' --exclude=www/js --exclude=www/css -czvf mdt.tar.gz ."
       }
    } 
  }
}
