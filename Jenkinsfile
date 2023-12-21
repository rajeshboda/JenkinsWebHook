pipeline {
    agent any
    
    stages {
        stage('Validate Commit') {
            steps {
                script {
                    // Clone the repository
                    git 'https://github.com/yourusername/JenkinsWebHook.git'
                    sh "git log -1 --pretty=format:'%s' > commit_message.txt"
                    def commitMessage = readFile('commit_message.txt')
                    echo "Commit Message: $commitMessage"

                    def pattern = ~/SCO:\d{4,6}/ // Regular expression to match "SCO:" followed by 4 to 6 digits
                    if (commitMessage =~ pattern) {
                        echo "Validation Passed!"
                    } else {
                        error "Validation Failed! Commit message doesn't match the pattern SCO:***** (where * represents 4 to 6 numbers)"
                    }
                }
            }
        }
    }
}
