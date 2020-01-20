pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                echo "${params.instancetype} World!"
                sh '''#!/bin/bash

				AppID=`echo "${JOB_BASE_NAME}" | awk -F\\. \'{print $2}\'`
				echo it=$(echo "$instancetype") >> iaas.props'''
            }
        }
        stage('AWS Cloud Formation') {

			steps {
			    script {
                    def props = readProperties file:'iaas.props';
                    env['instancetype'] = props['it'];
                    env['AppID'] = props['AppID'];
                }

                echo "${it}"
                echo "${AppID}"
				
			}
		}
    }
}