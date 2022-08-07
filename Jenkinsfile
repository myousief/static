pipeline {
     agent any
     stages {
         stage('Build') {
             steps {
                 sh 'echo "Hello World"'
                 sh '''
                     echo "Multiline shell steps works too"
                     ls -lah
                 '''
             }
         }
         stage('Lint HTML') {
              steps {
                  sh 'tidy -q -e *.html'
              }
         }

         stage('Test') {
             steps {
                 sh './gradlew check'
             }
         }
          post {
              always {
                  junit 'build/reports/**/*.xml'
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
