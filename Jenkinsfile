pipeline {
    agent any

    stages {
        stage('Initialize Terraform') {
            steps {
                script {
                    // Change to the Terraform directory in the Git repository
                    dir('/terraform') {
                        // Run Terraform init
                        sh 'terraform init'
                    }
                }
            }
        }

        stage('Plan Terraform') {
            steps {
                script {
                    // Change to the Terraform directory in the Git repository
                    dir('/terraform') {
                        // Run Terraform plan and save the output to a file
                        sh 'terraform plan -out=tfplan'
                    }
                }
            }
        }

        stage('Apply Terraform') {
            steps {
                script {
                    // Change to the Terraform directory in the Git repository
                    dir('/terraform') {
                        // Apply the Terraform plan
                        sh 'terraform apply -auto-approve tfplan'
                    }
                }
            }
        }
    }

    post {
        always {
            // Clean up Terraform plan file
            script {
                deleteFile('/terraform/tfplan')
            }
        }
    }
}

// Function to delete a file if it exists
def deleteFile(filename) {
    sh "rm -f ${filename}"
}

