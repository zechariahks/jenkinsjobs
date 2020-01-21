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
                    def props = readProperties file:'iaas.props';
                    env['proxy'] = props['proxy'];
                    env['it'] = props['it'];

                    echo "${proxy}"
                    echo "${it}"
                    def outputs = cfnUpdate(stack:'my-stack', file:'webserver.json', params:['InstanceType': 't2.micro'])
                }
			}
		}
    }
}