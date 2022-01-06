def user
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
              
              sh "zip myapp.zip -r ."
            }
        }
      
        stage('upload') {
            input {
                message "Should we continue?"
                ok "Yes"
            }
            steps {
                s3Upload consoleLogLevel: 'INFO', dontSetBuildResultOnFailure: false, dontWaitForConcurrentBuildCompletion: false, entries: [[bucket: 'test-gitlab-jenkins', excludedFile: '', flatten: false, gzipFiles: false, keepForever: false, managedArtifacts: false, noUploadOnFailure: true, selectedRegion: 'sa-east-1', showDirectlyInBrowser: false, sourceFile: 'app.zip', storageClass: 'STANDARD', uploadFromSlave: false, useServerSideEncryption: false]], pluginFailureResultConstraint: 'FAILURE', profileName: 'testings3', userMetadata: []
                sh "echo 'Uploaded to S3' "
            }
        }
    }
}
