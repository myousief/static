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
         stage('Upload to AWS') {
              steps {
                  withAWS(region:'us-west-2',credentials:'AWS') {
                  sh 'echo "Uploading content with AWS creds"'
                      s3Upload(PathStyleAccessEnabled: true, PayloadSigningEnabled: true, File:'index.html', Bucket:'myousief-static', path:'/home/myousief/static/index.html')
                  }
              }
         }
     }
}
