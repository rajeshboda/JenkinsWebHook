pipeline {
    agent any
    
    stages {
        stage('Validate Commit') {
            steps {
                script {
                    // Checkout the repository explicitly
                    checkout([$class: 'GitSCM', 
                              branches: [[name: 'main']], // Replace 'master' with your branch name
                              doGenerateSubmoduleConfigurations: false, 
                              extensions: [], 
                              submoduleCfg: [], 
                              userRemoteConfigs: [[url: 'https://github.com/rajeshboda/JenkinsWebHook.git']]]) // Replace URL with your repository URL

                    // Perform your validation steps here
                    // Example: Fetch commit message
                    sh "git log -1 --pretty=format:'%s' > commit_message.txt"

                    // Read the commit message
                    def commitMessage = readFile('commit_message.txt')
                    echo "Commit Message: $commitMessage"

                    // Validation based on the commit message pattern
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
