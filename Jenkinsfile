import groovy.json.JsonSlurper

pipeline{
	agent any
	environment {
	    vault_token = 's.uwrjN7r94O60oEBxATtseAfi'
	}
    stages{
        stage('Prepare') {
            steps {
                deleteDir()
                checkout scm
                script {
                	def Json_data = getSecretsJson("${vault_token}")
                    def password = getSecret(Json_data,"db-password")
                    def user = getSecret(Json_data,"db-user")
                }
            }
        }
    }
}

def getSecretsJson(token) {
    def response = httpRequest url: 'http://localhost:4000/v1', customHeaders: [[name:'X-Vault-Token', value: token]]
    def json = new JsonSlurper().parseText(response.content)
    return json
}

def getSecret(json, key) {
    return json.data.data.get(key)
}
