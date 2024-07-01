pipeline {
    agent any
    
    triggers {
        githubPush()
    }
    
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        
        stage('Run JMeter Tests') {
            steps {
                bat """
                "C:\\Vasanth\\apache-jmeter-5.6.3\\bin\\jmeter.bat" -n -t "IfController_Demo.jmx" -l results.jtl
                """
            }
        }
        
        stage('Publish JMeter Report') {
            steps {
                perfReport filterRegex: '', sourceDataFiles: '**/*.jtl'
            }
        }
    }
}
