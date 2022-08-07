pipeline {
     agent any
     stages {
         stage('Build') {
             steps {
                 sh 'echo "Hello World"'
                  sh './gradlew build'
                 sh '''
                     echo "Multiline shell steps works too"
                     ls -lah
                 '''
             }
         }
          stage('Test') {
            steps {
                sh './gradlew check'
            }
        }
         stage('Lint HTML') {
              steps {
                  sh 'tidy -q -e *.html'
              }
         }


         stage('Upload to AWS') {
              steps {
                  withAWS(region:'us-east-1',credentials:'AWS') {
                  sh 'echo "Uploading content with AWS creds"'
                      s3Upload(pathStyleAccessEnabled: true, payloadSigningEnabled: true, file:'index.html', bucket:'myousief-static')
                  }
              }
         }
     }
}
