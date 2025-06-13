pipeline {
    agent any

    tools {
        maven 'mymaven'
    }

    environment {
        MY_ENV_VAR = 'Dev'
    }

    stages {
        stage('Check File in Remote Branch') {
            steps {
                script {
                    def repoUrl = 'https://github.com/prasannabavaraju/jenkinsfile.git'
                    def branch = 'feature'
                    def filePath = 'Jenkinsfile' // No leading slash

                    try {
                        sh """
                            git ls-remote --exit-code --heads ${repoUrl} ${branch}
                            git fetch ${repoUrl} ${branch}:${branch}
                            git show ${branch}:${filePath} > /dev/null
                        """
                        echo "File '${filePath}' exists in branch '${branch}' of remote repo."
                    } catch (Exception e) {
                        echo "File '${filePath}' does NOT exist in branch '${branch}' of remote repo."
                        // Optionally, fail the build
                        // error("File not found in remote branch")
                    }
                }
            }
        }
    }
}