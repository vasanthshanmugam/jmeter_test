pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/vasanthshanmugam/jmeter_test' // Replace with your repository URL
            }
        }

        stage('Run JMeter Test') {
            steps {
                script {
                    def jmeterHome = tool name: 'JMeter', type: 'JMeterInstallation'
                    sh "${jmeterHome}/bin/jmeter -n -t IfController_Demo.jmx -l results.jtl"
                }
            }
        }

        stage('Publish Results') {
            steps {
                perfReport sourceDataFiles: 'results.jtl'
            }
        }

        stage('Email Notification') {
            steps {
                mail to: 'vasanthtce@gmail.com',
                     subject: "Performance Test Results",
                     body: "The performance tests have completed. Please check the Jenkins job for detailed results."
            }
        }
    }
}
