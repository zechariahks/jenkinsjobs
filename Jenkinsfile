pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                echo "${params.instancetype} World!"
                sh '''#!/bin/bash

				AppID=`echo "${JOB_BASE_NAME}" | awk -F\\. \'{print $2}\'`
                proxy="test"
				echo AppID=$(echo "$AppID") >> iaas.props
				echo proxy=$(echo "$proxy") >> iaas.props
				echo it=$(echo "${params.instancetype}") >> iaas.props'''
            }
        }
        stage('AWS Cloud Formation') {

			steps {

                script {
                    def props = readProperties file:'iaas.props';
                    env['AppID'] = props['AppID'];
                    env['proxy'] = props['proxy'];
                    env['it'] = props['it'];
                }
                echo "${proxy}"
                echo "${it}"
                echo "${AppID}"
				
			}
		}
    }
}