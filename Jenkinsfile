pipeline {
    agent any
    stages {
        stage('One') {
            steps {
                echo 'Hi, all'
            }
        }
        stage('Two') {
            steps {
                input 'Do you want to proceed?'
            }
        }
        stage('Three') {
            when {
                not {
                    branch 'master'
                }
            }
            steps {
                echo 'Hello'
            }
        }
        stage('Four') {
            parallel {
                stage('Unit Test') {
                    steps {
                        echo 'Running the unit test...'
                    }
                }
                stage('Integration Test') {
                    agent {
                        docker {
                            image 'ubuntu'
                            reuseNode false
                        }
                    }
                    steps {
                        script {
                            // Convert Windows path to Unix path
                            def workspaceUnixPath = pwd().replace('\\', '/')
                            echo "Workspace Unix Path: ${workspaceUnixPath}"
                            sh "echo Running inside Docker container with workspace: ${workspaceUnixPath}"
                        }
                    }
                }
            }
        }
    }
}
