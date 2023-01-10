pipeline {
    agent {label 'b'}
    stages {
        stage('my Build') {
            steps {
                sh 'docker build -t tomcat_build:${BUILD_NUMBER} .'
            }
        }  
        stage('publish stage') {
            steps {
                sh "echo ${BUILD_NUMBER}"
                sh 'docker login -u ebenneelpinto -p Neil123451!'
                sh 'docker tag tomcat_build:${BUILD_NUMBER} navyakonappalli/mynav:${BUILD_NUMBER}'
                sh 'docker push navyakonappalli/mynav:${BUILD_NUMBER}'
            }
        } 
        stage( 'my deploy' ) {
        agent {label 's'} 
            steps {
               sh 'docker pull navyakonappalli/mynav:${BUILD_NUMBER}'
               sh 'docker rm -f mytomcat'
               sh 'docker run -d -p 8080:8080 --name mytomcat navyakonappalli/mynav:${BUILD_NUMBER}'
            }
        }    
    } 
}
