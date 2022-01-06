def bucket_name = 'test-gitlab-jenkins'
def upload_filename = 'myapp.zip'
node {
  
emailext mimeType: 'text/html',
    subject: "[Jenkins]${currentBuild.fullDisplayName}",
    from: "shrivastavankit62@gmail.com",
    to: "shrivastavankit62@gmail.com",
    body: '''<a href="${BUILD_URL}input">click to approve</a>'''
}

pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                sh "rm -rf *"
                sh "git clone https://github.com/ankit-since1996/jenkins_test.git/"
            }
        }
        stage('build') {
          steps {
              
            sh "zip ${upload_filename} -r ."
            }
        }
      
        stage('upload') {
            input {
                message "Should we continue?"
                ok "Yes"
            }
            steps {
                s3Upload(file:"${upload_filename}", bucket:"${bucket_name}", path:"s3://test-gitlab-jenkins/${upload_filename}")
                sh "echo ${upload_filename} Uploaded to S3"
            }
        }
    }
}
