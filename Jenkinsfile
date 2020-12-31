def gv
//the above gv will be later used for holding the groovy script file.

/* this is a multi-line comment in jenkinsfile
  the jenkinsfile shold be named Jenkinsfile with capital J.
  Jenkinsfile to be maintained in the root repo folder.
*/

// this is a single line comment in jenkinsfile


pipeline {
    agent any 
    //the above makes sure that this job can run on any of the available jenkins servers.
    //define all the buld toold needed for the execution so that we dont have to specifically refer to the build tool in the steps.
    
    tools {
    gradle ‘Gradle-6.2’
    }
    
    //below are the parameters or variables defined which can be used in the scrips directly or even within the external groovy scripts
    parameters {
        choice(name: 'VERSION', choices: ['1.1.0', '1.2.0', '1.3.0'], description: '')
        booleanParam(name: 'executeTests', defaultValue: true, description: '')
    }
    stages {
        stage("init") {
            steps {
                script {
                //loading the external groovy script to a variable
                   gv = load "script.groovy" 
                }
            }
        }
        stage("build") {
            steps {
                script {
                //call a groovy file method from the variable holding the entire groovy script
                    gv.buildApp()
                }
            }
        }
        stage("test") {
        //conditional execution in jenkins file steps
            when {
                expression {
                    params.executeTests
                }
            }
            steps {
                script {
                    gv.testApp()
                }
            }
        }
        stage("deploy") {
            steps {
                script {
                    gv.deployApp()
                }
            }
        }
    }   
}
