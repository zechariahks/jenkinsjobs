pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                echo "${params.instancetype} World!"
                sh '''#!/bin/bash

				AppID=`echo "${JOB_BASE_NAME}" | awk -F\\. \'{print $2}\'`
                proxy="test"
                echo proxy=$(echo "$proxy") >> iaas.props
				echo it=$(echo "$instancetype") >> iaas.props'''
            }
        }
        stage('AWS Cloud Formation') {

			steps {

                echo "${it}"
                echo "${AppID}"
                echo "${proxy}"
				
			}
		}
    }
}