pipeline{
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
            }
        }
    }
}
