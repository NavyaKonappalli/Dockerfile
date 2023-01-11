pipeline {
    agent {label 'slaveone'}
    stages {
        stage('my Build') {
            steps {
                sh "echo ${BUILD_NUMBER}"
                sh 'sudo chmod -R 777 /var/run/docker.sock'
                sh 'docker build -t tomcat_build:${BUILD_NUMBER} .'
            }
        }  
        stage('publish stage') {
            agent {label 'slaveone'}
            steps {
                sh "echo ${BUILD_NUMBER}"
                sh 'docker login -u navyakonappalli -p NaMaN@5160'
                sh 'docker tag tomcat_build:${BUILD_NUMBER} navyakonappalli/tomcat:${BUILD_NUMBER}'
                sh 'docker push navyakonappalli/tomcat:${BUILD_NUMBER}'
            }
        } 
        stage( 'my deploy' ) {
        agent {label 'slavetwo'} 
            steps {
               sh 'docker rm -f mytomcat'
               sh 'docker run -d -p 8080:8080 --name mytomcat navyakonappalli/tomcat:${BUILD_NUMBER}'
            }
        }    
    } 
}
