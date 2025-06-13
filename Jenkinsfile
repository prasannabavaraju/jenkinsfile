pipeline {
    agent any
    tools {
        maven 'mymaven'
    }
    stages {
        stage('Check Jenkinsfile in Branches') {
            steps {
                script {
                    def branches = ['master',  'feature']
                    for (branch in branches) {
                        retry(3) {
                            try {
                                echo "Checking Jenkinsfile in branch: ${branch}"
                                // Replace the following with your actual Git command or logic
                                sh "git fetch origin ${branch}"
                                sh "git show origin/${branch}:Jenkinsfile"
                                echo "Jenkinsfile found in ${branch}"
                            } catch (err) {
                                echo "Jenkinsfile not found in ${branch} or error occurred: ${err}"
                                // Optionally, you can fail or continue
                                // error("Stopping pipeline due to missing Jenkinsfile in ${branch}")
                            }
                        }
                    }
                }
            }
        }
    }
}