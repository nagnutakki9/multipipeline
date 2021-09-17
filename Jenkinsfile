pipeline {
    options {
        buildDiscarder(logRotator(numToKeepStr: '10'))
        timeout(time: 120, unit: 'MINUTES')
    }
    agent {
        label 'OpenJDK8'
    }
//     tools {
//         maven "Maven 3.3"
//         jdk "OpenJDK 1.8"
//     }
    // Environment variables
    //environment {
    //}
    stages {
        stage ('Run Package') {
            steps {
                script {
                    sh "mvn clean package -Dmaven.test.skip=true"
                    //sh "mvn clean deploy -Dmaven.test.skip=true"
                    //sh "mvn jetty:run"
                    }
                }
            }
        stage ('Run Tests') {
            steps {
                echo "Running test"
                script {
                    sh "mvn clean test"
                    sh "mvn clean integration-test"
                    sh " mvn clean verify"
                }
            }
        }
//         stage ('Build Image') {
//             steps {
//                 script {
//                     sh "cd ${WORKSPACE} && sudo podman build ."
//                 }
//             }
//         }
        }
}
