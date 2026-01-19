def gv
pipeline {
    agent any
    parameters {
        choice( name : 'VERSION', choices: ['1.1.2', '1.4.3', '1.4.2'], description: '')
        booleanParam(name: 'executeTests', defaultValue: true, description: '')
    }

    stages {
        stage('init') {
            steps {
                script{
                    gv = load "script.groovy"
                }                
            }
        }
        stage('build') {
            steps {
                script{
                    gv.buildApp()
                }                
            }
        }
        stage('Test') {
            steps {
                script{
                    gv.testApp()
                }                
            }
        }
        stage('deploy') {
            input{
                message "Select the environment to deploy"
                ok "Done"
                parameters {
                    choice(name: 'ENV', choices: ['dev', 'staging', 'production'], description: '')
                }                
            }
            steps {
                script{
                    gv.deployApp()
                    echo "deploying to the ${ENV}"
                }                
            }
        }        
    }
}
