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

                script {
                    def props = readProperties file:'iaas.props';
                    env['proxy'] = props['proxy'];
                    env['it'] = props['it'];

                    echo "${proxy}"
                    echo "${it}"
                }

				vzAWS_CF_CICD_V2 region: 'us-west-2', stackName: 'teststack', templateName: 'webserver.json', templateParameter: '{"InstanceType":"${InstanceType}"}'
			}
		}
    }
}