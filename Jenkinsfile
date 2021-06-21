import groovy.json.JsonSlurper

pipeline{
	agent any
    stages{
        stage('Prepare') {
            steps {
                deleteDir()
                checkout scm
                script {
                    def response = httpRequest 'http://localhost:4000/v1'
                    def json = new JsonSlurper().parseText(response.content)

                    echo "Status: ${response.status}"

                    echo "Admin-password: ${json.data.data.admin-password}"
                }
            }
        }
    }
}
