pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                echo "${params.instancetype} World!"
                sh '''#!/bin/bash
                proxy="test"
                instance="${instancetype}"
				echo proxy=$(echo "$proxy") > iaas.props
				echo it=$(echo "$instance") >> iaas.props'''
            }
        }
        stage('AWS Cloud Formation') {

			steps {
                
                withAWS(credentials: 'aws-credentials', region: 'us-west-2') {
                    sh 'echo "hello KB">hello.txt'
                    
                    cfnUpdate(stack:'my-stack', file:'webserver.json', params:['InstanceType': 't2.micro'])
                }
			}
		}
    }
}