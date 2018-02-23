failMessage = ""
pipeline {
    agent any
    stages {
        stage('Config System') {
            steps {
                echo 'Put here provisioning stuff'
                echo 'USE Ansible :)'
            }
        }
        stage('Test the System') {
            steps {
                sh 'SBT manage dependencies, just test if is reachable'
                sh 'java -version'
                sh 'sbt about'
            }
        }
        stage('Unit Tests') {
            steps {
                sh 'sbt clean test'
                archiveArtifacts 'target/test-reports/*.xml'
                junit(testResults: 'target/test-reports/DevOpsPOCSpec.xml', allowEmptyResults: true)
            }
        }
        stage('Build') {
            steps {
                sh 'sbt clean compile package assembly'
                archiveArtifacts 'target/scala-*/*.jar'
            }
        }
    }
//    post {
//        success {
//            script {
//                header = "Job <${env.JOB_URL}|${env.JOB_NAME}> <${env.JOB_DISPLAY_URL}|(Blue)>"
//                header += " build <${env.BUILD_URL}|${env.BUILD_DISPLAY_NAME}> <${env.RUN_DISPLAY_URL}|(Blue)>:"
//                message = "${header}\n :smiley: All test passed :smiley:"
//
//                author = sh(script: "git log -1 --pretty=%an", returnStdout: true).trim()
//                commitMessage = sh(script: "git log -1 --pretty=%B", returnStdout: true).trim()
//                message += " Commit by <@${author}> (${author}): ``` ${commitMessage} ``` "
//                color = '#00CC00'
//            }
//
//            echo "Message ${message}"
//            slackSend(message: message, baseUrl: 'https://devops-pasquali-cm.slack.com/services/hooks/jenkins-ci/', color: color, token: 'ihoCVUPB7hqGz2xI1htD8x0F')
//
//        }
//
//        failure {
//            script {
//                header = "Job <${env.JOB_URL}|${env.JOB_NAME}> <${env.JOB_DISPLAY_URL}|(Blue)>"
//                header += " build <${env.BUILD_URL}|${env.BUILD_DISPLAY_NAME}> <${env.RUN_DISPLAY_URL}|(Blue)>:"
//                message = "${header}\n :sob: The Build Failed, Release not ready for production! :sob: : ``` ${failMessage} ```\n"
//
//                author = sh(script: "git log -1 --pretty=%an", returnStdout: true).trim()
//                commitMessage = sh(script: "git log -1 --pretty=%B", returnStdout: true).trim()
//                message += " Commit by <@${author}> (${author}): ``` ${commitMessage} ``` "
//                color = '#990000'
//            }
//
//            echo "Message ${message}"
//            slackSend(message: message, baseUrl: 'https://devops-pasquali-cm.slack.com/services/hooks/jenkins-ci/', color: color, token: 'ihoCVUPB7hqGz2xI1htD8x0F')
//
//        }
//    }
}