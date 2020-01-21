pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                echo "${params.instancetype} World!"
                bat 'set proxy="test" >> iaas.props '
                bat  'set it=${params.instancetype} >> iaas.props '
            }
        }
        stage('AWS Cloud Formation') {

			steps {

                bat  'echo %it%'
                bat  'echo %proxy%'
				
			}
		}
    }
}