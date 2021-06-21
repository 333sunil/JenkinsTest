import groovy.json.JsonSlurper

pipeline{
	agent any
	environment {
	    token = 's.uwrjN7r94O60oEBxATtseAfi'
	}
    stages{
        stage('Prepare') {
            steps {
                deleteDir()
                checkout scm
                script {
                    def json = getSecretsJson()
                    env.DB_PASSWORD = getSecret(json,"db-password")
                    env.DB_USER = getSecret(json,"db-user")
                }
                sh """
		            	chmod +x ./test.sh
		            	./test.sh
                """
            }
        }
    }
}

def getSecretsJson() {
    def response = httpRequest url: 'http://localhost:4000/v1', customHeaders: [[name:'X-Vault-Token', value: "$token"]]
    def json = new JsonSlurper().parseText(response.content)
    return json
}

def getSecret(json, key) {
    return json.data.data.get(key)
}
