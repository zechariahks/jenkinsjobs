pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                echo "${params.instancetype} World!"
                sh '''#!/bin/bash
                proxy="test"
                export newinstancetype="t2.small"
				echo proxy=$(echo "$proxy") > iaas.props
				echo it=$(echo "$instance") >> iaas.props'''
            }
        }
        stage('AWS Cloud Formation') {

			steps {
                
                withAWS(credentials: 'aws-credentials', region: 'us-west-2') {
                    sh 'echo "hello KB">hello.txt'
                    sh "printenv | sort"
                    cfnUpdate(stack:'my-stack', file:'webserver.json', params:['InstanceType': "${env.newinstancetype}"])
                }
			}
		}
    }
}