pipeline {
    agent any
    stages {
        stage('build') {
            steps {
                echo "${params.instancetype} World!"
                bat 'set proxy="test" \n set it=$(echo "$instancetype") '
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