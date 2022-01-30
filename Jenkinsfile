pipeline {
    agent any
    environment {
        NEXUS_USER         = credentials('NEXUS-USER')
        NEXUS_PASSWORD     = credentials('NEXUS-PASS')
    }
    
    parameters {
    choice choices: ['maven', 'gradle'], description: 'Seleccione una herramienta', name: 'compileTool'
    }



    stages {
        stage("Pipeline"){
            steps {
                script{
                    sh "env"
                    if(params.compileTool == 'maven'){
                        // compilamos con maven
                        def executor = load "maven.groovy"
                        executor.call()
                    }else{
                        // compila mos con Gradle    
                        def executor = load "gradle.groovy"
                        executor.call()
                    }
                }
            }
            post {
                always {
                    sh "echo 'fase always executed post'"
                }
                success {
                    sh "echo 'fase success'"
                }
                failure {
                    sh "echo 'fase failure'"
                }
            }
        }
    }
}