import groovy.json.JsonSlurper

pipeline{
	agent any
    environment {
        GRAFANA_VERSION = '7.5.6'
    } 
    stages{
        stage('Prepare') {
        	environment {
				Vault_addr = 'http://10.68.216.206:8200'
			} 
            steps {
                deleteDir()
                checkout scm
                sh """
                    chmod +x test.sh
                    ./test.sh
                """
                script {
                    def response = httpRequest 'https://dog.ceo/api/breeds/list/all'
                    def json = new JsonSlurper().parseText(response.content)

                    echo "Status: ${response.status}"

                    echo "Dogs: ${json.message.keySet()}"
                }
            }
        }
    }
}
