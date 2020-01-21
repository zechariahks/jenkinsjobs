pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                echo "${params.instancetype} World!"
                sh '''#!/bin/bash
                proxy="test"
                newinstancetype="t2.medium"
				echo proxy=$(echo "$proxy") > iaas.props
				echo type=$(echo "$newinstancetype") >> iaas.props'''
            }
        }
        stage('AWS Cloud Formation') {

			steps {
                script {
                    def props = readProperties file:'iaas.props';
                    env.instancetype2 = props['type'];
                }
                
                withAWS(credentials: 'aws-credentials', region: 'us-west-2') {
                    sh "printenv | sort"
                    cfnUpdate(stack:'my-stack', file:'webserver.json', params:['InstanceType': "${env.instancetype2}"])
                }
			}
		}
    }
}