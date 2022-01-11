def bucket_name = 'test-gitlab-jenkins'
def upload_filename = 'app.zip'
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
            archiveArtifacts artifacts: '/*.zip', followSymlinks: false, onlyIfSuccessful: true
            sh "chmod 777 ${upload_filename}"
            sh "ls -la"
            }
        }
      
        stage('upload') {
            input {
                message "Should we continue?"
                ok "Yes"
            }
            steps {
                s3Upload consoleLogLevel: 'INFO', dontSetBuildResultOnFailure: false, dontWaitForConcurrentBuildCompletion: false, entries: [[bucket: "${bucket_name}", excludedFile: '', flatten: false, gzipFiles: false, keepForever: false, managedArtifacts: false, noUploadOnFailure: true, selectedRegion: 'sa-east-1', showDirectlyInBrowser: false, sourceFile: "${upload_filename}", storageClass: 'STANDARD', uploadFromSlave: false, useServerSideEncryption: false]], pluginFailureResultConstraint: 'FAILURE', profileName: 'testings3', userMetadata: []
                sh "echo ${upload_filename} Uploaded to S3"
            }
        }
    }
}
