pipeline {
    agent { label 'windows-11-slave' }

    environment {
        // Define the location of the Git repository and credentials
        POSTMAN_COLLECTION = 'UserManagementAPITestForCI.postman_collection.json'
        REPORT_DIR = 'newman'
        JUNIT_REPORT = "${REPORT_DIR}/*.xml"
    }

    stages {
        stage('Run Postman Tests') {
            steps {
                // Run the Postman collection using Newman command-line tool
                bat "newman run ${POSTMAN_COLLECTION} -r \"cli,junit\" " 
            }
        }
    }

    post {
        success {
            // Publish JUnit test results from Newman only when pass
            junit "${JUNIT_REPORT}"
        }
    }
}
