pipeline {

    agent any

    parameters {
        booleanParam(name: "RUN_INTEGRATION_TESTS", defaultValue: true)
    }

    stages {
        stage('Test') {
            parallel {
                stage('Unit tests') {
                    steps {
                        sh './mvnw test -D testGroups=unit'
                    }
                }
                stage('Integration tests') {
                    when {
                        expression { return param.RUN_INTEGRATION_TESTS }
                    }
                    steps {
                        echo "uintegration"
                    }
                }

            }
        }

        stage("Build") {
            steps {
                script {
                    try {
                        sh './mvnw package -D skipTests'
                    } catch (ex) {
                        echo "Error while generating JAR file"
                        throw ex
                    }
                }
            }
        }
}
}