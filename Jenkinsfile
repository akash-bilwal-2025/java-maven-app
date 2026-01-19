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
            steps {
                script{
                    env.ENV = input message: "Select the environment to deploy", ok: "Done", parameters: [choice(name: 'ONE', choices: ['dev', 'staging', 'production'], description: '')]
                    gv.deployApp()
                }                
            }
        }        
    }
}
