pipeline {
    agent any

    stages {
        stage ('SCM pull') {
            steps {
                scmLibrary.scmPull()
                //SCM pull
            }
        }
        stage ('Parallel Scan') {
         parallel {
            stage ('Docker Build') {
                steps {
                    dockerLibrary.dockerBuild()
                    //docker build
                }
            }
            stage ('trivy scan') {
                steps {
                    scanLibrary.trivyScan()
                    //trivy scan
                }
            }
            stage ('bandit scan') {
                steps {
                    scanLibrary.banditScan()
                    //bandit scan
                }
            }
            stage ('sonarqube') {
                steps {
                    scanLibrary.sonarqube()
                    // sonarqube
                }
            }
         }
        }
        stage ('Parallel Test') {
            parallel {
                stage ('Docker Push') {
                    steps {
                        dockerLibrary.dockerPush()
                        // Docker push
                    }
                }
                stage ('Unit Test') {
                    steps {
                        echo "Unit Test"
                        // Unit Test
                    }
                }
                stage ('Sign Artifact') {
                    steps {
                        echo "Sign Artifact"
                        // Sign Artifact
                    }
                }
            }
        }
       
        stage ('Deploy') {
            steps {
                echo "Deploy"
                // Deploy
            }
        }
        stage ('Test') {
            steps {
                echo "Test"
                // Test
            }
        }
        stage ('Post install') {
            steps {
                echo "Post install"
                // Post install
            }
        }
    }
}