def user
node {
  
emailext mimeType: 'text/html',
    subject: "[Jenkins]${currentBuild.fullDisplayName}",
    to: "shrivastavankit62@gmail.com",
    body: '''<a href="${BUILD_URL}input">click to approve</a>'''
}

pipeline {
    agent any
    stages {
        stage('Clone') {
            steps {
                sh "git clone https://github.com/ankit-since1996/jenkins_test.git/"
            }
        }
        stage('deploy') {
            input {
                message "Should we continue?"
                ok "Yes"
            }
            when {
                expression { user == 'hardCodeApproverJenkinsId'}
            }
            steps {
                sh "echo 'describe your deployment' "
            }
        }
    }
}
